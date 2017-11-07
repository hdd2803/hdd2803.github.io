---
layout: post
title: Sublime Text3的Markdown配置
date: 2017-11-05 
tag: WebNote
---

　　Sublime Text3是一款及其强大的软件，其特点在于丰富的插件，可以扩展各种功能，可谓“只有你想不到，没有它做不到”。通过一段时间的使用后，发现用它来编写Markdown文本，很是方便。但感觉网上的教程五花八门，没有系统性的介绍在Markdown下的配置，现把自己的配置历程，做一下总结。

### 一、MacOS下的配置

#### 1、注册Sublime Text3
点击Help→Enter License，输入找到的可用注册码，即可注册成功。
可用注册码（2017.11.05）：
```
—– BEGIN LICENSE —–
Morin
2 User License
EA7E-924018
184B9FDB 02612F57 33B15E69 BBC567F1
E20FA231 C077EA95 CC14B48B 71DD2536
E209843A 94D13692 03AC2FAA 895B688D
B8F4A0E6 FDC15964 A5573FD7 6405ED1E
6F205469 7F34C69D 3D36E475 52AF6A5B
DFD15C31 85BA64EF F95DD592 4B42C314
AC655762 C0F0F5A1 018824E4 17C56E16
AC5AA84C 034F7A53 2C9A801B 8AED239F
—— END LICENSE ——
```


#### 2、安装Package Control
1）打开Sublime Text3，按下组合键Ctrl + `，调出控制台，在控制台输入如下命令后回车：
```
import urllib2,os; pf='Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler( ))); open( os.path.join( ipp, pf), 'wb' ).write( urllib2.urlopen( 'http://sublime.wbond.net/'; +pf.replace( ' ','%20' )).read()); print( 'Please restart Sublime Text to finish installation')
```

2）安装成功后，按下组合件Shift + Command + P，即可打开Package Control。或者通过Tools→Command Palette来打开，如下图所示。
![](/images/posts/WebNote/SublimeText/1.png)


#### 3、安装Markdown Preview
1）打开Package Control，输入“PCIP”后点击回车，进入安装插件的页面。  

2）输入“Markdown Preview”后，选择此插件进行安装。


#### 4、安装Markdown Editing
1）打开Package Control，输入“PCIP”后点击回车，进入安装插件的页面。

2）输入“Markdown Editing”后，选择此插件进行安装。


#### 5、设置Markdown浏览器中查看快捷键
1）选择Sublime Text→Perferences→Key Bindings，打开如下页面。
![](/images/posts/WebNote/SublimeText/2.png)

2）在右侧的User设置中输入如下代码，设置快捷键为Command + R，当然可以随自己喜好设置。
```
[
    { "keys": ["command+r"], "command": "markdown_preview", "args": {"target": "browser", "parser":"markdown"} }
]
```


#### 6、设置浏览器自动刷新功能
1）选择Sublime Text→Perferences→Package Settings→Markdown Preview→Setting-User，打开如下页面。
![](/images/posts/WebNote/SublimeText/3.png)

2）在页面中输入如下代码。
```
{
    "enable_autoreload": true
}
```

3）打开Package Control，输入“PCIP”后点击回车，进入安装插件的页面。

4）输入“LiveReload”后，选择此插件进行安装，重启Sublime Text3。

5）在每次打开.md格式文件后，打开Package Control，先输入`LiveReload: Enable/disable plug-ins`回车，然后选择`Simple Reload with delay (400ms)`后点击回车，即可尽情的编辑Markdown文件了。每次保存文件后，就会在浏览器打开的页面中自动刷新。

6）对于一些文件需要调整到Markdown模式下编辑，则点击Sublime Text的右下角，选择MarkdownEditing→Markdown，如下图所示。
![](/images/posts/WebNote/SublimeText/4.png)

7）个人不建议使用MarkdownLivePreview来进行双面浏览显示，因为它显示的不全面，有些细节无法反映。


#### 7、设置自动保存功能（可选）
1）打开Package Control，输入“PCIP”后点击回车，进入安装插件的页面。

2）输入“Auto-save”后，选择此插件进行安装。

3）每次打开.md格式文件后，打开Package Control，输入“current file only”后点击回车，即打开了自动保存功能。

4）若需要设置保存的间隔，则选择Sublime Text→Perferences→Package Settings→Auto-save，打开Setting-Default和Setting-User，如下所示。
![](/images/posts/WebNote/SublimeText/5.png)

5）将Settin-Default中的内容复制到Setting-User，并修改如下设置：
`"auto_save_delay_in_seconds": 1`
即可设置自己的保存间隔。


#### 8、删除多余的插件（可选）
1）打开Package Control，输入“PCRP”后点击回车，进入删除插件的页面。

2）选择你不需要的插件回车，即可删除。


#### 9、关闭文件记忆功能（可选）
1）选择Sublime Text→Perferences→Settings，打开如下页面。
![](/images/posts/WebNote/SublimeText/6.png)

2）在右侧的User设置中输入如下代码，设置快捷键为Command + R，当然可以随自己喜好设置。
```
{
     "hot_exit": false,
     "remember_open_files": false
}
```


#### 10、介绍几个实用功能
1）SideBarEnhancements：侧栏右键功能增强。

2）Theme – Soda：完美的编码主题，用过的都说好。

3）GBK to UTF8：将文件编码从GBK转换成UTF8，菜单（Sublime Text）里面找。

4）ZenCoding：前端开发方面的插件。安装后可直接使用，Tab键触发，Alt+Shift+W是个代码机器。
  

### 二、Windows下的配置
Windows下的配置和MacOS下的大致相同，不同的地方就是快捷键的位置。比如：   

1）Windows下的Preferences是在导航栏，而MacOS的是在Sublime Text下。

2）设置打开浏览器的快捷键，在Windows下我喜欢设置成Ctrl + R。

3）Windows下打开Package Control的快捷键是Shift + Ctrl + P，而MacOS下是Shift + Command + P。

以上就是Markdown在MacOS及Windows下的详细配置，如有不懂之处，可以向我咨询，谢谢！

<br>
转载请注明：[Dong的博客](http://hdd2803.github.io) » [Sublime Text3的Markdown配置](http://hdd2803.github.io/2017/11/WebNote_Sublime_Text/)  


