# sign_simple_baidu_bce_python3
百度 bce auth 签名生成方法 Python3 语法修改
官方 Python2.7 版本链接：https://cloud.baidu.com/doc/Reference/AuthenticationMechanism.html#Python.E7.A4.BA.E4.BE.8B


执行 2to3 后，进一步修改如下：
hmac.new 方法只接受 utf8 编码的 byte
``` python
sign_key = hmac.new(
        bytes(credentials.secret_access_key, 'utf-8'),
        bytes(sign_key_info, 'utf-8'),
        hashlib.sha256).hexdigest()
        
sign_result = hmac.new(bytes(
        sign_key, 'utf-8'), bytes(string_to_sign, 'utf-8'), hashlib.sha256).hexdigest()
```

lambda 表达式传入的索引fix
```
if encoding_slash:
    def encode_f(c): return NORMALIZED_CHAR_LIST[int(c)]
else:
    def encode_f(c): return NORMALIZED_CHAR_LIST[int(c)] if c != '/' else c
```

这样就能正确生成了
```
/anaconda3/bin/python sign_sample.py
bce-auth-v1/0b0f67dfb88244b289b72b142befad0c/2015-04-27T08:23:49Z/1800//c2d82f9eb62e93233a60f507b67ede797fa4a75d82eef4c35727f97d23b5defa
```
