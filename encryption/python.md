# python(N1CTF)





> ## python(N1CTF)
>
> ### 100
>
> 
>
> 
>
> [challenge.py](python/challenge.py)
>
> [N1ES.py](python/ddaf74ef46efdb8adffb3f9f93049bbf/N1ES.py)





## 1.python脚本解密

> 根据题目大概意思，是让我们根据已知的加密方式，写出解密的脚本
>
> `HRlgC2ReHW1/WRk2DikfNBo1dl1XZBJrRR9qECMNOjNHDktBJSxcI1hZIz07YjVx`
>
> 难度较大 放弃



以下是网上抄的python代码

参考[N1CTF baby_N1ES writeup](<https://findneo.github.io/180310N1CTFWP/>)

```python
import base64,string,N1ES
key = "wxy191iss00000000000cute"
c = base64.b64decode("HRlgC2ReHW1/WRk2DikfNBo1dl1XZBJrRR9qECMNOjNHDktBJSxcI1hZIz07YjVx")
n1es = N1ES.N1ES(key)
f=""
for i in xrange(3):
	for j in xrange(16):
		for k in string.printable:
			s="x"*i*16+"x"*j+k+"x"*(48-i*16-j-1)
			e=n1es.encrypt(s)
			check=c[i*16+j+8]==e[i*16+j+8] if j<8 else c[i*16+j-8]==e[i*16+j-8]
			if check:
				f+=k
				break
print f
# N1CTF{F3istel_n3tw0rk_c4n_b3_ea5i1y_s0lv3d_/--/}
```



或者参考[**Bugku 密码学AK指南**](<https://blog.csdn.net/prowes5/article/details/85167667>)

```python
# -*- coding: utf-8 -*-
import base64
def round_add(a,b):
	f = lambda x,y: x + y - 2 * (x & y)
	res = ''
	for i in range(len(a)):
		res += chr(f(ord(a[i]),ord(b[i])))
	return res

def permutate(table,block):
	return list(map(lambda x: block[x], table))

def string_to_bits(data):
	data = [ord(c) for c in data]
	l = len(data)*8
	result = [0] * l
	pos = 0
	for ch in data:
		for i in range(0,8):
			result[(pos<<3)+i] = (ch>>i) & 1
		pos += 1
	return result

s_box = [54, 132, 138, 83, 16, 73, 187, 84, 146, 30, 95, 21, 148, 63, 65, 189, 188, 151, 72, 161, 116, 63, 161, 91, 37, 24, 126, 107, 87, 30, 117, 185, 98, 90, 0, 42, 140, 70, 86, 0, 42, 150, 54, 22, 144, 153, 36, 90, 149, 54, 156, 8, 59, 40, 110, 56,1, 84, 103, 22, 65, 17, 190, 41, 99, 151, 119, 124, 68, 17, 166, 125, 95, 65, 105, 133, 49, 19, 138, 29, 110, 7, 81, 134, 70, 87, 180, 78, 175, 108, 26, 121, 74, 29, 68, 162, 142, 177, 143, 86, 129, 101, 117, 41, 57, 34, 177, 103, 61, 135, 191, 74, 69, 147, 90, 49, 135, 124, 106, 19, 89, 38, 21, 41, 17, 155, 83, 38, 159, 179, 19, 157, 68, 105, 151, 166, 171, 122, 179, 114, 52, 183, 89, 107, 113, 65, 161, 141, 18, 121, 95, 4, 95, 101, 81, 156, 17, 190, 38, 84, 9, 171, 180, 59, 45, 15, 34, 89, 75, 164, 190, 140, 6, 41, 188, 77, 165, 105, 5, 107, 31, 183, 107, 141, 66, 63, 10, 9, 125, 50, 2, 153, 156, 162, 186, 76, 158, 153, 117, 9, 77, 156, 11, 145, 12, 169, 52, 57, 161, 7, 158, 110, 191, 43, 82, 186, 49, 102, 166, 31, 41, 5, 189, 27]

def generate(o):
	k = permutate(s_box,o)
	b = []
	for i in range(0,len(k),7):
		b.append(k[i:i+7]+[1])
	c = []
	for i in range(32):
		pos = 0
		x = 0
		for j in b[i]:
			x += (j<<pos)
			pos += 1
		c.append((0x10001**x) % (0x7f))
	return c

class N1ES:
	def __init__(self,key):
		if (len(key) != 24 or isinstance(key,bytes) == False):
			raise Exception("key must be 24 bytes long")
		self.key = key
		self.gen_subkey()
	
	def gen_subkey(self):
		o = string_to_bits(self.key)
		k = []
		for i in range(8):
			o = generate(o)
			k.extend(o)
			o = string_to_bits([chr(c) for c in o[0:24]])
		self.Kn = []
		for i in range(32):
			self.Kn.append(map(chr,k[i*8: i*8+8]))
		return
	
	def decrypt(self,plaintext):
		res = ''
		for i in range(len(plaintext)/16):
			block = plaintext[i*16:(i + 1)*16]	
			L = block[:8]
			R = block[8:]
			for round_cnt in range(32):
				L,R = R, (round_add(L, self.Kn[31-round_cnt]))
			L,R = R,L
			res += L + R
		return res


key = "wxy191iss00000000000cute"
nles = N1ES(key)
flag = base64.b64decode("HRlgC2ReHW1/WRk2DikfNBo1dl1XZBJrRR9qECMNOjNHDktBJSxcI1hZIz07YjVx")
flag = nles.decrypt(flag)
print flag

```

