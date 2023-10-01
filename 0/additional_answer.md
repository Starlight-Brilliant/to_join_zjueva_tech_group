以解密算法为例:  
```Python
decrypt = lambda cipher, key: "".join([chr(int(cipher.split('/')[i], 16) // ord(key[i])) for i in range(4)])
```
这是一行结合了Python的**匿名函数**与**列表推导式**的极简代码，综合使用了匿名函数创建和(for loop和list处理和创建)的*语法糖*，在实现上等价于  
```Python
def decrypt(cipher, key):
    res = ""
    for i in range(4):
        res += chr(int(cipher.split('/')[i], 16) // ord(key[i]))
    return res
```
与第二种实现相比，第一种要简洁许多，但是代码过于紧密，不美观，不方便debug，不方便优化，甚至补注释都让人抓狂，实际上，在日常编程中并不太建议用第一种方式。  
收到题目限制，几乎没有可以更优的方法，  
但是，如果抛开题目限制（也就是明文可能很长很长），很明显可以发现`cipher.split('/')`数据预处理部分**被执行了多次，每次却只取一个值**，这其实是一种低效的数据处理方式，  
理论上，应该把预处理的结果缓存起来，再一个一个进行解密处理。
```Python
def my_decrypt(cipher: str, key: str) -> str:
    res = ""
    tmp = cipher.split('/')
    for i in range(4):
        res += chr(int(tmp[i], 16) // ord(key[i]))
    return res
```
这样写更舒服一些。
