确定平台

* 
PHP定义了常量PHP_OS,包含了PHP解析器所执行的操作系统名字。

* 
PHP_OS的可能值包括HP-UX、Darwin(Mac OS)、Linux、SunOS、WIN32和WINNT。

* 
内建函数php_uname(),可以返回更多的操作系统信息。

服务器环境

* 
超级全局常量数组$_SERVER提供了服务器和执行环境的信息。

行尾处理

* 
Windows中的文本文件行是以"\r\n"结束的,UNIX中的文本文件是以"\n"结束的。

```
echo PHP_EOL;
//windows平台相当于    echo "\r\n";
//unix\linux平台相当于    echo "\n";
//mac平台相当于    echo "\r";
``` 

