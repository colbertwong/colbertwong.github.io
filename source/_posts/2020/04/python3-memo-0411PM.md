---
title: python3 memo 0411PM
categories:
  - 技术
tags:
  - python
date: 2020-04-12 13:35:52
---

## python3 memo 0411PM

python3的随堂笔记，这是第二部分。

``` python

# 猜数字
import random

n = random.randint(1, 10)
# print(n)

while True:
    m = int(input('请输入:'))
    if m == n:
        print('相等')
        break
    elif m > n:
        print('大了')
    else:
        print('小了')

# python中没有switch/case
# 输入月份，求当前月份中的天数
# switch(month) {
#     case 1:
#     case 3:
#     case 5:
#     // ..
#     case 12: System.out.println(31); break;
#     // ..
# }

month = int(input('请输入月份: '))
if month in [1, 3, 5, 7, 8, 10, 12]:
    print(31)
elif month in [4, 6, 9, 11]:
    print(30)
else:
    print(28)

# while: 求100~200之间的素数
# 注意：缩进
i = 100
while i <= 200:

    j = 2
    while j < i:
        if i % j == 0:
            break
        j += 1
    else:  # 循环条件不成立时执行else，如果break，else不执行
        print(i)

    i += 1

# for: 相当于Java中的for/each
for m in [1, 3, 4, 2, 11]:
    print(m)
else:
    print('else')

# range(5): 0, 1, 2, 3, 4
# range(5, 10): 5, 6, 7, 8, 9
# range(5, 10, 2): 5, 7, 9
# range(10, 1, -1): 10, ... , 2
for i in range(10, 1, -1):
    print(i)

# 求和：1 + 2 + ... + 100
sum = 0
for i in range(1, 101):
    sum += i
print(sum)

# 求水仙花数，要求：3位数，153 = 1^3 + 5 ^3 + 3^3
for i in range(100, 1000):
    s = str(i)
    if i == int(s[0]) ** 3 + int(s[1]) ** 3 + int(s[2]) ** 3:
        print(i)


# 数据结构
# 序列：列表，元祖，字符串
# 映射：字典
# 集合：集合

# 序列通用操作
# 索引
a = [1, 11, 2, 33]
print(a[1])
print(a[-1])  # 33

# 切片：【左闭右开】
# 第一个参数：代表开始位置,省略到序列的开头
# 第二个参数：代表结束位置（不包括）,省略到序列的末尾
# 第三个参数：步长，默认是1
a = ['aa', 'bb', 'cc']
print(a[1: 2])

# 相加：连接
# 乘法：重复出现
a = [1, 2] * 7
print(a) # [1, 2, 1, 2, 1, 2, 1, 2, 1, 2, 1, 2, 1, 2]

# None：相当于Java中null
a = [None] * 7
print(a) # [None, None, None, None, None, None, None]

# 常用函数
# len() max() min() sum()
a = [1, 22, 33, 4]
print(len(a), max(a), min(a)) # 4 33 1

# 求3个数字的最大值
a = int(input('a: '))
b = int(input('b: '))
c = int(input('c: '))

m = max([a, b, c])
print(m)

# 变量交换
a = 1
b = 2
a, b = b, a

# 列表：模拟打分
# 5个评委，去掉一个最高分，去掉一个最低分，剩下求平均值
list = [None] * 5
for i in range(5):
    list[i] = int(input('请输入：'))
# 方法1
avg = (sum(list) - max(list) - min(list)) / (len(list) - 2)
print(avg)
# 方法2
list.sort()
list2 = list[1: len(list) - 1]
print(sum(list2) / len(list2))

# tuple
# 只读的列表
a = (1, 2, 3)
print(type(a))  # <class 'tuple'>

# 注意事项
# 默认情况下，()代表数学上括号
# 如果想创建只有一个元素的tuple，需要在元素后加逗号
a = (1,)
print(type(a))  # <class 'tuple'>

# 字符串，一些常用函数
# ''.format()
# ''.endswith()
# ''.startswith()
# ''.find()
# ''.isalpha()
# ''.isdigit()
# ''.islower()
# ''.isupper()
# ''.lower()
# ''.upper()
# ''.strip()
# ''.lstrip()
# ''.rstrip()
# ''.replace()
# ''.split()

# Set: 集合，消除重复的元素，集合运算

# 字典：相当于Map
# []: 列表，(): 元祖，{}: 字典
dict = {'key': '11', 'key': '22'};
print(dict['key'])  # 后面的值，会替换前一个值，22
print(dict['key2'])  # key2不存在，KeyError: 'key2'

# 通过get取值
print(dict.get('key2'))  # None
print(dict.get('key2', 0))  # 当key不存在，返回第二个参数

# 求英文中，每个字母出现的次数
# 字典：key：字母；value：出现次数
str = 'Process finished with exit code 0'
dict = {}
for c in str:
    if c.isalpha():
        dict[c] = dict.get(c, 0) + 1
# 遍历
for k, v in dict.items():
    print(k, v)


# 定义: dict = {key:value}
# 存值: dict[key] = value
# 取值：dict.get(key)
# 遍历：for

# 函数
# 不写返回类型
# """ doc string """
def func(a, b):
    """ doc string """
    return a + b


print(func(1, 2))

```
