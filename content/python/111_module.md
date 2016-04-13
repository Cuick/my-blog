+++
date = "2016-04-10T15:07:49+08:00"
title = "python基础-模块"

tags = [ "python" ]
categories = [
  "python"
]

+++
<!--more-->

## 模块

在Python中，一个.py文件就称之为一个模块（Module）。

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
