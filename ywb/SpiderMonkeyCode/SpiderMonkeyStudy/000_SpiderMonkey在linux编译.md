# Spider Monkey入门（一）

参考[博客]<https://www.cnblogs.com/chenfool/p/3840625.html>     
<https://www.cnblogs.com/jingzhishen/p/3600855.html>  
[TOC]
博客说明：  

​      测试系统 Ubuntu 18.04 LTS， js 1.7.0， js 解压在/opt/js 路径下，下载路径     <http://ftp.mozilla.org/pub/js/>  

```shell
tar -zxvf js-1.7.0.tar.gz -C /opt
```

## SpiderMonkey 编译步骤
### 1 登录源码目录：
```shell
cd /opt/js/src
```
### 2 编译
```shell
make -f Makefile.ref
```
编译好之后，编译文件会在/opt/js/src/Linux_All_DBG.OBJ

其中js 是一个js 的交互式客户端

libjs.so  libjs.a 是动态库与静态库
## spider Monkey实例
```c++
#include "jsapi.h"

#include "stdlib.h"

#include "string.h"
static void usage();
int main(int argc,const char* argv[])
{

if(argc!=2){
  usage();
  exit(-1);
}
JSRuntime *runtime = NULL;
JSContext *context = NULL;
JSObject *global = NULL;
const char *script = argv[1];
printf("script is \n%s\n", script);
jsval rval;

if (
  (!(runtime = JS_NewRuntime(1024L * 1024L)))
  || (!(context = JS_NewContext(runtime, 8192)))
  || (!(global = JS_NewObject(context, NULL, NULL, NULL)))
)
return EXIT_FAILURE;

if (!JS_InitStandardClasses(context, global))
   return EXIT_FAILURE;

if (!JS_EvaluateScript(context, global, script, strlen(script), "script", 1, &rval))
   return EXIT_FAILURE;

printf("the script's result is \n%d\n",JSVAL_TO_INT(rval));

JS_DestroyContext(context);
JS_DestroyRuntime(runtime);
JS_ShutDown();
return EXIT_SUCCESS;
}
void usage()
{
   printf("example1 script_content\n");
   printf("for example:./example1 \"var a=1;b=2;a+b\"\n");
}
```

### 1 gcc 编译命令

```shell
gcc -DXP_UNIX -I/opt/js/src -o excample test.c  -L/opt/js/src/Linux_All_DBG.OBJ -ljs -lm
```

* 1. "-DXP_UNIX" 代表使用 #define XP_UNIX；  

* 2. "-I"代表包含(include)路径  

* 3. "-o" excample 代表生成目标文件的文件名是 excample.o  

* 4. "-L"代表包含链接的函数库  


### 2 测试一下
```shell
./excample "var a=1;var b=2;a+b"
```
### 3 运行结果
```ejs
script is
var a=1;var b=2;a+b
the script's result is
3
```
