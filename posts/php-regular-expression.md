# PHP 正则表达式匹配页面链接

```php
$html = '<a href=\'/1\'></a><a href=\'/2\'></a>';
$preg = "/<a .*?href='(.*?)'.*?>/ism";
preg_match_all($preg, $html, $matches);
var_dump($matches);
```
