[20150910]

* 总共有4个处理日期和时间的类

* DateTime类处理日期和时间本身

* DateTimeZone类处理时区

* DateTimeInterval类处理两个DateTime实例间的时间跨度

* DatePeriod类处理日期和时间特定间隔的遍历。

* 获取全部时区

```
DateTimeZone::listIdentifiers();

timezone_identifiers_list();

```
```
// 从服务器选择时区并把它放进DateTimeZone类
$tz = ini_get('date.timezone');
$dtz = new DateTimeZone($tz ? $tz : "Asia/Shanghai");
// 需要从服务器获取日期和时间,第一个参数为now
$dt = new DateTime("2015-09-10 19:00:10", $dtz);
var_dump($dt->format("Y-m-d h:i"));
```
```
// DateTime的diff()方法返回两个日期的差异
$tz = ini_get('date.timezone');
$dtz = new DateTimeZone($tz ? $tz : 'Asia/Shanghai');
$past = new DateTime("2009-02-12 16:42:33", $dtz);
$current =  new DateTime("now", $dtz);
// 创新新的DateInterval实例
$diff = $past->diff($current);
$pastString = $past->format("Y-m-d");
$currentString = $current->format("Y-m-d");
$diffString = $diff->format("%yy %mm, %dd");
echo "{$pastString} 和 {$currentString} 相差 {$diffString}";
// 2009-02-12 和 2015-09-11 相差 6y 6m, 29d
```
* DateInterval格式化控制字符

| 字符 | 描述 |
| -- | -- |
| a | 天,如23 |
| d | 天,不包括前导0 |
| D | 天,10之内包括前导0；例如02和125 |
| h | 小时 |
| H | 小时,包括前导0;例如12和04 |
| 0:7 | 1:7 |
| 0:8 | 1:8 |
| 0:9 | 1:9 |
| 0:10 | 1:10 |
| 0:11 | 1:11 |
| 0:12 | 1:12 |
| 0:13 | 1:13 |
| 0:14 | 1:14 |
| 0:15 | 1:15 |
| 0:16 | 1:16 |






