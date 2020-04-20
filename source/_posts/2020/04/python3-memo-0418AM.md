---
title: python3 memo 0418AM
categories:
  - 技术
tags:
  - python3
date: 2020-04-20 20:00:49
---

## python3 memo 0418AM

python3的随堂笔记，这是第三部分。

``` python

# 函数
# 定义函数，求两个数字的最大公约数
def gongyue(a, b):
    """ 求最大公约数 """
    result = 1
    for i in range(1, min(a, b) + 1):
        if a % i == 0 and b % i == 0:
            result = i
    return result

print(gongyue(5, 10))

# 别名: 函数名指向函数的指针
f = gongyue
print(f(50, 10))

# 参数类型
# 不可变的类型(改变后创建一个新值): string, number, tuple
# 可变的类型： list, dict
def method(a):
    a = '123'
    print(id(a)) # 1858020758960

b = 'abc'
print(id(b)) # 1858020668336
method(b)
print(b) # abc

# 默认参数: 必须出现在参数列表的右侧
def method(a, b = 1):
    pass

method(1, 2)
method(1)

# 可变参数，a tuple类型
# 最少的个数0，最多不限制
def method(*a):
    print(a)

method()
method(1, 2, 3)
method(1, 2, 3, '4', 5)

# 关键字参数：给指定的参数赋值
def method(a, b):
    pass

method(b = 1, a = 2)
method(3, b = 4)

# **形参：按关键字参数传值，形参得到字典
def method(**a):
    print(a) # {'x': 1, 'y': 2, 'z': 3}

method(x = 1, y = 2, z = 3) # 关键字参数

# **实参：把字典转换成关键字参数
def method(a, b):
    pass

kw = {'b': 1, 'a': 2}
method(**kw)

# 组合: 必写参数，[可变参数，默认参数]，关键字参数
def print(self, *args, sep=' ', end='\n', file=None)
def method(x, y = 1, *z, **kw):
    print(x, y, z)

def method(x, *z, y = 1, **kw):
    pass

# 匿名函数，:前是形参，:后是返回表达式
# 相当于
def method(x, y, z):
    return x + y + z

method = lambda x, y, z : x + y + z
print(method(1, 2, 3))


# 作用域
a = 1  # 全局作用域
def method1():
    global a  # 声明使用全局变量
    a = 2
    b = 3 # 闭包函数外的变量
    def method2():
        global a  # 声明使用全局变量
        nonlocal b  # 声明使用闭包函数外的变量

# 导入模块
# 1: 文件名.函数名
import Hello2
Hello2.getSalary()

# 2.函数名
from Hello2 import *
getSalary()

# 包: 相当于文件夹 + __init__.py
# 在文件名前加包名，两种写法都支持
import util.Hello2
util.Hello2.getSalary()

# 类
class Student:
    # 类属性
    clazz = '1班'

    #构造函数
    def __init__(self, id, name):
        # 实例属性
        self.id = id
        self.name = name

    #方法
    def print_student(self):
        print(self.id, self.name)

# 创建对象，没有new关键字
stu1 = Student(1, '张')
# 访问实例属性，对象与对象之间独立
print(stu1.id, stu1.name) # 1 张
# 调用函数
stu1.print_student() # 1 张
# 访问类属性，可以通过对象名.，类名.访问，全局唯一，与对象无关
print(stu1.clazz, Student.clazz)
Student.clazz = '2班'

stu2 = Student(2, 'Lee')
stu2.print_student() # 2 Lee
print(stu2.clazz)  # 2班


class Emp:
    __name = 'Lee'  # 私有类属性
    _dept = 'HR'  # 保护型类属性，编码上的约定

print(Emp.__name)

class Emp:
    # 普通方法: 通过对象调用
    def method1(self):
        pass

    # 类方法: 通过类名调用
    @classmethod
    def method2(cls): # cls类名
        pass

    # 静态方法: 通过类名调用
    @staticmethod
    def method3():
        pass

# 继承
class Parent:
    a = 1

    def __init__(self, x):
        self.b = 2
        self.x = x

    def method(self):
        pass

class Sub(Parent):
    a = 2  # 属性隐藏

    def __init__(self, x):
        super().__init__(x)  # 调用父类的构造函数

    def method(self): # 方法重写
        print('sub')

# 子类可以继承类属性、实例属性、方法
# 没有方法重载
# 调用父类的构造函数  super().__init__(x)
obj = Sub(100)
print(obj.a, obj.b, obj.x)
obj.method()

```
