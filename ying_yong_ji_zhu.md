输出缓冲
* 
用PHP的输出缓冲函数来收集正常发送到浏览器的信息到缓冲区,可以延迟发送(或清理彻底)

* 使用ob_start()函数打开输出缓冲ob_start([callback])

* 当调用 callback 时，它将收到输出缓冲区的内容作为参数并预期返回一个新的输出缓冲区作为结果，这个新返回的输出缓冲区内容将被送到浏览器。

* 当输出缓冲开启后,所有的输出将被存储进内部的缓冲区。要获取当前缓冲区的长度和内容,用ob_get_length()和ob_get_contents()。

* 
两种方式抛弃缓冲区中的数据。ob_clean()函数可清理输出缓冲区但是不关闭后面的输出缓冲。ob_end_clean()函数清理输出缓冲区并且结束输出缓冲。

错误报告

* 
可以使用按位运算符来组合这些值或者屏蔽某些类型的错误。请注意，在 php.ini 之中，只有'|', '~', '!', '^' 和 '&' 会正确解析。

* 
$a & $b	And（按位与）	将把 $a 和 $b 中都为 1 的位设为 1。
* 
$a | $b	Or（按位或）	将把 $a 和 $b 中任何一个为 1 的位设为 1。

* 
$a ^ $b	Xor（按位异或）	将把 $a 和 $b 中一个为 1 另一个为 0 的位设为 1。
* 
~ $a	Not（按位取反）	将 $a 中为 0 的位设为 1，反之亦然。

触发错误

* 
可以在脚本中用trigger_error()函数抛出一个错误。

* 
trigger_error(message [, type]);

* 
第一个参数是错误信息,第二个(可选)参数表示等级E_USER_ERROR、E_USER_WARNING或E_USER_NOTICE(默认)中的一个。

```
function divider($a, $b){
    if($b == 0){
        trigger_error('$b cannot be 0', E_USER_ERROR);
    }
    return ($a/$b);
}

echo divider(200, 3);
echo divider(10,0);
// 66.666666666667
// Fatal error: $b cannot be 0 in /Users/gehuanyun/a.php on line 5
```
错误处理器中的日志

```
// 日志分流错误处理器
function log_roller($error, $errorString){
    $file = '/tmp/php_errors.log';
    if(!file_exists($file)){
        touch($file);
    }
    // 3表示附加错误到文件
    error_log($errorString, 3, $file);
    // 清除文件状态缓存
    // 函数缓存特定文件名的信息
    // 因此只在对同一个文件名进行多次操作并且需要该文件信息不被缓存时才需要调用
    clearstatcache();
    if(filesize($file) > 1024){
        rename($file, $file.(string)time());
    }
}

set_error_handler('log_roller');

for($i=0; $i<50000; $i++){
    trigger_error(time().": Just an error, ma'am.\n");
}

echo 5/0; // 执行log_roller,直接写入日志

restore_error_handler();// 还原之前的错误处理函数

echo 5/0; // Warning: Division by zero in /Users/gehuanyun/a.php on line 26 
```
性能调优

* 
一旦你的代码可以工作,你应该找出其中需要优化的。

* 
优化代码的目标通常为缩短运行时间和减少内存占用。

* 
优化之前,问自己哪里需要优化。

* 
只有在页面花费长时间加载并且用户感受到它慢的时候,优化才是必需的。

优化内存占用

* 
当处理完一个大字符串,把保存字符串的变量设置为空,这样释放内存以便重用。

