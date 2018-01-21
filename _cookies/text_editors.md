---
layout: page
title: tools
---

---
## mac tools
### keyboard shotcuts
  * open terminal `command + T`
  * switching between terminals `control + Tab`
  * switching between applications `command + Tab`
  
---
## learning list
* C++ 
 
  http://www.learncpp.com/

* tensorflow slim/sonnet

---

## latex
* latex for ubuntu [https://help.ubuntu.com/community/LaTeX][latex-ubuntu]
* markdown latex

  [MathJax basic tutorial and quick reference][mathjax]

* Mathjax与LaTex公式简介 [url][mathjax-formular]

* `Hello world!`
  1. 使用文本编辑器将如下内容写入文件 *latex_test.tex* 中
    ```
      \documentclass{article}
      \begin{document}
        Hello world!
      \end{document}
    ```
  2. Linux系统下使用命令 `latex latex_test.tex` 将会得到 *latex_test.dvi* 文件；
    
      可以通过命令 `xdvi latex_test.dvi` 查看该文件中的内容。

  3. 使用命令 `dvipdf latex_test.dvi` 生成 **latex_test.pdf** 文件。


[latex-ubuntu]: https://help.ubuntu.com/community/LaTeX
[mathjax]: http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference
[mathjax-formular]: http://mlworks.cn/posts/introduction-to-mathjax-and-latex-expression/

---

## Atom
* [Atom Flight Manual][atom-flight-manual]
* [Getting Started][getting-started]
* shortcut keys
  * run python script
  `ctrl+shift+b`
  * delete line, duplicate line
  `ctrl+shift+k`, `ctrl+shift+d`
  * move begining/end of line
  `shift+HOME`, `shift+END`
  * select lines
  `shift+HOME`, `shift+END`
  `shift+up`, `shift+down`
  * open a file/directory
  `ctrl+o`, `ctrl+shift+o`

[atom-flight-manual]: http://flight-manual.atom.io/
[getting-started]: http://flight-manual.atom.io/getting-started/sections/why-atom/

---

## Vim
* mac vim+tmux copy & paste
    first, my vim is the system vim, and the following 2 steps will allow you to copy & pasta between vim
    step1: `brew install reattach-to-user-namespace`
    step2: paste the following lines to `~/.tmux.conf` (if do not have, create one)
        ```
        ```
    
* Vim YouCompleteMe

  [https://github.com/Valloric/YouCompleteMe][youcompleteme]
* vim colorscheme

  [http://cocopon.me/app/vim-color-gallery/][vim-colorscheme]
* 一个可用的 vim 配色方案

  [https://github.com/altercation/vim-colors-solarized][vim-colorscheme-2]
* differences between vim-gnome & vim-gtk

  [askubuntu][askubuntu]


* Install vim from github
 ![vim-install-done](http://obmpvqs90.bkt.clouddn.com/vim-installation-done.png)

* vim 跨终端复制粘贴

  `vim --version` (查看是否有`+xterm_clipboard`, 如果没有则不可以运用系统剪切板进行跨终端复制粘贴)

  `sudo apt-get install vim-gtk`

  `vim --version` （此时出现`+xterm_clipboard`，必须适用vim 而不是vi进行文本编辑)

  `vim paste`

  [url-1](http://linux.cn/article-2751-1.html)
  [url-2](http://www.cnblogs.com/jianyungsun/archive/2011/03/19/1988855.html)
  [url-3](http://linux.vbird.org/linux_basic/0310vi.php#vim_ws)

* [vim 相对行号](http://jeffkreeftmeijer.com/2012/relative-line-numbers-in-vim-for-super-fast-movement/)

  [vim 配置博客](http://blog.csdn.net/wklken/article/details/9076621)



[vim-colorscheme]: http://cocopon.me/app/vim-color-gallery/
[vim-colorscheme-2]: https://github.com/altercation/vim-colors-solarized
[youcompleteme]: https://github.com/Valloric/YouCompleteMe
[askubuntu]: http://askubuntu.com/questions/281886/what-are-the-differences-between-the-different-vim-packages-available-in-ubuntu
