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

    d6c26f41fb3d9fdf5c59131f827675
    [214, 194, 111, 65, 251, 61, 159, 223, 92, 89, 19, 31, 130, 118, 117]


Xor-ing the message with key gives us the ciphertext bytes


```python
ciphertext: bytes = utils.xor(message1, key)
print(ciphertext.hex())
print(list(ciphertext))
```

    97b61b209856bfbe2879777ef51854
    [151, 182, 27, 32, 152, 86, 191, 190, 40, 121, 119, 126, 245, 24, 84]


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

When the intended recipient decrypts the modified ciphertext they get the wrong message.


```python
decrypted = utils.xor(modified_ctext, key)
print(decrypted)
```

    b'Attack at dusk!'


### Security games

Security games help model a combination of adversary capabilities with security goals.

The game or (challenger) is built from an encryption scheme which includes

- a key generation function;
- an encryption function;
- and a decryption function.

For our first example, we will use a shift cipher.


```python
def shift_cipher_encrypt(key: int, message: bytes) -> bytes:
    ctext = bytes([(b + key) % 256 for b in message])
    return ctext
```

And we can try it out.


```python
shift_cipher_encrypt(3, b"Attack at dawn")
```




    b'Dwwdfn#dw#gdzq'




```python
def shift_cipher_decrypt(key: int, message: bytes) -> bytes:
    ctext = bytes([(b - key) % 256 for b in message])
    return ctext
```


```python
def shift_cipher_keygen() -> int:
    return secrets.randbelow(256)
```


```python
key = shift_cipher_keygen()

m = b"Attack at dawn!"

assert m == shift_cipher_decrypt(key, shift_cipher_encrypt(key, m))
```

For the IND-EAV (Indistinguishability in the presense of a eavesdropper) we won't be using the decryption function, so we just define the game with the key generation function and the encryption function.



```python
shift_eav_game = sec_games.IndEav(shift_cipher_keygen, shift_cipher_encrypt)
```

The challenger (the game) must pick a key and a bit, _b_ that it keeps to itself. This is done with the `initialize()` method.


```python
shift_eav_game.initialize()
```

The adversary picks two plaintexts.


```python
m0 = b"AA"
m1 = b"AB"
```

We tell the challenger will encrypt one of them depending in its choice of bit _b_ and its key which it created during inititialization.


```python
ctext = shift_eav_game.encrypt_one(m0, m1)
```

Now the adversary uses its understanding of m0, m1, ctext and how the shift cipher works to try to construct a guess of whether m0 m1 was encrypted.

In this case it is easy, because the shift cipher will encrypt each identical input byte the same way. Different input bytes will be encrypted differently.


```python
if ctext[0] == ctext[1]:
    #  "AA" was encrypted
    guess = False  # b is 0
else:
    # "AB" was encrypted
    guess = True  # b is 1
```

And now we check whether the guess was correct


```python
shift_eav_game.finalize(guess)
```




    True


