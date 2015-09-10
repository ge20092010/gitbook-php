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
$dt = new DateTime("2015-09-10 19:00:10", $dtz);
var_dump($dt->format("Y-m-d h:i"));
```