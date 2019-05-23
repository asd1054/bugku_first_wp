# affine



> ## affine
>
> ### 100
>
> 
>
> y = 17*x-8 flag{szzyfimhyzd}答案格式：flag{******}
>
> 来源：第七届山东省大学生网络安全技能大赛





## 1.仿射加密

> #### affine 为仿射的意思，那就 仿射加密，直接解密
>
> **仿射密码**为单表加密的一种，字母系统中所有[字母](https://baike.baidu.com/item/字母/1710184)都藉一简单数学方程[加密](https://baike.baidu.com/item/加密/752748)，对应至数值，或转回字母。
>
> 参考 [仿射密码（affine）原理解密](<https://blog.csdn.net/weixin_43858318/article/details/89202645>)

```python
y = 'szzyfimhyzd'
flag = ''
for i in y:
	i = ord(i)
	for j in range(0,26):
		if i == (17*j-8)%26+97: #如果相等，赋值给flag
			flag += chr(j+97)
print(flag)
```

`flag{affineshift}`