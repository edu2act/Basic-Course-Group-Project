# 1 构建Spider Money  
使用这些指令构建最新的SpiderMonkey源代码。  
在开始之前，请确保为您的计算机准备了正确的构建工具:Linux、Windows、Mac等。当构建大于28的版本时，您还需要[NSPR](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/NSPR)。  
当然，您还需要获得[SpiderMonkey源代码](./003\ 获取SpiderMonkey的源代码.md)。  
##1.1 非开发人员的(最佳)构建  
如果您想安装SpiderMonkey以供生产使用或运行性能基准测试，请使用以下步骤。(如果您想在c++应用程序中使用SpiderMonkey作为库，或者改进SpiderMonkey本身，请执行开发人员/调试构建，如下所述)。  
```shell
cd js/src
autoconf-2.13

# This name should end with "_OPT.OBJ" to make the version control system ignore it.
mkdir build_OPT.OBJ
cd build_OPT.OBJ
../configure
# Use "mozmake" on Windows
make
```
关于这一点有几点需要注意:  
* 最常见的构建问题是依赖关系问题。请参阅[平台的构建先决条件页面](https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Build_Instructions#Getting_started)。  
* SpiderMonkey不支持在源目录中构建。您必须在一个单独的构建目录中配置和构建，如上所示。  
* 是的，autoconf 2.13版本确实是必需的。以后的版本将无法工作。(但是，不要将其安装为您的系统autoconf。这也行不通，这是个坏主意，因为那个版本太旧了。)  
**注意：**如果你在Mac上，得到一个类似的错误  
>"checking whether the C compiler (gcc-4.2  ) works... no
configure: error: installation or configuration problem: C compiler cannot create executables."   

您可以这样配置:
>CC=clang CXX=clang++  ../configure   

也有可能胡言乱语无法编译：
>/usr/local/Cellar/llvm/7.0.1/lib/clang/7.0.1/include/inttypes.h:30:15: fatal error: 'inttypes.h' file not found                                                                                             
>/usr/local/Cellar/llvm/7.0.1/lib/clang/7.0.1/include/inttypes.h:30:15: fatal error: 'inttypes.h' file not found, err: true  

这是因为，从Mohave开始，头文件不再安装在/usr/include中。参考命令行工具下的发布说明——>新特性.  
发布说明还指出，在不久的将来，这个兼容性包将不再提供，因此必须对macOS上的构建系统进行调整，以便在SDK中查找头文件  
在此之前，以下几点应该会有所帮助，  
>open /Library/Developer/CommandLineTools/Packages/macOS_SDK_headers_for_macOS_10.14.pk  


这将在build-release/dist/bin目录中构建一个名为js的可执行文件。您可以使用dist/bin/js——help来测试它，它会显示一个帮助页面。现在，您已经准备好运行并尝试shell。  
在Mac、Linux或UNIX上，您可以使用附加命令make install在系统上安装SpiderMonkey。这会将共享库安装到/usr/local/lib，将C头文件安装到/usr/local/include，将js可执行文件安装到/usr/local/bin。  
## 1.2 开发人员(调试)构建  
对于开发和调试SpiderMonkey本身，最好将调试构建(用于日常调试)和优化构建(用于性能测试)放在单独的构建目录中。因此，除了遵循上面的步骤，您还应该使用以下步骤创建调试构建:  
```shell
cd js/src
autoconf-2.13

# This name should end with "_DBG.OBJ" to make the version control system ignore it.
mkdir build_DBG.OBJ
cd build_DBG.OBJ
../configure --enable-debug --disable-optimize
# Use "mozmake" on Windows
make
```
您还可以使用js\_gc\_选项构建SpiderMonkey的调试构建，该选项向SpiderMonkey添加了一个新的内置函数，允许您配置积极主动的垃圾收集。这可以帮助调试内存泄漏和其他与内存相关的问题。有关详细信息，请参见[js_setgc()](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/SpiderMonkey/JSAPI_reference/JS_SetGCZeal)。  
对于其他可用的构建选项列表，键入(假设当前工作目录是上面创建的构建目录之一):
```shell
../configure --help
```
### 1.2.1 生成编译数据库  
有些工具(如IDEs、静态分析程序和重构工具)使用名为compile_commands.json的文件包含构建软件所需的所有部分的描述，这样工具就不必理解构建系统。  
生成一个compile_commands.json需要使用SpiderMonkey配置脚本，启用CompileDB后端，如下所示:  
```shell
../configure <options> --enable-build-backends=CompileDB,RecursiveMake
```
(RecursiveMake就在那里，您可能也希望能够构建它!)   
## 1.3 Windows系统构建  
**注意：**自第28版以来，threadsafe构建是默认的，应该可以在所有POSIX平台上脱离使用。因此，只有在Windows上或编译旧版本的SpiderMonkey时，下面的说明才应该是相关的。  
用于打开shell的MozillaBuild批处理文件(例如start-shell-msvc2013.bat或start-shell-msvc2013-x64.bat)确定编译器工具链将针对32位或64位构建。要创建64位构建，请注意必须使用——target=x86_64-pc-mingw32——host=x86_64-pc-mingw32进行配置。  
由于POSIX NSPR模拟对Windows不可用，所以您的构建必须有一个可用的NSPR工作版本。最简单的选项是配置——enable- nsprl -build。这个配置选项构建NSPR的树内版本，这可能是您想要的;因为SpiderMonkey使用较新的NSPR符号，所以操作系统附带的NSPR可能无法工作。  
如果--enable- nsprl -build不起作用，使用--with- nsprl -cflags和--with- nsprl -libs配置选项显式地告诉configure在哪里找到NSPR。例如，假设您的本地NSPR已经安装到C:/mozilla-build/msys/local:  
```shell
./configure --with-nspr-cflags="-IC:/mozilla-build/msys/local/include" \
            --with-nspr-libs="C:/mozilla-build/msys/local/lib/libnspr4.a \
                              C:/mozilla-build/msys/local/lib/libplds4.a \
                              C:/mozilla-build/msys/local/lib/libplc4.a"
```
如果你得到符号加载或动态库错误，你可以强制正确的NSPR加载:  
```shell
PATH="$PATH;C:/mozilla-build/msys/local/lib/" ./js
```
# 2 直接安装具体说明  
默认情况下，make install将文件放在以下目录中。您可以通过将选项传递给configure脚本来覆盖它:  
| 名字 |位置 |配置选项 |
|:-|:-|:-|
|可执行文件,shell脚本|/usr/local/bin|--bindir|
|库、数据|/usr/local/lib|--libdir|
|与体系结构无关的数据|/usr/local/share|--sharedir|
|C头文件|/usr/local/include|--includedir|
为了方便起见，您可以向configure脚本传递一个表单的选项--prefix=\<PREFIXDIR\>，它在上面的所有设置中用\<PREFIXDIR\>替换/usr/local，只需一步。这通常是最不麻烦的事情，因为它保留了lib、bin等的典型安排。       

**注意：**传递给configure的所有目录都记录在生成的makefile中，因此在重新运行configure之前不需要再次指定它们。    
# 3 将SpiderMonkey构建为一个静态库  
默认情况下，SpiderMonkey构建为一个共享库。但是，您可以通过在运行configure时指定--disable-share -js标志，将SpiderMonkey构建为一个静态库。  
## 3.1 指定编译器和编译器标志  
如果希望使用configure脚本默认为您选择的编译器之外的编译器，可以在运行configure时在环境中设置CXX变量。这将保存您在生成的makefile中指定的值，因此，一旦您设置了它，在重新运行configure之前，您不需要再次这样做。  
如果希望将某些标志传递给编译器，可以在运行configure时设置CXXFLAGS环境变量。例如，如果您正在使用GNU工具链，下面的代码将把-g3标志传递给编译器，使它发出有关宏的调试信息。然后你可以在gdb命令中使用这些宏:  
```shell
$ CXXFLAGS=-g3 $SRC/configure
...
checking whether the C++ compiler (c++ -g3 ) works... yes
...
$
```
# 4 交叉编译选项  
对于交叉编译，您将需要一个交叉编译编译器。由于clang内置了交叉编译支持，所以使用clang更容易。不过，您可能需要其他库。例如，在debian linux上，您将需要以下代码从x86_64交叉编译到x86。  
```shell
apt install clang libstdc++-8-dev-i386-cross binutils-i686-gnu zlib1g-dev:i386
```  
你还需要锈病，除了正常锈病设置，你需要添加另一个目标到你现有的锈病工具链(不要添加一个新的工具链spidermonkey将只使用一个工具链，并使用它的主机和目标代码:  
```shell
rustup target add i686-unknown-linux-gnu
```  
要在64位Linux系统上构建32位版本，可以使用以下命令:  
```shell
PKG_CONFIG_LIBDIR=/usr/lib/pkgconfig CC="gcc -m32 -mfpmath=sse -msse -msse2" CXX="g++ -m32 -mfpmath=sse -msse -msse2" AR=ar \ 
$SRC/configure --target=i686-pc-linux
```  
或 clang.
```shell
$SRC/configure --target=i686-pc-linux-gnu
```  
要在64位Linux系统上构建运行在arm模拟器中的32位arm版本，可以使用以下工具:  
```shell
AR=ar CC="gcc -m32 -mfpmath=sse -msse -msse2" CXX="g++ -m32 -mfpmath=sse -msse -msse2" \
    $SRC/configure --target=i686-pc-linux --enable-simulator=arm
```  
要在64位Mac系统上构建32位版本(目标版本是特定于OS/X SDK的)，可以使用以下工具:  
```shell
$SRC/configure --target=i386-apple-darwin16.7.0 # Choose the appropriate SDK version for your version of OS/X
```   
要在32位Mac系统(例如Mac OS X 10.5)上构建64位版本，可以使用以下命令:  
```shell
AR=ar CC="gcc -m64" CXX="g++ -m64" ../configure --target=x86_64-apple-darwin10.0.0
```    
要构建64位Windows版本，可以使用以下工具:  
```shell
$SRC/configure --host=x86_64-pc-mingw32 --target=x86_64-pc-mingw32
```   
**注意：**您必须使用正确的-x64.bat脚本启动MozillaBuild shell，以便64位编译器位于您的路径中。  
无论传递给configure的编译器和标志是什么，都会记录在生成的makefile中，因此在重新运行configure之前，不需要再次指定它们。  
# 5 构建您的应用程序  




