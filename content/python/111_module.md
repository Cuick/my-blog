+++
date = "2016-04-13T15:07:49+08:00"
title = "python基础-模块"

tags = [ "python", "模块", "包", "PYTHONPTAH" ]
categories = [
  "python"
]

+++
<!--more-->

## 包

避免模块名冲突，Python又引入了按目录来组织模块的方法，称为包（Package）


    package1
    ├─ __init__.py
    ├── admin.py
    ├── models.py
    ├── tests.py
    └─ views.py

每一个包目录下面都会有一个__init__.py的文件，这个文件是必须存在的，否则，Python就把这个目录当成普通目录，而不是一个包。__init__.py可以是空文件，也可以有Python代码，因为__init__.py本身就是一个模块，而它的模块名就是mycompany

可以有多级目录，组成多级层次的包结构。

## 模块

    在Python中，一个.py文件就称之为一个模块（Module）。

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-

    ' a test module '

    __author__ = 'Michael Liao'

    import sys

    def test():
        args = sys.argv
        if len(args)==1:
            print 'Hello, world!'
        elif len(args)==2:
            print 'Hello, %s!' % args[1]
        else:
            print 'Too many arguments!'

    if __name__=='__main__':
        test()

当我们在命令行运行hello模块文件时，Python解释器把一个特殊变量__name__置为__main__，而如果在其他地方导入该hello模块时，if判断将失败，因此，这种if测试可以让一个模块通过命令行运行时执行一些额外的代码，最常见的就是运行测试。

## 使用模块

    import sys

导入sys模块后，我们就有了变量sys指向该模块，利用sys这个变量，就可以访问sys模块的所有功能


### 别名

    try:
        import cStringIO as StringIO
    except ImportError: # 导入失败会捕获到ImportError
        import StringIO

由于Python是动态语言，函数签名一致接口就一样，因此，无论导入哪个模块后续代码都能正常工作


## 第三方模块

### 安装

Python有两个封装了setuptools的包管理工具：easy_install和pip。

### 模块搜索路径

当我们试图加载一个模块时，Python会在指定的路径下搜索对应的.py文件，如果找不到，就会报错

Python解释器会搜索当前目录、所有已安装的内置模块和第三方模块，搜索路径存放在sys模块的path变量中

### 添加自己的搜索目录

* 方法一：直接修改sys.path，添加要搜索的目录

    >>> import sys
    >>> sys.path.append('/Users/michael/my_py_scripts')

* 方法二：设置环境变量PYTHONPATH，该环境变量的内容会被自动添加到模块搜索路径中


### future

Python提供了__future__模块，把下一个新版本的特性导入到当前版本，于是我们就可以在当前版本中测试一些新版本的特性。

果你想在Python 2.7的代码中直接使用Python 3.x的除法，可以通过__future__模块的division实现：

    from __future__ import division

    print '10 / 3 =', 10 / 3
    print '10.0 / 3 =', 10.0 / 3
    print '10 // 3 =', 10 // 3

结果如下：

    10 / 3 = 3.33333333333
    10.0 / 3 = 3.33333333333
    10 // 3 = 3
