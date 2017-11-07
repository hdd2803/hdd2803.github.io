---
layout: post
title: Jekyll搭建个人博客
date: 2017-11-07 
tag: WebNote
---

　　一直想有一个自己的博客，用来发表或者管理自己的文章，这几天在自己的折腾下，终于在Windows和MacOS下均搭建好了Jekyll的博客环境。搭建的过程也不是一帆风顺，尤其是在Windows系统下，所以略有所感悟，记录下来以供分享。

### 一、Windows系统下
#### 1、安装Ruby
1）去[Ruby官网](https://rubyinstaller.org/downloads/)下载适合自己系统的Ruby版本，以及对应Ruby的Development Kits。比如：[Ruby 2.3.3 (x64)](https://dl.bintray.com/oneclick/rubyinstaller/rubyinstaller-2.3.3-x64.exe)版本需要对应下载的Development Kits：[DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe](https://dl.bintray.com/oneclick/rubyinstaller/DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe)。记住一定要按照官网的要求，下载对应的两个软件。注意一下，Ruby 2.4.0及以上使用的开发套件是MSYS2 toolkit。

2）双击下载的Ruby软件进行安装，安装路径中切记不要带有空格。比如`C:\Program Files\Ruby193`就是错误的路径，而`D:\Program\Ruby23-x64`是正确路径。

3）安装完成后，双击下载的Development Kits提取文件，选择的存放路径也一定不要带有空格，否则会遇到未知错误。比如：`D:\Program\DevKit`。

4）打开命令窗口cd到Development Kits的存放路径。运行`ruby dk.rb init`，在Development Kits目录下会生产`config.yml`文件。打开此文件，在其中输入Ruby的安装路径，如：`- D:/Program/Ruby23-x64`。
![](/images/posts/WebNote/Jekyll/1.png)

5）(可选)在命令窗口输入`ruby dk.rb review`，可以查看第四步中输入的路径是否正确。

6）最后再输入`ruby dk.rb install`来增强Ruby的功能。成功后，可在路径`<RUBY_INSTALL_DIR>\lib\ruby\site_ruby`下，可以看到`devkit.rb`文件。

7）若要测试DevKit是否在Ruby环境中正确安装，可以输入如下几个命令：
```
- gem install json --platform=ruby
- ruby -rubygems -e "require 'json'; puts JSON.load('[42]').inspect"
```
如果没有报错且返回结果42，则安装成功。步骤如下图所示：
![](/images/posts/WebNote/Jekyll/2.png)

#### 2、安装Jekyll并启动
1）在命令窗口中输入如下命令来安装Jekyll：
`gem install jekyll`

2）在电脑中创建博客存放文件夹（如：`E:\StudyDocument\Blog`），cd进入此路径
```
e:
cd E:\StudyDocument\Blog
```

3）获取文件`Gemfile.lock`需要的bundler：
`gem install bundler`

4）安装bundler：
`bundle install`

5）启动jekyll：
`jekyll server`

6）若安装过程中没有报错，则启动成功。在浏览器地址栏中输入`http://127.0.0.1:4000/`，即可查看博客。

#### 3、部署到GitHub
1）在你的GitHub中创建一个和你用户名一致的仓库，如我创建的是：`hdd2803.github.io`。

2）把此仓库克隆到本地，然后把你刚才创建的Blog文件夹中全部文件复制到仓库中，然后同步到GitHub网站上去。同步方式可以选择Git命令或者GitHub Desktop客户端。

3）到GitHub网站，选择你的博客仓库，选择Setting→GitHub Page开启网站服务。

4）在浏览器地址栏输入你的`username.github.io`，即可访问你的博客。

#### 4、更换主题
1）从GitHub上下载别人jekyll主题的仓库文件，解压到本地。

2）cd到解压的文件夹。

3）输入如下命令来启动博客：
```
gem install bundler
bundle install
jekyll server
```

4）若过程中没有报错，则在浏览器地址栏中输入`http://127.0.0.1:4000/`即可查看博客。

5）切记：将博客中别人的信息替换成自己的！！
- （1）将博客文件夹`_posts/`目录下的文件全部删除。
- （2）修改` _config.yml`中的内容为自己的。
- （3）修改`about.md`和`README.md`文件的内容。

6）若出现bundler版本不相符的情况，有如下两个方法：
- （1）修改`Gemfile.lock`中对应的bundler版本。
- （2）对版本不相符的bundler，执行如下命令：
    `bundle clean —force`或者`bundle update xxx`。
![](/images/posts/WebNote/Jekyll/3.png)

### 二、MacOS系统下
　　MacOS系统下只有安装插件和Windows系统的步骤不同，即第一步不相同，从第二步到后面均一样，就不赘述了。接下来重点讲一下安装HomeBrew、Xcode、Ruby的过程。

#### 1、安装HomeBrew
1）在终端输入如下命令来安装HomeBrew：
`ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"``

2）HomeBrew的常用命令
- （1）安装工具：`brew install xxx`
- （2）查看安装的工具：`brew list —versions`
- （3）更新brew：`brew update`
- （4）搜索工具：`brew search xxx`
- （5）卸载工具：`brew uninstall xxx`
- （6）查看brew版本：`brew -v`

#### 2、安装Xcode及Xcode command line tools
1）通过App Store安装Xcode。

2）在Xcode中选择Preferences→Downloads→Components来安装Xcode command line tools。

#### 3、安装Ruby
1）在终端输入来安装Ruby：
`brew install ruby`

2）常用命令
- （1）显示ruby版本：`ruby -v`
- （2）显示ruby安装位置：`whick ruby`

3）使用brew安装ruby成功后，若输入命令`ruby -v`显示的是系统Ruby的版本，则需要在在系统目录下修改.profile文件（文件地址如：`/Users/Dong/.profile `），来切换Ruby。输入语句如下：
```
# for brew install
export PATH=/usr/local/bin:$PATH
```
仅当输入命令`whick ruby`后显示的是`/usr/local/bin/ruby`，则在末尾添加以上语句有用。

<br>
以上就是用Jekyll搭建个人博客的全过程，如有不正之处，请多多指教！

<br>
转载请注明：[Dong的博客](http://hdd2803.github.io) » [Jekyll搭建个人博客](http://hdd2803.github.io/2017/11/WebNote_Jekyll/)
