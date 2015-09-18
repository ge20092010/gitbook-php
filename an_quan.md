过滤输入

* 
bool ctype_alnum ( string $text )
检查提供的string,text 是否全部为字母和(或)数字字符。

* 
bool ctype_alpha ( string $text )查看提供的string，text里面的所有字符是否只包含字符(字母)

* 
bool ctype_digit ( string $text )检查提供的 string 和 text 里面的字符是不是都是数字。

* 
bool ctype_lower ( string $text )检查提供的 string 和 text 里面的字符是不是都是小写字母。

* 
bool ctype_upper ( string $text )检查 string 和 text 里面的字符是不是都是大写字母。

跨站脚本

```
// 为了预防XSS,你只需要合适地从输出中转义上下文
$html = array(
    'username' => htmlentities($_POST['username'], ENT_QUOTES, 'UTF-8');
);
echo $html;
```
SQL注入

* 
不转义SQL查询中的数据就会有SQL注入漏洞。

```
$name = "a' OR 't'='t";
$query = "SELECT * FROM users WHERE name='{$name}'";
echo $query;
// SELECT * FROM users WHERE name='a' OR 't'='t'
```
* 
针对SQL注入最佳的方法是使用绑定的参数。

```
$sql = $db->prepare("SELECT count(*) FROM users WHERE
        username=:username AND password=:hash");
$sql->bindParam(":username", $clean['username'], PDO::PARAM_STRING, 32);
$sql->bindParam(":hash", $clean['hash'], PDO::PARAM_STRING, 32);
```

