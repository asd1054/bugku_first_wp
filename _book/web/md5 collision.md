# md5 collision(NUPT_CTF)

### 



<http://123.206.87.240:9009/md5.php>



> ## md5 collision(NUPT_CTF)
>
> ### 100
>
> 
>
> <http://123.206.87.240:9009/md5.php>





```php
<?php
$md51 = md5('QNKCDZO');
$a = @$_GET['a'];
$md52 = @md5($a);
if(isset($a)){
if ($a != 'QNKCDZO' && $md51 == $md52) {
    echo "nctf{*****************}";
} else {
    echo "false!!!";
}}
else{echo "please input a";}
?>

```

bugku没有给出网站代码，Emma！！！



## 1.md5逻辑漏洞 进行md5碰撞

代码分析后，得出思路

- 本题考到了php的弱类型比较，当两个值使用== 进行比较时，只是比较变量的值，而不会去比较变量的类型，md5('QNKCDZO')的hash值为 0e830400451993494058024219903391 ，对于 0ed+ 类型的数字，==会认为该值为0，所以只需满足md5($a)的值为0ed+类型即可满足条件，并且$a != 'QNKCDZO'
- 使用在线网站[cmd5](https://www.cmd5.com/hash.aspx?s=)进行加密测试



```python
#python md5的简单使用
import hashlib   

src = 'this is a md5 test.'   
m2 = hashlib.md5() #定义一个md5对象  
m2.update(src.encoding('utf-8'))   #需要对字符串进行转码 得到一个md5的值
print (m2.hexdigest())   #打印md5的值
```



- **写python文件跑出0ed+类型的字符串** ~~（放弃）~~
- **彩虹表进行查表**  ~~（放弃）~~

```python
#-*-coding:utf8;-*-
#qpy:3
#qpy:console
# 代码耗时太长，Emma
import hashlib
240610708
1000000000
for i in range (240610000,240610710):
    tmp = str(i).encode ("utf-8")
    m1 = hashlib.md5() 	#定义一个md5对象  
    m1.update(tmp)
    pd = m1.hexdigest()
    pd_digit = pd[2:]
    if pd.startswith('0e') and pd_digit.isdigit():
        print (i)
        print(pd)
        break
'''
240610708
0e462097431906509019562988736854
'''
```

> 这里列出一些符合条件的值：
>
> var_dump(md5('240610708') == md5('QNKCDZO'));
> var_dump(md5('aabg7XSs') == md5('aabC9RqS'));
> var_dump(sha1('aaroZmOk') == sha1('aaK1STfY'));
> var_dump(sha1('aaO8zKZF') == sha1('aa3OFF9m'));
> var_dump('0010e2' == '1e3');
> var_dump('0x1234Ab' == '1193131');
> var_dump('0xABCdef' == ' 0xABCdef');

所以 构造出 a=240610708

得到[flag](http://123.206.87.240:9009/md5.php?a=240610708)

`flag{md5_collision_is_easy}`