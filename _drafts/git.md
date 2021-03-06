---
published: true
layout: post
title: git常用命令的使用

git是一个强大的分布式**文本文件**的管理工具。可以记录文件改动的时间和内容等等，因此，对于团队合作开发某一个项目来说，免费又好用。值得注意的是git只能完全(充分)识别和检测文本文件的改动，不能完全识别二进制文件的改动，对于二进制文件，只能识别改动的时间和大小，不能识别其改动的内容（也没办法识别）。因此，利用git托管文件时，应尽量选择文本文件，并保持**编码一致性**（如统一为UTF-8）。下面就开始简单介绍一下git的一些常用命令。
<!--more-->

### 1. git仓库的创建、修改、提交与删除

一般来说，托管文本文件之前，要初始化一个Git仓库(Repository):
```
 mkdir gitRepository
$ cd gitRepository
$ git init   //将当前目录初始化为一个Rsponsitry，初始化前一定要进入这个目录。
```
初始化后，只需要两步基本的操作就可以实现文件的上传和提交：
- 为Reponsitry添加文件（当然也可以改动文件）
  ```
$ git add demo1.txt demo2.txt
```
- 提交（commit）所有改动：
 ```
$ git commit -m"改动注释"   //改动注释一般为这次更新的主要内容及一些改动说明
```


后续的一些常用命令要从Git的工作原理去理解比较容易些。
Git的工作原理主要是工作区和暂存区的文件传递。如图所示：
<img class="alignnone size-medium wp-image-112" src="http://blog.hedilict.com/wp-content/uploads/2016/06/0-300x153.jpg" alt="0" width="300" height="153" />
实际上，添加文件的过程(git add file.txt)就是将文件从工作区复制到暂存区的过程；而提交文件(git commit -m"")的过程则是将缓存区的文件真真正正地添加到项目树下面。以下几个命令都是基于对这一模型的理解。

 	版本回退：
```
$ git reset --hard HEAD^
```

需要说明的是，由于Git本身是C语言开发的，实际上HEAD只的就是最近一次提交(commit)后的项目(Reponsitory)的头指针，而HEAD^代表上次提交(commit)的项目(Reponsitory)的头指针，同理，HEAD^^则代表上上次，上10次则表示为HEAD~10.每个版本都有对应的版本号。
有时，当需要回退到特定的某个版本时，可以
<pre>$git log
</pre>
命令查看提交历史，以便确定要回退到哪个版本。

也可以使用
<pre>$git reflog
</pre>
查看命令历史，以便确定要回到未来的哪个版本。
这两个命令可以查看提交的版本对应的版本号，然后执行
<pre>$git reset --hard 67897   //67897为相应的版本号
</pre>
就可以回退到这个版本。</li>
 	<li>查看状态：在添加或是提交文件之前，养成查看当前Reponsitory的状态是个好习惯。只需要执行
<pre>$git status
</pre>
即可</li>
 	<li>撤销修改：
<ul>
 	<li>注意，修改文件但未添加(add)时，可以执行以下命令撤销所有修改
<pre>$git checkout --file   //file为相应的修改过的文件名
</pre>
注意：该命令只能撤回未添加(add)之前的修改。</li>
 	<li>若要撤回已经添加(add)后的修改，即恢复到添加前的状态(但是已经在工作区修改后了)，需要执行以下命令:
<pre>$git reset HEAD file  //file为相应的文件名</pre>
</li>
</ul>
</li>
 	<li>删除文件：删除文件包过本地删除和Responsitory删除，如果本地删除后想要恢复，可以直接执行与撤销修改(删除也是一种修改嘛)相同的命令
<pre>$git checkout --file
</pre>
进行恢复。当然，如果果真需要删除这个文件(从Reponsitory中删除)，那么可以执行
<pre>$git rm file  //file 为要删除的文件名
</pre>
来将文件从库中进行移除</li>
</ul>
一、git与远程服务器的关联(例如:<a href="http://github.com">github.com</a>)
<!--more-->
