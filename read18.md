[ HOME ](README.md)
# Read 18 - Cryptography, AKA Caesar's cipher, the shift cipher, Caesar's code or Caesar shift

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4a/Caesar_cipher_left_shift_of_3.svg/330px-Caesar_cipher_left_shift_of_3.svg.png)

- Is one of the simplest and most widely known encryption techniques.
- It is a type of substitution cipher in which each letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet. 
- It is still has modern application in the ROT13 system.

### Example
- The transformation can be represented by aligning two alphabets; the cipher alphabet is the plain alphabet rotated left or right by some number of positions.
```
Plain:    ABCDEFGHIJKLMNOPQRSTUVWXYZ
Cipher:   XYZABCDEFGHIJKLMNOPQRSTUVW
```

When encrypting, a person looks up each letter of the message in the "plain" line and writes down the corresponding letter in the "cipher" line.

```
Plaintext:  THE QUICK BROWN FOX JUMPS OVER THE LAZY DOG
Ciphertext: QEB NRFZH YOLTK CLU GRJMP LSBO QEB IXWV ALD
```

- The encryption can also be represented using modular arithmetic by first transforming the letters into numbers, according to the scheme, A → 0, B → 1, ..., Z → 25. 
- Encryption of a letter x by a shift n can be described mathematically as:

```
E_{n}(x)=(x+n)\mod 26.
E_{n}(x)=(x+n)\mod 26.
```
Decryption is performed similarly,

{\displaystyle D_{n}(x)=(x-n)\mod {26}.}D_{n}(x)=(x-n)\mod {26}.
(There are different definitions for the modulo operation. In the above, the result is in the range 0 to 25; i.e., if x + n or x − n are not in the range 0 to 25, we have to subtract or add 26.)

___

# Video
[Tutorial](https://www.youtube.com/watch?v=jhXCTbFnK8o)