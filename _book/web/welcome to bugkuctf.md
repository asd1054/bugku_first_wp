# welcome to bugkuctf



> ## welcome to bugkuctf
>
> ### 100
>
> 
>
> <http://123.206.87.240:8006/test1/>
> 作者：pupil



~~我一开始的时候使用的是**hackbar**并没有任何反应所以最后选择使用**burp~~**

服务器还是没反应，放弃此题

直接查看源代码

```php
you are not the number of bugku !   
  
<!--  
$user = $_GET["txt"];  
$file = $_GET["file"];  
$pass = $_GET["password"];  
  
if(isset($user)&&(file_get_contents($user,'r')==="welcome to the bugkuctf")){  
    echo "hello admin!<br>";  
    include($file); //hint.php  
}else{  
    echo "you are not admin ! ";  
}  
 -->  
```

参考文献：

* [isset](https://www.runoob.com/php/php-isset-function.html)  

  > 如果指定变量存在且不为 NULL，则返回 TRUE，否则返回 FALSE。

* [file_get_contents](http://www.w3school.com.cn/php/func_filesystem_file_get_contents.asp)

  > file_get_contents() 函数把整个文件读入一个字符串中。
  >
  > 和 [file()](http://www.w3school.com.cn/php/func_filesystem_file.asp) 一样，不同的是 file_get_contents() 把文件读入一个字符串。
  >
  > file_get_contents() 函数是用于将文件的内容读入到一个字符串中的首选方法。如果操作系统支持，还会使用内存映射技术来增强性能。

开始构造参数



