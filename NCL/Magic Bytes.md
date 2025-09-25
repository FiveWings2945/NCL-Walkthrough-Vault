Created: 2025-09-25

Challenge Type: #Forensics 
Challenge Difficulty: #Medium
Attachments: flag.jpeg

Magic Bytes
Description
***
This file appears to be changed in some way. Can you recover the original?

(You can use either CyberChef or a tool of your choosing to complete this challenge)

Questions
***
When we try to open the file, it doesnt. Instead it gives us an error, saying the format isnt supported or the file is corrupted. Well, lets see if binwalk can find anything helpful here
```sh
┌──(kali㉿kali)-[~/Downloads]
└─$ binwalk flag.jpeg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 13.73, thumbnail 1x-114
537           0x219           Zlib compressed data, best compression

```

Hmm, not much here. Maybe checking the metadata will help?

```sh
┌──(kali㉿kali)-[~/Downloads]
└─$ exiftool flag.jpeg
ExifTool Version Number         : 13.10
File Name                       : flag.jpeg
Directory                       : .
File Size                       : 7.1 kB
File Modification Date/Time     : 2025:09:25 19:53:34-04:00
File Access Date/Time           : 2025:09:25 19:53:57-04:00
File Inode Change Date/Time     : 2025:09:25 19:53:34-04:00
File Permissions                : -rw-rw-r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
Warning                         : JPEG format error
```

Thats interesting. Its giving us a JPEG format error. Maybe then its something deeper that is wrong. Something on the binary level. Lets open up our favorite hex editor (in my case, thats HxD)