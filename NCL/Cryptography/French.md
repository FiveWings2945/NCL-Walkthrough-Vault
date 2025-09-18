Created: 2025-09-18

Challenge Type: #Cryptography
Challenge Difficulty: #Medium
Attachments: None

French
Description
***
Our analysts have obtained an encrypted message. We know that the key, "qizkwcgqbs" was used. See if you can crack them.

Questions
***
This is another public key encryption. I search for "French" in cyber chef and it does not return anything helpful. I can use two tools here to determine the cipher. Since the title has a hint to the cipher, I can google French cipher to get a cipher that looks promising. I can also use dcode's [cipher identifier](https://www.dcode.fr/cipher-identifier) to help me determine what the cipher is. By plugging the cipher text in, we get this result:
![[Crypto-French.png]]
The top three results are:
- Jefferson Wheel Cipher
- Ragbaby Cipher
- Vigenere Cipher

I need a cipher that uses a key for encryption. The first two options are both monoalphabetic substitution ciphers, so they can be right. I then look to Vigenere Cipher, a cipher developed by a **French** diplomat in the 1500's. This might be the right track. I go back to cyber chef and plug in the key to the Vigenere recipe and get my cipher text. 

| User | Ciphertext                                                     | Encoding | Why?                                                                    |
| ---- | -------------------------------------------------------------- | -------- | ----------------------------------------------------------------------- |
| Tom  | Y ln xkv lubj swlzqvkht, A vmzb pjk bbua we ddgs ILQ-GQYU-8026 | Vigenere | A public key cipher. Based on the title, its a french cipher (Vigenere) |
