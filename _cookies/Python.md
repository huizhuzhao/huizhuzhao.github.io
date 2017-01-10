---
layout: page
title: Python
---
---

## Anaconda

* Official website: [http://anaconda.org/][anaconda-url]

* install packages steps

  ```
  anaconda search -t conda imagemagic
  anaconda show kalefranz/imagemagick # 与在网页端搜索 imagemagick 一样
  ```

* Using conda:
[http://conda.pydata.org/docs/using/using.html][using-conda]

* 安装anaconda后需要`source ~/.bashrc`

[anaconda-url]: http://anaconda.org/
[using-conda]: http://conda.pydata.org/docs/using/using.html

* 装饰器

  ```
  class A(object): ##必须有object
    def __init__(self):
        self.name = 'john'
    @property
    def name(self):
        print 'property'
        return self._name

    @name.setter
    def name(self, name):
        print 'setter'
        self._name = name
  ```

  ```
  >>> a = A()
  setter
  property
  ```

* python 处理文件

  [os.path 模块博客](http://www.cnblogs.com/dkblog/archive/2011/03/25/1995537.html)

  [python built-in functions](python built-in
https://docs.python.org/2/library/functions.html)

  [os.path offical](https://docs.python.org/2/library/os.path.html)
  
  ```
  shutil.copy("oldfile","newfile")  ＃python 移动文件，oldfile只能是文件夹，newfile可以是文件，也可以是目标目录
  os.path.join(name1, name2)
  os.path.isdir(dir_name)
  os.listdir(directory)
  file_name.endswith(suffix, start, end)
  os.path.dirname(path) #返回文件路径
  ```

* python 简单的数据操作
  ```
  s = '123+'
  s[:s.find('+')] == '123'
  dic = {}
  dic.setdefault('a', []) # dic.get('a', []) and also set dic['a']=[] if 'a' not in dic
  print __file__
  ```
  ```
  from numpy.matlib import repmat
  repmat(x, m,n) #类似于matlab中的repmat函数
  ```

* `iterator` vs `generator`
  [blog-using iterators and generators](http://anandology.com/blog/using-iterators-and-generators/)

  `next(generator_name)`
  *# The transformation of images is not under thread lock so it can be done in parallel* 受线程保护的程序不能够并行，

* python 互相导入
  `test1.py`, `test2.py`
  两个文件可以互相导入

* [line_profiler](https://github.com/rkern/line_profiler#frequently-asked-questions)
line_profiler is a module for doing line-by-line profiling of functions. kernprof is a convenient script for running either line_profiler or the Python standard library's cProfile or profile modules, depending on what is available.

* 记忆体、递归
  `@functools.lru_cache(maxsize=None)`
  [wiki](https://en.wikipedia.org/wiki/Memoization)

* python class
  ```
  class A():
    '''
    class A description
    '''
    def __init__(self):
            pass
    x = 10
  ```
  ```    
  >>> A.__dict__
  {'x': 10, '__module__': '__main__', '__doc__': '\n\tclass A description\n\t', '__init__': <function __init__ at 0x7f5335e46488>}
  >>> A.__doc__
  '\n\tclass A description\n\t'
  ```

* [blog-super-considered-super](https://rhettinger.wordpress.com/2011/05/26/super-considered-super/) by [Deep Thoughts by Raymond Hettinger](https://rhettinger.wordpress.com/)

  super() is in the business of delegating method calls to some class in the instance’s ancestor tree
  [Things to Know About Python Super](http://www.artima.com/weblogs/viewpost.jsp?thread=236275)
  [What does super do in Python?-stackoverflow](http://stackoverflow.com/questions/222877/what-does-super-do-in-python/33469090#33469090)

* 下面两段代码在 blocks_dict 很大时的速率相差很大，后者明显优于前者

  ```
  blocks_list_1 = []
  for ref in refcode_list:
    if ref in blocks_dict.keys(): # blocks_dict a dictionary
        tmp = blokc_dict[ref]
        blocks_list_1.append(tmp)
    else:
        continue
  ```
  ```
  blocks_list_1 = []
  for ref in refcode_list:
    try:
        tmp = blokc_dict[ref]
        blocks_list_1.append(tmp)
    except Exception:
        continue
  ```

* 切换python运行版本

  `ls /usr/bin/python*`
  ![python-versions](/images/cookies/python_versions.png)

  vim ~/.bashrc
  ```
  # add this line in the file bottom
  alias python='/usr/bin/python2.7'
  . ~/.bashrc
  ```

* python 优雅的操作字典
  [https://www.linuxzen.com/python-you-ya-de-cao-zuo-zi-dian.html](https://www.linuxzen.com/python-you-ya-de-cao-zuo-zi-dian.html)

* Numpy 读.txt文件，生成矩阵
[http://hyry.dip.jp/tech/book/page/scipy/numpy_file.html](http://hyry.dip.jp/tech/book/page/scipy/numpy_file.html)


* 美团点评技术团队
  [http://tech.meituan.com/](http://tech.meituan.com/)
  [http://www.w3ctech.com/](http://www.w3ctech.com/)
