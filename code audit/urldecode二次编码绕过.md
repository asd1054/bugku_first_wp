# urldecode二次编码绕过



> ## urldecode二次编码绕过
>
> ### 50
>
> 
>
> <http://123.206.87.240:9009/10.php>
>
> <?php
> if(eregi("hackerDJ",$_GET[id])) {
> echo("
>
> not allowed!
>
> ");
>
> exit();
>
> }
>
> $_GET[id] = urldecode($_GET[id]);
>
> if($_GET[id] == "hackerDJ")
>
> {
>
> echo "
>
> Access granted!
>
> ";
>
> echo "
>
> flag
>
> ";
>
> }
>
> ?>



## 1.php代码审计

代码审计得需要传入一个 `hackerDJ` 

但是又不能直接传需要简单编码一下绕过eregi函数

查表得 %44 = D

构造 `hacker%44J`过不了

于是把%也重新构造一下

相当于2次编码 得 `hacker%2544J`

得到

> Access granted!
>
> flag{bugku__daimasj-1t2}



参考 [eregi()](https://wiki.jikexueyuan.com/project/php/regular-expression/eregi.html)

> eregi()函数在一个字符串搜索指定的模式的字符串。搜索不区分大小写。Eregi()可以特别有用的检查有效性字符串,如密码。　
>
> 可选的输入参数规则包含一个数组的所有匹配表达式,他们被正则表达式的括号分组。
>
> 返回值
>
> 如果匹配成功返回true,否则,则返回false

参考 [html url编码](http://www.w3school.com.cn/tags/html_ref_urlencode.html)

> URL 编码形式表示的 ASCII 字符（十六进制格式）。
>
> 十六进制格式用于在浏览器和插件中显示非标准的字母和字符。