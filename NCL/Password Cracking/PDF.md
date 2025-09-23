Created: 2025-09-22

Challenge Type: #Password
Challenge Difficulty: #Medium
Attachments: [[encrypted.pdf]]

PDF
Description
***
We have captured an encrypted pdf from a hacker's FTP server. Decrypt it and find out what you can.
Questions
***
Q1
What is the password used to encrypt the pdf?

Here we are tasked with finding the password of an encrypted PDF. We can assume that the flag will be contained in this PDF, so we can start by cracking the password to the pdf. John the Ripper has a very helpful tool in helping with this challenge. 

`pdf2john encrypted.pfd > hash.txt`

This will give us a crack-able hash for the pdf password for hashcat or john to handle. We just have to trim a bit of the pdf2john output so that hashcat will accept it.
raw:
```
encrypted.pdf:$pdf$5*6*256*-etc...
```
trimmed:
```
$pdf$5*6*256*-etc...
```
I will personally use hashcat here, but john will be just as good.

`-m 10700`: hashmode 10700 - PDF 1.7 Level 8 (Acrobat 10 - 11) 
`-a 0`: attackmode 0 - standard attack (\[wordlist] Incremental ASCII)
`hash.txt`: hash
`/usr/share/wordlists/rockyou.txt`: wordlist (rockyou is always a good place to start when not having to build a wordlist)
(Note: This cracking may take a bit as hashcat has to convert each password into a proper hash. This isnt as fast as md5!)

Eventually, you will get the password from the hash. 


Q2
What is the flag in the PDF?

This is the flag you get from opening the PDF with the password you got in Q1. It also doubles as a pretty funny meme (not really....)