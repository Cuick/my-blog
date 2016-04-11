+++
date = "2016-04-11T15:58:49+08:00"
title = "python-特性(切片、迭代...)"

tags = [ "python" ]
categories = [
  "python"
]

+++
<!--more-->

## 切片

取一个list或tuple的部分元素
* L[0:3]表示，从索引0开始取，直到索引3为止，但不包括索引3。即索引0，1，2，正好是3个元素。
* 如果第一个索引是0，还可以省略L[:3]
* 倒数第一个元素的索引是-1。L[-2:-1]
* L[:]就可以原样复制一个list
* tuple也是一种list，唯一区别是tuple不可变。因此，tuple也可以用切片操作，只是操作的结果仍是tuple：
* 字符串'xxx'也可以看成是一种list，每个元素就是一个字符。因此，字符串也可以用切片操作，只是操作结果仍是字符串：
* L[:10:2],前10个数，每两个取一个

## 迭代

* dict的存储不是按照list的方式顺序排列，所以，迭代出的结果顺序很可能不一样
* 判断一个对象是可迭代对象用collections模块的Iterable进行判断

        >>> from collections import Iterable
        >>> isinstance('abc', Iterable) # str是否可迭代
        True
        >>> isinstance([1,2,3], Iterable) # list是否可迭代
        True
        >>> isinstance(123, Iterable) # 整数是否可迭代
        False
* Python内置的enumerate函数可以把一个list变成索引-元素对，这样就可以在for循环中同时迭代索引和元素本身

        >>> for i, value in enumerate(['A', 'B', 'C']):
        ...     print(i, value)
        ...
        0 A
        1 B
        2 C

## 列表生成式

* range(3)  [0,1,2]
* [x * x for x in range(1, 11)]  生成[1*1,2*2 ... 11*11]
* [x * x for x in range(1, 11) if x % 2 == 0] 偶数的平方的列表
* 两层循环

        >>> [m + n for m in 'ABC' for n in 'XYZ']
        ['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']

* 运用列表生成式，可以快速生成list，可以通过一个list推导出另一个list，而代码却十分简洁。
* 在python3.x里range生成的是一个迭代对象而不是list，要想生成list需要list(range(n))

## 生成器

* 通过列表生成式，我们可以直接创建一个列表。但是，受到内存限制，列表容量肯定是有限的。而且，创建一个包含100万个元素的列表，不仅占用很大的存储空间，如果我们仅仅需要访问前面几个元素，那后面绝大多数元素占用的空间都白白浪费了。

* 列表元素可以按照某种算法推算出来，我们是否可以在循环的过程中不断推算出后续的元素,这样就不必创建完整的list，从而节省大量的空间。

* 这种一边循环一边计算的机制，称为 *生成器* （Generator）。

* 创建生成器：把一个列表生成式的[]改成()

        >>> L = [x * x for x in range(10)]
        >>> L
        [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
        >>> g = (x * x for x in range(10))
        >>> g
        <generator object <genexpr> at 0x104feab40>
* 获得每个元素

        >>> g.next()
        0
        >>> g.next()
        1
        ...
        >>> g.next()
        64
        >>> g.next()
        81
        >>> g.next()
        Traceback (most recent call last):
          File "<stdin>", line 1, in <module>
          StopIteration

* 因为generator也是可迭代对象

        >>> g = (x * x for x in range(10))
        >>> for n in g:
        ...     print n
        ...
        0
        1
        4
        9
        16
        25
        36

    创建了一个generator后，很少调用next()方法，而是通过for循环来迭代它

* 如果一个函数定义中包含yield关键字，那么这个函数就不再是一个普通函数，而是一个generator：

        def fib(max):
            n, a, b = 0, 0, 1
            while n < max:
                yield b
                a, b = b, a + b
                n = n + 1

    generator和函数的执行流程不一样。函数是顺序执行，遇到return语句或者最后一行函数语句就返回。而变成generator的函数，在每次调用next()的时候执行，遇到yield语句返回，再次执行时从上次返回的yield语句处继续执行。

# 迭代器

* 可作用于for循环的对象都是可迭代对象Iterable类型；
* 可作用于next()函数的对象都是迭代器Iterator类型，它们表示一个惰性计算的序列；
* 集合数据类型如list、dict、str等是可迭代对象Iterable但不是迭代器Iterator，不过可以通过iter()函数获得一个迭代器Iterator对象。
* 生成器generator都是迭代器Iterator
