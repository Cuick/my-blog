+++
date = "2016-03-19T20:24:49+08:00"
title = "闭包"

tags = [ "python", "闭包","编程语言"]
categories = [
  "python"
]

+++
<!--more-->

闭包

    def make_addr(addend):
        def addr(augend):
            return augend + addend
        return addr

    p = make_addr(23)
    q = make_addr(42)

    print p(10)
    print q(10)
