+++
date = "2016-03-20T17:57:49+08:00"
title = "字典删除元素"

tags = [ "python", "字典"]
categories = [
  "python"
]

+++

# Python 字典删除元素clear、pop、popitem

### clear()

clear()方法是用来清除字典中的所有数据，因为是原地操作，所以返回None（也可以理解为没有返回值）

    >>> x['name'] = 'lili'
    >>> x['age'] = 20
    >>> x
    {'age': 20, 'name': 'lili'}
    >>> returned_value = x.clear()
    >>> x
    { }
    >>> print returned_value
    None

    字典的clear()方法有什么特点：
    >>> f = {'key':'value'}
    >>> a = f
    >>> a
    {'key': 'value'}
    >>> f.clear()
    >>> f
    {}
    >>> a
    {}
当原字典被引用时，想清空原字典中的元素，用clear()方法，a字典中的元素也同时被清除了。
<!--more-->

### pop()

移除字典数据pop()方法的作用是：删除指定给定键所对应的值，返回这个值并从字典中把它移除。注意字典pop()方法与列表pop()方法作用完全不同。

    >>> x = {'a':1,'b':2}
    >>> x.pop('a')
    1
    >>> x
    {'b': 2}

### popitem()

字典popitem()方法作用是：随机返回并删除字典中的一对键和值（项）。为什么是随机删除呢？因为字典是无序的，没有所谓的“最后一项”或是其它顺序。在工作时如果遇到需要逐一删除项的工作，用popitem()方法效率很高。

    >>> x
    {'url': 'aaa', 'title': 'bbb'}
    >>> x.popitem()
    ('url', 'aaa')
    >>> x
    {'title': 'bbb'}
