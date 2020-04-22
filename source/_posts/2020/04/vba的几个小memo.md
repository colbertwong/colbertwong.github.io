---
title: vba的几个小memo
categories:
  - 技术
tags:
  - vba
date: 2020-04-22 10:46:19
---

## vba的几个小memo

帮同事写了一个vba小工具。需求是将某目录下的一些excel表格的内容（CRUD），按照某个维度（画面ID）进行合并，输出在一个新excle表格中。用到了几个vba的小知识点，memo一下。

1. 文件夹下所有文件取得
2. 字典（用于记录合并key的map）
3. 文本文件输出（记录日志）

``` vb

' vba源代码
Sub update_Click()
    ' 定义变量
    Dim myFso As Object
    Dim myFiles
    Dim sh As Variant
    Dim strWorkPath As String
    Dim strWorkBook As String
    Dim shtWork As Worksheet
    Dim strMyBook As String
    Dim lngRow As Long
    Dim lngNewRow As Long
    Dim lngLoopRow As Long
    Dim lngLoopCol As Long
    Dim strSheet As String
    Dim strCRUD As String
    Dim i As Integer
    Dim flgFound As Boolean
    Dim dict As Object

    Application.ScreenUpdating = False

    If MsgBox("确定要更新一览的内容吗？", vbYesNo) = vbNo Then
        Exit Sub
    End If

    lngNewRow = 2
    strMyBook = ActiveWorkbook.Name

    ' 删除表格中第四行所有内容
    Rows(4 & ":" & Cells(4, 2).End(xlDown).Row).Delete shift:=xlUp
    ' 清楚第三行内容，保留格式
    Rows(3).ClearContents
    ' 取得当前目录下文件一览
    Set myFso = CreateObject("Scripting.FileSystemObject")
    Set myFiles = myFso.GetFolder(ActiveWorkbook.Path).Files
    ' 以输出模式打开日志文件log.txt
    Open ActiveWorkbook.Path & "\log.txt" For Output As #1
    ' 创建字典对象
    Set dict = CreateObject("Scripting.Dictionary")
    
    For Each sh In myFiles
        If InStr(sh.Name, "CRUD(") <> 0 Then
            strWorkPath = sh.Path
            strWorkBook = sh.Name
            Application.StatusBar =  strWorkBook & "文件处理中..."
            ' 只读方式打开文件
            Workbooks.Open Filename:=strWorkPath, ReadOnly:=True, UpdateLinks:=0
            Set shtWork = Workbooks(strMyBook).Sheets(1)
            With Workbooks(strWorkBook).Sheets("CRUD")
                ' 显示所有隐藏列
                .Columns.Hidden = False
                lngLoopCol = 6
                Do Until .Cells(4, lngLoopCol) = ""
                    flgFound = False
                    ' 判断字典中key是否存在
                    If dict.exists(.Cells(5, lngLoopCol).Value) Then
                        flgFound = True
                        ' 取出字典中的值
                        lngRow = dict.Item(.Cells(5, lngLoopCol).Value)
                    End If

                    If Not flgFound Then
                        lngNewRow = lngNewRow + 1
                        lngRow = lngNewRow
                        If .Cells(5, lngLoopCol) = "" Then
                            .Cells(5, lngLoopCol) = "UNKNOWN" & (lngRow - 2)
                        End If
                        ' 追加字典中的项目，key尽量用字符串，不要用对象
                        dict.Add .Cells(5, lngLoopCol).Value, lngRow
                        shtWork.Rows(lngRow).Insert CopyOrigin:=xlFormatFromRightOrBelow
                        ' 序号
                        shtWork.Cells(lngRow, 2) = lngRow - 2
                        ' 画面ID
                        shtWork.Cells(lngRow, 3) = .Cells(5, lngLoopCol)
                        ' 画面名
                        shtWork.Cells(lngRow, 4) = .Cells(4, lngLoopCol)
                    End If
                     ' CRUD合并，去重
                    lngLoopRow = 7
                    Do Until .Cells(lngLoopRow, 3) = ""
                        ' 向日志文件中写入内容
                        Print #1, strWorkBook & "->" & .Cells(5, lngLoopCol) & .Cells(lngLoopRow, 5) & "." & .Cells(lngLoopRow, 3) & " : " & .Cells(lngLoopRow, lngLoopCol)
                        If .Cells(lngLoopRow, lngLoopCol) <> "" Then
                            strCRUD = .Cells(lngLoopRow, lngLoopCol)
                            For i = 1 To Len(strCRUD)
                                If InStr(shtWork.Cells(lngRow, 5), Mid(strCRUD, i, 1)) = 0 Then
                                    shtWork.Cells(lngRow, 5) = shtWork.Cells(lngRow, 5) & Mid(strCRUD, i, 1)
                                End If
                            Next
                            ' 表名
                            shtWork.Cells(lngRow, 6) = shtWork.Cells(lngRow, 6) & .Cells(lngLoopRow, 5) & "." & .Cells(lngLoopRow, 3) & "(" & .Cells(lngLoopRow, lngLoopCol) & ")" & Chr(10)
                        End If
                        
                        lngLoopRow = lngLoopRow + 1
                    Loop

                    ' CRUD顺序整理
                    If shtWork.Cells(lngRow, 5) <> "" Then
                        strCRUD = ""
                        If InStr(shtWork.Cells(lngRow, 5), "C") Then
                            strCRUD = strCRUD & "C"
                        End If
                        If InStr(shtWork.Cells(lngRow, 5), "R") Then
                            strCRUD = strCRUD & "R"
                        End If
                        If InStr(shtWork.Cells(lngRow, 5), "U") Then
                            strCRUD = strCRUD & "U"
                        End If
                        If InStr(shtWork.Cells(lngRow, 5), "D") Then
                            strCRUD = strCRUD & "D"
                        End If
                        shtWork.Cells(lngRow, 5) = strCRUD
                    End If

                    lngLoopCol = lngLoopCol + 1
                Loop
            End With
            ' 关闭文件，不保存
            Workbooks(strWorkBook).Close saveChanges:=False
        End If
    Next
    ' 关闭日志文件
    Close #1
    Application.StatusBar = False
    Set myFso = Nothing
    Application.ScreenUpdating = True
End Sub

```

补充：同时打开多个文件进行处理数据时，要明确指出文件对象，不要相信什么默认当前文件对象。
