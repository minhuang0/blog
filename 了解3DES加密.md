title: 了解3DES加密
date: 2016-03-06
tags: 
    - 3DES
categories: 编程

---
3DES（Triple DES）是三重数据加密算法（TDEA，Triple Data Encryption Algorithm）,对一个数据块进行三次的DES加密。
<!--more-->  
加密过程:

密文 = EK3(DK2(EK1(平文)))

也就是说，使用K1为密钥进行DES加密，再用K2为密钥进行DES“解密”，最后以K3进行DES加密。

而解密则为其反过程：

平文 = DK1(EK2(DK3(密文)))

即以K3解密，以K2“加密”，最后以K1解密。

每次加密操作都只处理64位数据，称为一块。

标准定义了三种密钥选项：

密钥选项1：三个密钥是独立的。
密钥选项2：K1和K2是独立的，而K3=K1
密钥选项3：三个密钥均相等，即K1=K2=K3
这是一个对String进行3des用ruby加密的一小段代码（仅做个人纪录）

```ruby
# -*- encoding : utf-8 -*-
require 'digest'
require 'openssl'
require 'base64'
KEY = "Y6WawY6WawY6WawY6WawY6WawY6WawY6Waw"
STR = "中国人"
cipher = OpenSSL::Cipher::Cipher.new("DES-EDE3")
cipher.encryptcipher.key = KEYencrypted_string = cipher.update(STR) + cipher.finalputs Base64.encode64(encrypted_string);
```
