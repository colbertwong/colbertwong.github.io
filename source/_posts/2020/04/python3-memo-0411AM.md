---
title: python3 memo 0411AM
categories:
  - 技术
tags:
  - python3
date: 2020-04-12 10:26:35
---

## python3 memo 0411AM

python3的随堂笔记，这是第一部分。

``` python

import keyword

# 几个特别的关键字：False, True, elif
print(keyword.kwlist)

# 强类型: 不能自动完成类型转换
print(1 + '2') # error

# 动态语言：可以接受任意类型
a = 1
a = 'abc'
print(a) # abc

# 默认所有接收输入，字符串类型
# int(): 类型转换函数
a = input('请输入一个数字:')
print(int(a) + 1) # 正确计算

# 显示类型和内存地址
print(type(a)) # <class 'str'>
print(id(a)) # 2081020976816

b = 2000
print(id(b)) # 140729862683744
c = 2000
print(id(c)) # 140729862683744

# 数值类型
# / 除法：能除到小数
# // 地板除
# ** 乘方
print(10 // 3)  # 3
print(10 // -3)  # -4, 地板除(向下取整)
print(10 % -3)  # -2, 10 - (-3) * (-4)
print(-10 % -3)  # -1, -10 - (-3) * 3

# bool True对应1，False对应0 ,布尔型是数值类型
a = True
print(a + 1)  # 2

# 强制转换
# int(), float(), bool(), str()

# 自动转换（数值内部，包括bool类型）

# 字符串类型：
# 多行字符串表示，三个引号
# r,R 不转义

# 取子字符串，【左闭右开】，切片操作 
# 第一个参数：代表开始位置,省略到字符串的开头
# 第二个参数：代表结束位置（不包括）,省略到字符串的末尾
# 第三个参数：步长，默认是1
a = '1234567'
print(a[0])  # 1
print(a[0:1])  # 1
print(a[1:])
print(a[:2])
print(a[:])  # 1234567, id() ?
print(a[::2])  # 1357

# *：重复字符串
# +: 连接字符串
print('*' * 30)
print('*' + ' ' * 10 + 'Hello' + ' ' * 13 + '*')
print('*' * 30)

print('abd' in 'abcdefg')  # False, 相当于contains(), indexOf()

# 格式化 %
print('Hello, %s' % 100)
print('Hello, %s%s' % (100, 200))
print('Hello, %.2f%.2f' % (100, 200))

print(1, 'abc', '333', sep='|', end='')  # 1|abc|333
print(1, 'abc', '333', sep='|')

# 格式化 format()
print('Hello, {}-{}'.format(100, 200))
print('Hello, {1}-{0}'.format(100, 200))  # Hello, 200-100
print('Hello, {a}-{b}'.format(a=100, b=200))
print('Hello, {a:.2f}-{b}'.format(a=100, b=200))

# Python中没有++，--
# ==：判断值是否相等；is：判断地址是否相等

a = '123'
b = '123'
print(a == b)
print(a is b)
print(id(a), id(b))

```