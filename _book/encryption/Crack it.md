# Crack it



> ## Crack it
>
> ### 100
>
> 
>
> 破解该文件，获得密码，flag格式为：flag{*****}
>
> 来源：第七届山东省大学生网络安全技能大赛
>
> [shadow](Crack it/shadow)



## 1.shadow文件破解

参考

* [linux根文件系统 /etc/shadow文件详解](https://blog.csdn.net/mybelief321/article/details/10045873)
* [linux shadow文件破解](http://gv7.me/articles/2017/batch-crack-shadows/)



`john --show shadow`

> root:hellokitty:17770:0:99999:7:::
>
> 1 password hash cracked, 0 left

得到`flag{hellokitty}`