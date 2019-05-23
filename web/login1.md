# login1(SKCTF)



> ## login1(SKCTF)
>
> ### 100
>
> 
>
> <http://123.206.31.85:49163/>
> flag格式：SKCTF{xxxxxxxxxxxxxxxxx}
> hint:SQL约束攻击



## 1.任意权限用户登陆

正常注册登陆 发现关键字 `不是管理员还想看flag？！`

于是开始想办法获取管理员权限

网上搜索SQL约束攻击发现 `在执行sql语句时候，字符串末尾的空格会被删除`

那么可以思考构造一个admin+空格的账户进行测试

`’admin               ‘`

登陆得到flag



`SKCTF{4Dm1n_HaV3_GreAt_p0w3R}`