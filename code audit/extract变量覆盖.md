# extract变量覆盖





> ## extract变量覆盖
>
> ### 50
>
> 
>
> <http://123.206.87.240:9009/1.php>
> <?php
> $flag='xxx';
>
> extract($_GET);
> if(isset($shiyan))
> {
> $content=trim(file_get_contents($flag));
> if($shiyan==$content)
> {
> echo'flag{xxx}';
> }
> else
> {
> echo'Oh.no';
> }
> }
> ?>



## 1.代码审计



> extract()函数从数组中将变量导入到当前的符号表，该函数使用数组键名作为变量名，使用数组键值作为变量值；
>
> isset()函数判断是否存在变量`$shiyan`;trim()函数移除字符串两侧的空白字符或其他预定义字符 ，这里是移除字符串两侧的空格；
>
> file_get_contents()函数将整个文件读入一个字符串；假如`$shiyan`的值等于文件的内容(`$content`)时，就打印出flag
>
> trim（）移除字符串两侧的字符（"Hello" 中的 "He" 以及 "World" 中的 "d!"）：

抱着尝试的心理 传入一个 `shiyan`

即 `http://123.206.87.240:9009/1.php?shiyan`

直接得到 `flag{bugku-dmsj-p2sm3N}`