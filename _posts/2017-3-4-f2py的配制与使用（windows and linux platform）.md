---
layout: post
title: f2py的配制与使用（windows and linux platform）
published: true
---

_f2py(Fortran to Python)_，顾名思义，**_f2py_**是作为一个『连接』`Fortran`与`Python`这两种语言的工具而存在的。[Fortran](https://www.fortran.com/)是数值计算领域常用的偏底层语言，其运行速度之快，满足了大量数值模拟过程中度计算速度的要求；而[Python](https://www.python.org/)作为一个现代的面向对象的高级语言，有着简洁优美的语法，并且是扩展性最好的语言之一。**_f2py_**的存在正是为底层语言和高级语言建立了一个桥梁，让我们在继承两种语言的优点的同时，方便了对程序的调试和扩展。

> 更详细的关于f2py的介绍可以参考其官网[f2py2e](https://sysbio.ioc.ee/projects/f2py2e/)，里面有更详细的说明和背景介绍以及简单地使用方法。

下面分别介绍**_f2py_**在windows和linux平台下的安装和使用。



### Linux下的安装和使用

Linux平台下的安装是十分简单地，基本上按照[f2py安装过程](https://sysbio.ioc.ee/projects/f2py2e/#download)就可以完成。当然Python的[Numpy](http://www.numpy.org/)包中已经包含了**f2py**包，所以，以下都是通过直接安装**Numpy**来实现对**f2py**的安装和使用。

#### 1.  **Numpy**的安装

Linux下，**Numpy**的安装十分简单，只需要在终端执行以下命令：

```
pip install numpy
```

即可安装**Numpy**包。这里是通过[pip](https://pypi.python.org/pypi/pip)这个工具安装的。

> **Note:**若系统中存在两个版本的Python，请执行
>
>  ```
>  pip2 install numpy ###for python2.x
>  ```
>
> 或者
>```
> pip3 install numpy ###for python3.x
>```
>

#### 2.  **编译器**的安装

 一般来说，需要fortran和c的编译器，Linux平台下，一般预装了[gcc](https://gcc.gnu.org/)，我们可以通过命令：

`gcc`

来测试gcc是否已经被安装；若出现如图的信息，则说明gcc已经被成功安装。
![enter image description here](http://www.hedilict.com/images/2017-03-02-测试gcc.png)

否则，则执行命令：

    sudo apt-get install gcc

安装gcc。

同样的，执行命令

    gfortran

若出现以下信息，则说明gfortran也被成功安装。

![](http://www.hedilict.com/images/2017-03-02-测试gfortran.png)
> **Note:** **gfortran**是**gcc**的一部分，详情可参考[gcc/gfortran](https://gcc.gnu.org/fortran/)


#### 3. f2py的执行与测试

一般来说，经过以上两步后，f2py已经安装成功。可以执行以下命令查看f2py的所在路径以及是否是可执行状态：
```
    //查看f2py所在的路径
    whereis f2py
    //执行
    f2py
 ```
 
![enter image description here](https://lh3.googleusercontent.com/-ngDJpC9NTFc/WLgemdSstSI/AAAAAAAAAKU/lIkDQiK6KogUdfGuY5S4t_-O_Lr1z3V7ACLcB/s0/2017-03-02+21-15-01%25E5%25B1%258F%25E5%25B9%2595%25E6%2588%25AA%25E5%259B%25BE.png "2017-03-02 21-15-01屏幕截图.png")

如果出现上图所示情况，则f2py已经安装成功！

接着，我们开始测试一个Demo：

- 创建一个命名为`hello.f90`的Fortran文件。

![enter image description here](https://lh3.googleusercontent.com/-E8TzqyEfR88/WLgfv1BVp0I/AAAAAAAAAKg/9qu08a1wTdEjeX75ZLWVFPjByT5gAJXbwCLcB/s0/2017-03-02+21-34-42%25E5%25B1%258F%25E5%25B9%2595%25E6%2588%25AA%25E5%259B%25BE.png "2017-03-02 21-34-42屏幕截图.png")

- 进入到该文件所在的文件夹，并执行以下命令：

![enter image description here](https://lh3.googleusercontent.com/-AHUZttcTioo/WLghGjBdy-I/AAAAAAAAALA/EC9ytYQzwnQX3zK_Z17z_tV9efg8C_LXgCLcB/s0/2017-03-02+21-38-16%25E5%25B1%258F%25E5%25B9%2595%25E6%2588%25AA%25E5%259B%25BE.png "2017-03-02 21-38-16屏幕截图.png")

可以看到，编译成功！可以在Fortran源文件`hello.f90`所在的文件夹内找到生成的Python模块**hello**。

- 调用该模块**hello**

进入Python，Import该模块，执行以下命令：

![enter image description here](http://www.hedilict.com/images/2017-03-02-测试结果.png)

可以看到，模块**hello**已经调用成功，输出了`hello world`字符串。
至此，f2py在Linux（测试发行版为[Ubuntu](https://www.ubuntu.com/)）安装成功！

### Windows下的安装和使用

> Windows下f2py的安装要比Linux上复杂的多，只要是涉及到编译器上的选择以及这其中存在的版本差异导致的冲突。

####  1. Python与f2py的下载安装

笔者的环境为：

- windows10，64bit

这里以Python2.7版本为例：

- 下载Python2.7：[Python2.7](http://www.python.org/getit/)
- 下载numpy：[numpy](http://www.lfd.uci.edu/~gohlke/pythonlibs/#numpy)
 >**Note:**请选择与操作系统对应bit（32 or 64）的Python和numpy

 numpy下载下来的文件为`.whl`（[wheel](http://pythonwheels.com/)）文件，需要使用**pip**来进行安装。
 安装之前，需要将`Path\Python27`和`Path\Python27\Scripts`添加进windows环境变量。

打开**cmd**或者**PowerShell**，进入到numpy的`.whl`文件所在的目录，执行以下命令：
```
    pip install numpy_xxx.whl
```
如果出现以下错误：
```
    Fatal error in launcher: Unable to create process using '"'
```
则执行：
```
    python -m pip install numpy_xxx.whl
```

> 以上错误解决参考：[http://stackoverflow.com/questions/24627525/fatal-error-in-launcher-unable-to-create-process-using-c-program-files-x86](http://stackoverflow.com/questions/24627525/fatal-error-in-launcher-unable-to-create-process-using-c-program-files-x86)

通过以上步骤便可以成功安装numpy。测试f2py是否成功安装，执行命令：

    python Path\Python27\Scripts\f2py.py

若出现如下提示，则安装成功。

![enter image description here](https://lh3.googleusercontent.com/-lgNlvnN08wM/WLgqmPqAXQI/AAAAAAAAAL8/Sz1_iquxxo0NGHywENClsAw7UUtDzYruQCLcB/s0/YE%2529%255DWM%2524F0H%255DY%255BCR%2560IOU%2528RK1.png "YE&#41;]WM$F0H]Y[CR`IOU&#40;RK1.png")

 

#### 2. **编译器**的安装
推荐使用[mingw-64](http://www.mingw-w64.org/doku.php)作为windows下64bit的编译器。
下载[mingw-64 download](https://sourceforge.net/projects/mingw-w64/)，下载如图所示的压缩包，并解压到`C:\mingw`下。

![enter image description here](https://lh3.googleusercontent.com/-6cQSrXGQgzc/WLgsb6Jj8YI/AAAAAAAAAMQ/-irqlckyemIINOYJs59n3Ds5xrqQgkdAwCLcB/s0/%2560_%255D7QYDGR%25253TO6YJ%257BZ0PD%255BQ.png "`_]7QYDGR%3TO6YJ{Z0PD[Q.png")

之后，将`C:\mingw`加入环境变量中。

![enter image description here](https://lh3.googleusercontent.com/-23SQIX1nKg4/WLgs7fQfgwI/AAAAAAAAAMg/gFblVtDzBt0SZNuMwIqMn29VNiGUwd0_QCLcB/s0/0QNXB%2525%257D%2524E%2528WSX1%257DHYBC%2529%255B%255DD.png "0QNXB%}$E&#40;WSX1}HYBC&#41;[]D.png")

----------


#### 3. 编译和执行
同样的，新建一个Fortran源文件`hello.f`。

执行以下命令：

    python Path\Python27\Scripts\f2py.py -c --fcompiler=gnu95 --compiler=mingw32 -m yourmodulename yourfortranfile

如图所示：

![enter image description here](https://lh3.googleusercontent.com/-d2GwB1ad3Cc/WLguuus188I/AAAAAAAAAM8/Wx-z2em_KmMoqUp6D1-KwTlk1NBP3AbzwCLcB/s0/I3HJ6VLJ%255D%255DEUO8TTJAMZH2P.png "I3HJ6VLJ]]EUO8TTJAMZH2P.png")

执行成功后，可以在Fortran源文件所在的目录下找到f2py生成的**hello.pyd**文件。
之后，我们进入Python，重复和Linux下类似的命令：

![enter image description here](https://lh3.googleusercontent.com/-W8QxWaYn8Z8/WLgvW3OMvlI/AAAAAAAAANM/wJniHgl3asMnZtHZ5Vs0GNfilJleCkW5ACLcB/s0/V%2540%257DH%2525%255B9RNQZCIXA%2528CTM5I%25241.png "V@}H%[9RNQZCIXA&#40;CTM5I$1.png")

可以看到，执行成功！

----------

----------
以上便是f2py在Linux和windows平台下的安装使用过程。这里不建议使用msvc作为编译器，因为这里面会存在版本冲突。

----------
参考链接：

- [https://scientificcomputingco.blogspot.sg/2013/02/f2py-on-64bit-windows-python27.html](https://scientificcomputingco.blogspot.sg/2013/02/f2py-on-64bit-windows-python27.html)
- [ http://stackoverflow.com/questions/24627525/fatal-error-in-launcher-unable-to-create-process-using-c-program-files-x86]( http://stackoverflow.com/questions/24627525/fatal-error-in-launcher-unable-to-create-process-using-c-program-files-x86)
