Created: 2025-09-18

Challenge Type: #Cryptography
Challenge Difficulty: #Easy
Attachments:

@bash
Description
***
Our analysts have obtained password dumps storing hacker passwords. See if you can crack them.

Questions
***
Based on the challenge title, the passwords probably use an At-Bash operation. We can use cyber chef to solve this challenge.

| User  | Ciphertext          | Encoding | Why?                                                                                                                                                                                                                                       |
| ----- | ------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Molly | hzuvob lyerlfh xzev | Atbash   | The text looks like a substitution cipher, so there are a handful of options we can try. I start with rotation ciphers because they are simple, and it wasnt quite right. I check the other common substitution cipher and it was correct. |
