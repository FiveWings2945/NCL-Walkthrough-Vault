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

![[MB-HxD Header.png]]

The header is correct for a Jpeg/Jfif file. Lets check the footer

![[MB-HxD Footer.png]]

Ahah! That's a PNG footer! Now all we have to do is figure out what the original file is. Assuming since the file came as a jpeg wit a png footer, the image will be a PNG. All we have to do is edit the header to the png header `89 50 4E 47 0D 0A 1A 0A`.

Q1
What is the original file type? 

We found what the footer type was and we can figure that the image follows that.


Continuing on, we can rename the image to PNG and open it up.

![[MB-PNG opening.png]]

Huh? Whats going on? We edited the header so everything should be fine, right? Well, we look back to the image hex and find some leftover hex from the JFIF header. The header for that file type is a bit longer than PNG (by 2 bytes). So we can zero that out and try opening our file again.

![[MB-Flag.png]]

There we go. That wasn't too bad

Q2
Whats the flag?

Found after recovering the corrupt image