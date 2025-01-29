---
title: "A toy example"
subtitle: "An attempt to blog using Jupyter"
summary: "A little bit of toy cryptography in a Jupyter notebook"
authors: [jpgoldberg]
tags: []
categories: []
date: 2025-01-29T00:14:42Z
lastmod: 2025-01-29T00:14:42Z
featured: false
draft: true
---
# Jupyter and Hugo

I have not had a lot of fun dealing with Hugo, HugoBlox, and academic-cv updates.
Perhaps someday I will write about what I learned, although I have not quite figured that out yet.

So for now we have a simple test of posting from Jupyter notebooks.


Attempting to follow the instructions https://miguelrodrigues.org/post/jupyter/

## Toy crypto examples

I've created a [toycrypto Python project](https://pypi.org/project/toycrypto/) primarily so that I could create reproducible code examples, including Jupyter notebooks, so that is what I will use for examples here.


```python
import secrets
from toy_crypto import sec_games, utils
```


```python
message1: bytes = b"Attack at dawn!"
message2: bytes = b"Attack at dusk!"
```

We want to create a key that is at least as long as the message, and we want to use a cryptographically secure random number generator to do so.


```python
length = len(message1)
key: bytes = secrets.randbits(length * 8).to_bytes(length)
print(key.hex())
print(list(key))
```

    ef3523a2cafa973f96008cb141e447
    [239, 53, 35, 162, 202, 250, 151, 63, 150, 0, 140, 177, 65, 228, 71]


Xor-ing the message with key gives us the ciphertext bytes


```python
ciphertext: bytes = utils.xor(message1, key)
print(ciphertext.hex())
print(list(ciphertext))
```

    ae4157c3a991b75ee220e8d0368a66
    [174, 65, 87, 195, 169, 145, 183, 94, 226, 32, 232, 208, 54, 138, 102]


If you do not know the key, the _contents_ of the ciphertext (other than its length) tells you nothing you _didn't already know_ about the message.

Suppose you already had reason to suspect that the message is either "`Attack at dawn!`" or "`Attack at dusk!`". Examining the ciphertext gives you no way to improve or update your assessment of the content of the message.

Someone who knows the key can decrypt.


```python
decrypted: bytes = utils.xor(ciphertext, key)
print(decrypted)
```

    b'Attack at dawn!'


### Malleablity

Even if an attacker can't learn anything new about the message from the ciphertext, they can still do damage if they have a good guess at its contents and have the opportunity to tamper with it in transit.

So again, let's assume that the attacker has reason to believe (via spies for example) that the message is either "`Attack at dawn!`" or "`Attack at dusk!`". The attacker can modify the ciphertext so that it will decrypt to the wrong message.



The attacker first creates a sequwence of bytes that is the difference between to two messages



```python
dusk_dawn_diff = utils.xor(message1, message2)

print(dusk_dawn_diff.hex())
print(list(dusk_dawn_diff))
```

    000000000000000000000014040500
    [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 20, 4, 5, 0]


The attacker takes the original ciphertext and xors it with the ciphertext to get a modified ciphertext.


```python
modified_ctext = utils.xor(ciphertext, dusk_dawn_diff)
```

When the intended recipient decrypts the modified ciphertext they get the wrong messagew.


```python
decrypted = utils.xor(modified_ctext, key)
print(decrypted)
```

    b'Attack at dusk!'

