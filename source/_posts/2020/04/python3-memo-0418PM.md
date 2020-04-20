---
title: python3 memo 0418PM
categories:
  - 技术
tags:
  - python3
date: 2020-04-20 20:11:38
---

## python3 memo 0418PM

python3的随堂笔记，这是最后一部分。

``` python

# 异常
try:
    print('A')
    a = 1 / 2
    print('B')
except: # 捕获异常
    print('C')
else:   # 没有异常
    print('D')
finally:
    print('E')

# 有异常：ACE
# 无异常：ABDE

# 跟踪信息
import traceback
try:
    a = 1 / 0
except ZeroDivisionError as e:
    # print(e)  # 异常信息
    traceback.print_exc() # 打印跟踪信息
except:
    print('出现异常2')

# 抛出异常
raise EOFError('出现异常')

# 定义一个函数，求n个数字的最大值
# max(1, 2, 3)
# max([1 , 2, 3])
# max()  TypeError: max expected 1 arguments, got 0
def findMax(*a):
    if a:
        return max(a)
    else:
        raise TypeError('max expected 1 arguments, got 0')

print(findMax())

# 文件操作
# 路径表示方法
# e:\\a.txt
# r'e:\a.txt'
# e:/a.txt
# 操作模式 r

# 基本读
f = open('e:/a.txt', 'r', encoding='utf-8')

# 一次性读
print(f.read())

# 多次读
while True:
    c = f.read(1024)
    if c:
        print(c)
    else:
        break

f.close()

# 改进1：通过with打开的文件，会自动关闭
with open('e:/a.txt', 'r', encoding='utf-8') as f:
    print(f.read())

# 改进2：按行读
with open('e:/a.txt', 'r', encoding='utf-8') as f:
    for line in f:
        print(line)

# 写文件
lineNumber = 1
with open('e:/a.txt', 'r', encoding='utf-8') as f, open('e:/b.txt', 'w', encoding='utf-8') as fw:
    for line in f:
        fw.write(str(lineNumber) + ' ' + line)
        lineNumber += 1

# time
import time
print(time.time()) # 1587193114.2873852
print(time.localtime())
print(time.strftime('%Y-%m-%d %H:%M:%S'))  # 2020-04-18 15:00:56

# 爬取数据：urllib，scrapy
# 解析数据：正则表达式，Beautiful Soup，scrapy

# .*: 贪婪匹配，匹配更多的字符，在结尾
# .*?: 非贪婪匹配，匹配最少的字符，在中间
import urllib.request
import re

resp = urllib.request.urlopen('http://www.xxx.com.cn/cn/index.action?locale=zh_CN')
html = resp.read().decode('utf-8')

news = re.findall('<li class="newsList">.*?title="(.*?)".*?</li>', html, re.S)
print(news)

# 数据库操作
import pymysql

config = {
    'host': '127.0.0.1',
    'port': 3306,
    'user': 'root',
    'password': '123456',
    'database': 'world'
}
con = pymysql.connect(**config)
sql = 'select * from country'

try:
    # 所有操作必须通过游标完成
    with con.cursor() as c:
        c.execute(sql) # 执行SQL
        result = c.fetchall() # 提取结果，((行),(行),(行))
        for row in result:
            print(row)

    con.commit()
except:
    con.rollback()
finally:
    con.close()

```

### 补充：解决pip无法安装问题

更换安装源，使用方法很简单，直接 -i 加 源url 即可！例如：
`pip install pymysql -i http://pypi.douban.com/simple --trusted-host pypi.douban.com`

其他源：
```
阿里云 http://mirrors.aliyun.com/pypi/simple/
中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/ 
豆瓣(douban) http://pypi.douban.com/simple/ 
清华大学 https://pypi.tuna.tsinghua.edu.cn/simple/
中国科学技术大学 http://pypi.mirrors.ustc.edu.cn/simple/
```
