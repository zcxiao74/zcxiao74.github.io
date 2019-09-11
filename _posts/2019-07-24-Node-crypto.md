---
layout: post
title: "Node-加密"
date: 2019-07-24
tags: HTML  
---

#  crypto(加密和哈希算法)

## MD5

```
const  crypto = require("crypto");

const hash = crypto.createHash("md5");

hash.update("hello world");

console.log(hash.digest('hex'));

console.log("----------------------------");
```



## SHA1

```
const  crypto = require("crypto");

const sha1 = crypto.createHash("sha1");

sha1.update("hello world");

console.log(sha1.digest('hex'));

console.log("----------------------------");
```



## Hmac

```
const  crypto = require("crypto");

const hamc = crypto.createHmac("sha256","secret-key");

hamc.update("hello world");

console.log(hamc.digest("hex"));

console.log("----------------------------");
```



## AES

```
const  crypto = require("crypto");

function aesEncrypt(data,key){

	 const cipher = crypto.createCipher("aes192",key);

	   var crypted = cipher.update(data,"utf8","hex");

	  crypted += cipher.final("hex");

	  return crypted;

}



function aesDecrypt(encrypted,key){

	 const decipher = crypto.createDecipher("aes192",key);

	 var decrypted = decipher.update(encrypted,"hex","utf8");

	 decrypted += decipher.final("utf8");

	  return decrypted;

}

var data = "hello world";

var key = "xiao";

var encrypted = aesEncrypt(data,key);

var decrpted = aesDecrypt(encrypted,key);



console.log(data);

console.log(encrypted);

console.log(decrypted);

console.log("----------------------------");
```

