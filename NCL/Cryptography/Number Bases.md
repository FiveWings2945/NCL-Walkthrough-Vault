Created: 2025-09-18

Challenge Type: #Cryptography
Challenge Difficulty: #Easy
Attachments: None

Number Bases
Description
***
Our analysts have obtained password dumps storing hacker passwords. After obtaining a few plaintext passwords, it appears that they are all simply encoded using different number bases.

Questions
***
Just based on the title, this will be related to number bases, like base 2 (binary) or base 64 encryption. These encryption methods are substitution ciphers, where letters are substituted with a code. We can use [cyber chef](https://gchq.github.io/CyberChef/) to decode these values.

| User    | Ciphertext                                                                                                  | Encoding     | Why?                                                                                                                   |
| ------- | ----------------------------------------------------------------------------------------------------------- | ------------ | ---------------------------------------------------------------------------------------------------------------------- |
| Patrick | 0x73636f7270696f6e                                                                                          | Hex (base 6) | `0x` often denotes hexidecimal                                                                                         |
| Stevie  | c2NyaWJibGU=                                                                                                | Base 64      | The `=` symbol at the end will often signal base 32 or 64. However, since there are lowercase letters, this is base 64 |
| Nan     | 01110011 01100101 01100011 01110101 01110010 01100101 01101100 01111001                                     | Binary       | Code of 1's and 0's is often binary                                                                                    |
| Mollie  | 01100010 01000111 00111001 01110011 01100010 01000111 01101100 01110111 01100010 00110011 01000001 00111101 | Binary       | Code of 1's and 0's is often binary                                                                                    |
