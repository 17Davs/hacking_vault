   

HMACs

HMACs

### HMACs

**HMAC (Keyed-Hash Message Authentication Code)** is a type of message authentication code (MAC) that uses a cryptographic hash function in combination with a secret key to verify the authenticity and integrity of data.

An HMAC can be used to ensure that the person who created the HMAC is who they say they are, i.e., authenticity is confirmed; moreover, it proves that the message hasn’t been modified or corrupted, i.e., integrity is maintained. This is achieved through the use of a secret key to prove authenticity and a hashing algorithm to produce a hash and prove integrity.

The following steps give you a fair idea of how HMAC works.

1. The secret key is padded to the block size of the hash function.
2. The padded key is XORed with a constant (usually a block of zeros or ones).
3. The message is hashed using the hash function with the XORed key.
4. The result from Step 3 is then hashed again with the same hash function but using the padded key XORed with another constant.
5. The final output is the HMAC value, typically a fixed-size string.

The illustration below should clarify the above steps.

![A visual representation of the HMAC function.](Hacking%20Vault/Attachments/4354e8f9cef94fe0a83e8172d9a85483.svg)

Technically speaking, the HMAC function is calculated using the following expression:

_H**M**A**C_(_K_,_M_) = _H_((_K_⊕_o**p**a**d_)||_H_((_K_⊕_i**p**a**d_)||_M_))

Note that M and K represent the message and the key, respectively.