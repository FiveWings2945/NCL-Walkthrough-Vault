Created: 2025-09-18

Challenge Type: #Cryptography
Challenge Difficulty: #Easy
Attachments: None

Shift
Description
***
Our analysts have obtained password dumps storing hacker passwords. It seems to be using a pretty simple encryption scheme, see if you can crack them.

Questions
***
Based on the challenge title, the passwords probably use a Bit-Shift operation, similar to a Caesar Cipher. We can use cyber chef to solve this challenge.

| User  | Ciphertext   | Encoding | Why?                                                                                                                                                                                |
| ----- | ------------ | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Jenny | iveghny ynxr | ROT-13   | The text looks like a substitution cipher, so there are a handful of options we can try. I start with rotation ciphers because they are simple, and it happened to be correct here. |
