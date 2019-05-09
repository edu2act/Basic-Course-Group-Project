# 获取SpiderMonkey源代码  
> 您可以以gzip格式或直接从Mercurial存储库获得SpiderMonkey源代码。   

##1.1 下载gzip压缩的SpiderMonkey源代码  
你可以从以下网址下载gzip压缩的SpiderMonkey源代码:  
> http://ftp.mozilla.org/pub/spidermonkey/releases/  
> http://ftp.mozilla.org/pub/spidermonkey/prereleases/  

下面是一个命令行例子，下载并解压缩SpiderMonkey源代码版本59.0:
```shell
mkdir mozilla
cd mozilla
wget http://ftp.mozilla.org/pub/spidermonkey/prereleases/59/pre1/mozjs-59.0a1.0.tar.bz2
tar xvf mozjs-59.0a1.0.tar.bz2
```
只要在Windows上使用[MozillaBuild bash shell](https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Build_Instructions/Windows_Prerequisites#mozillabuild)，这些命令应该可以在包括Windows在内的大多数平台上工作。  
## 1.2 从MercurialEdit获取最新的SpiderMonkey源代码  
[Mercurial](https://developer.mozilla.org/en-US/docs/Mozilla/Mercurial)存储库(https://hg.mozilla.org/mozilla-central/)承载最新的SpiderMonkey源代码。Mercurial也被称为hg。  
下面的命令行下载了整个Mozilla存储库，包括完整的更改历史记录，以及许多不属于SpiderMonkey的Gecko和Firefox源代码。它还将更改到SpiderMonkey目录(js/src)。  
```shell
hg clone https://hg.mozilla.org/mozilla-central/
cd js/src
```
要避免获得完整的更改历史记录，请单击zip或gz链接(https://hg.mozilla.org/index.cgi/mozilla-central/file/tip) 。这将获取当前Mozilla树的快照。  
如果您对上面的说明有问题，可以在[这里](https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Source_Code/Mercurial)阅读使用Mercurial获取Mozilla代码的详细信息。该页面还包含到几个bundle的链接，如果网络连接不好，这些链接可能很有用。   
## 1.3 从Git获得最新的SpiderMonkey源代码  
下面的命令行下载了整个Mozilla存储库，包括完整的更改历史记录，以及许多不属于SpiderMonkey的Gecko和Firefox源代码。它还会更改到SpiderMonkey目录(js/src)。  
```shell
git clone https://github.com/mozilla/gecko-dev.git
cd gecko-dev/js/src
```
如果您想要更快的下载速度(到2015年1月为止大约是下载速度的5倍)，可以尝试进行浅克隆(没有版本控制历史记录)。  
```shell
git clone --depth 1 https://github.com/mozilla/gecko-dev.git
```
如果您有任何问题，请检查(https://wiki.mozilla.org/Github)页面。    
## 1.4 从CVS获取老版本SpiderMonkey源代码  
**注意：**即使当前正在构建另一个Mozilla项目，也需要显式地获取JavaScript shell源代码，因为有些特定于shell的文件通常不会在Mozilla源代码树中找到。  
与从CVS获取任何其他Mozilla项目一样，您需要首先登录CVS服务器。为此，将cd进入您想要签入的基本目录的代码中，然后在命令行中输入以下命令:  
```shell
cvs -d :pserver:anonymous@cvs-mirror.mozilla.org:/cvsroot login
```
当提示时，输入密码anonymous。  
登录后，cd进入CVS树的根目录，并输入以下命令:
```shell
cvs -d :pserver:anonymous@cvs-mirror.mozilla.org:/cvsroot co -l mozilla/js/src mozilla/js/src/config mozilla/js/src/editline mozilla/js/src/fdlibm
```
这将检出构建JavaScript shell所需的所有文件。  
如果您还需要回归测试，请添加以下命令:  
```shell
cvs -d :pserver:anonymous@cvs-mirror.mozilla.org:/cvsroot co mozilla/js/tests
```
## 1.5 获取老版本SpiderMonkey分支源代码  
如果你想尝试一个特定分支的SpiderMonkey版本，你需要从分支中检出js/src，但要从主干中检出editline和config:  
```shell
cvs -d :pserver:anonymous@cvs-mirror.mozilla.org:/cvsroot co -l -r BRANCH_NAME mozilla/js/src mozilla/js/src/fdlibm
cvs -d :pserver:anonymous@cvs-mirror.mozilla.org:/cvsroot co -l mozilla/js/src/config mozilla/js/src/editline
```
将BRANCH_NAME更改为要签出的分支的名称。您可以使用JavaScript分支名称(例如JS_1_7_ALPHA_BRANCH)或Mozilla分支名称(例如MOZILLA_1_8_BRANCH)。  


