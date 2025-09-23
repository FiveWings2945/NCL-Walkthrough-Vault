Created: 2025-09-19

Challenge Type: #Password
Challenge Difficulty: #Easy
Attachments: None

Rockyou
Description
***
Our analysts have obtained password dumps storing hacker passwords. After obtaining a few plaintext passwords, it appears that they overlap with the passwords from the rockyou breach.

Questions
***
First we can analyze the description and the title. Right off the bat, we can tell we will be using the Rockyou wordlist for this challenge (info on why rockyou is significant [here](https://en.wikipedia.org/wiki/RockYou) if you're interested).

By looking at the hashes provided, we can take an educated guess these are MD5 hashes. Just in case though, we can run hashcat on any one of the hashes and look at its analysis.

(By default, if you dont pass any options to hashcat, the program will start in analysis mode)
```
┌──(kali㉿kali)-[~]
└─$ hashcat 68a96446a5afb4ab69a2d15091771e39                                    
hashcat (v6.2.6) starting in autodetect mode

OpenCL API (OpenCL 3.0 PoCL 6.0+debian  Linux, None+Asserts, RELOC, LLVM 18.1.8, SLEEF, DISTRO, POCL_DEBUG) - Platform #1 [The pocl project]
============================================================================================================================================
* Device #1: cpu-sandybridge-Intel(R) Core(TM) i5-8250U CPU @ 1.60GHz, 2913/5890 MB (1024 MB allocatable), 4MCU

The following 11 hash-modes match the structure of your input hash:

      # | Name                                                       | Category
  ======+============================================================+======================================
    900 | MD4                                                        | Raw Hash
      0 | MD5                                                        | Raw Hash
     70 | md5(utf16le($pass))                                        | Raw Hash
   2600 | md5(md5($pass))                                            | Raw Hash salted and/or iterated
   3500 | md5(md5(md5($pass)))                                       | Raw Hash salted and/or iterated
   4400 | md5(sha1($pass))                                           | Raw Hash salted and/or iterated
  20900 | md5(sha1($pass).md5($pass).sha1($pass))                    | Raw Hash salted and/or iterated
   4300 | md5(strtoupper(md5($pass)))                                | Raw Hash salted and/or iterated
   1000 | NTLM                                                       | Operating System
   9900 | Radmin2                                                    | Operating System
   8600 | Lotus Notes/Domino 5                                       | Enterprise Application Software (EAS)

Please specify the hash-mode with -m [hash-mode].

Started: Fri Sep 19 14:16:58 2025
Stopped: Fri Sep 19 14:17:01 2025

```

Both MD4 and MD5 show up as probable options, but since MD5 is more relevant, we will try that one first. When using hashcat, we have to set a few options:

`hashcat` - name of the program
`-m 0` - hash-mode 0: md5 (per the analysis we got)
`-a 0` - attack-mode 0: standard cracking (\[wordlist] Incremental ASCII)
`'68a96446a5afb4ab69a2d15091771e39'` - hash
`/usr/share/wordlists/rockyou.txt` - wordlist we are using
Note: Rockyou is always a good starting point for CTF challenges. You can install the wordlists directory shown in the command above in Linux if you havent already by running

`sudo apt install wordlists`

We will then set our hashcat options and run:

```
┌──(kali㉿kali)-[~]
└─$ hashcat -m 0 -a 0 '68a96446a5afb4ab69a2d15091771e39' /usr/share/wordlists/rockyou.txt
hashcat (v6.2.6) starting

OpenCL API (OpenCL 3.0 PoCL 6.0+debian  Linux, None+Asserts, RELOC, LLVM 18.1.8, SLEEF, DISTRO, POCL_DEBUG) - Platform #1 [The pocl project]
============================================================================================================================================
* Device #1: cpu-sandybridge-Intel(R) Core(TM) i5-8250U CPU @ 1.60GHz, 2913/5890 MB (1024 MB allocatable), 4MCU

..Output shortened..

68a96446a5afb4ab69a2d15091771e39:[PASSWORD]               
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 0 (MD5)
Hash.Target......: 68a96446a5afb4ab69a2d15091771e39
Time.Started.....: Fri Sep 19 14:20:47 2025 (3 secs)
Time.Estimated...: Fri Sep 19 14:20:50 2025 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (Documents/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:  2638.5 kH/s (0.29ms) @ Accel:512 Loops:1 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 8331264/14344385 (58.08%)
Rejected.........: 0/8331264 (0.00%)
Restore.Point....: 8329216/14344385 (58.07%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidate.Engine.: Device Generator
Candidates.#1....: [PASSWORD] -> [PASSWORD]
Hardware.Mon.#1..: Util: 58%

Started: Fri Sep 19 14:20:40 2025
Stopped: Fri Sep 19 14:20:51 2025
                                   
```

We can see in status that the password has been cracked. The password will be outputted by the hash.

Note: You can also run hashcat on a collection of passwords by putting them in a txt file then passing them into the command like this:

`hashcat -m 0 -a 0 /path/to/hashes.txt /usr/share/wordlists/rockyou.txt --show`

This way you can crack multiple hashes at a time

| User    | Password Hash                    | Hash Type? |
| ------- | -------------------------------- | ---------- |
| Tom     | 68a96446a5afb4ab69a2d15091771e39 | md5        |
| Laura   | ec5f0b1826389df8622133014e88afde | md5        |
| Jenny   | 32e5f63b189b78dccf0b97ac41f0d228 | md5        |
| Lindsay | 2233287f476ba63323e60addca1f6b64 | md5        |
| Zoe     | 6539bbb84fe2de2628fc5e4f2a31f23a | md5        |
