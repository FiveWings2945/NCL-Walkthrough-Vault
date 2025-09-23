Created: 2025-09-19

Challenge Type: #Password
Challenge Difficulty: #Medium
Attachments: None

Mask
Description
***
Our analysts have obtained password dumps storing hacker passwords. After obtaining a few plaintext passwords, it appears that they are all in the format: `SKY-HQNT-` followed by 4 digits. Can you crack them?

Questions
***
First lets analyze the title and description. We are told that the passwords of the hashes provided start with `SKY-HQNT-`. This is similar to the format of a NCL flag, so we can assume that the passwords will be `SKY-HQNT-####` where # is a decimal number. 

Here we are given hashes that look like they are in the md5 format. We can confirm this through hashcat:

```
┌──(kali㉿kali)-[~]
└─$ hashcat 71b816fe0b7b763d889ecc227eab400a                                  
hashcat (v6.2.6) starting in autodetect mode

OpenCL API (OpenCL 3.0 PoCL 6.0+debian  Linux, None+Asserts, RELOC, LLVM 18.1.8, SLEEF, DISTRO, POCL_DEBUG) - Platform #1 [The pocl project]
============================================================================================================================================
* Device #1: cpu-sandybridge-Intel(R) Core(TM) i5-8250U CPU @ 1.60GHz, 2913/5890 MB (1024 MB allocatable), 4MCU

The following 11 hash-modes match the structure of your input hash:

      # | Name                                                       | Category
  ======+============================================================+======================================
    900 | MD4                                                        | Raw Hash
      0 | MD5                                                        | Raw Hash
 
 ..Output Shortened..

Started: Fri Sep 19 14:34:49 2025
Stopped: Fri Sep 19 14:34:49 2025

```

The interesting thing about this challenge however is we need to use something called a mask. Hashcat has a bruteforce mode (-m 3) that we can use. In order to apply a mask, we need a REGEX expression so hashcat know what to brute force. We can use the following regex to achieve the 4 digits of text at the end: `?d?d?d?d` (Following Hashcat's charsets). We can then append this to our mask to get:

`'SKY-HQNT-?d?d?d?d`

We can then load our passwords into hashes.txt (the commands doesnt work without it) and we can then run hashcat with the following commands:

`-m 0`: Hash-mode 0 - md5
`-a 3`: Attack-mode 3 - bruteforce
`hashes.txt`: hashes
`'SKY-HQNT-?d?d?d?d'`: Mask
`--show`: show the passwords when they are cracked

```
hashcat -m 0 -a 3 ./hash.txt 'SKY-HQNT-?d?d?d?d' --show
hashcat (v6.2.6) starting

OpenCL API (OpenCL 3.0 PoCL 6.0+debian  Linux, None+Asserts, RELOC, LLVM 18.1.8, SLEEF, DISTRO, POCL_DEBUG) - Platform #1 [The pocl project]
============================================================================================================================================
* Device #1: cpu-sandybridge-Intel(R) Core(TM) i5-8250U CPU @ 1.60GHz, 2913/5890 MB (1024 MB allocatable), 4MCU

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

INFO: All hashes found as potfile and/or empty entries! Use --show to display them.

Started: Fri Sep 19 14:50:04 2025
Stopped: Fri Sep 19 14:50:04 2025
```



| Name   | Hash                             | Hash Type? |
| ------ | -------------------------------- | ---------- |
| Helen  | 71b816fe0b7b763d889ecc227eab400a | md5        |
| Stevie | 674291170dffcf620bda2a604a6820ea | md5        |
| Chris  | 06f03267f31077d2c4b5c728472070ae | md5        |
| Tom    | d866f4b3b34b598375149fb7661113ab | md5        |
| Mark   | d9053951a8d1c15254b46ec9fc974a6b | md5        |
