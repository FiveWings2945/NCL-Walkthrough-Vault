Created: 2025-09-25

Challenge Type: #Forensics
Challenge Difficulty: #Medium
Attachments: green_file

File Carving
Description
***
The security team has found a rather strange file exiting the network, we're not sure if it's containing any sensitive information. Help us identify what's in it.

Questions
***
File carving, my least favorite thing to do. But alas, lets get going.

There are two ways that I do file carving, although one is more tedious than the other. Sometimes the first method will fail though, and we must resort to the second option. I will run through both in case you encounter a puzzle that serves to be more difficult than it needs to be.

### Binwalk
Whenever I am doing forensics related to corrupt or hidden files, I will run binwalk on the file to see what it can find. 

```sh
┌──(kali㉿kali)-[~/Downloads]
└─$ binwalk green_file   

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             --- image, 63 x 36, 8-bit/color RGBA, non-interlaced
3243          0xCAB           gzip compressed data, from Unix, last modified: 2017-02-14 05:32:27
3605          0xE15           --- image, 24 x 24, 8-bit/color RGBA, non-interlaced
3818          0xEEA           --- image, 24 x 24, 8-bit/color RGBA, non-interlaced
4040          0xFC8           --- image, 24 x 24, 8-bit/color RGBA, non-interlaced
4264          0x10A8          --- image, 24 x 24, 8-bit/color RGBA, non-interlaced
```
(Note: Censored some output to prevent revealing flags)

Well, that was pretty easy

Q1
This file initially looks like something green, what's the file format of this green file?

From the binwalk output, we can see what our file type is based on the images in it.

Q2
How many files can be extracted from the binary blob?

We can count the number of files we can extract from this to get our answer.

Q3
What is the hidden flag in the file?

Now the fun part, picking out the goodies from the trash. By looking at binwalk's man pages, there are some options if we want to get individual files. 

```sh
...
-D, --dd=<type[:ext[:cmd]]>
              Extract <type> signatures (regular expression), give the files an extension of <ext>, and execute <cmd>
...
```

Lets build our binwalk command
`binwalk green_file --dd=gzip`

That will give us our file to extract and get our flag from.

### HxD
(Note: You can use any hex editor you want. I use HxD because its lightweight and pairs well with Autopsy, something we'll get into in a later challenge)

Sometimes, Binwalk cant identify anything helpful, either due to corrupt headers or misplaced files. We must then get our hands dirty and carve our files out by hand by looking at the hex.

HxD is a simplistic Hex editor, and it can help with carving files as you can extract the hex, stick it in a new binary, and use that as the file. File Carving at its finest!

Lets open our file up HxD
![[File Carving-HxD.png]]

Looks like a lot, but thankfully, all our PNG file headers will show up in ASCII, so that makes counting them easy.

The hard part is pulling out the file we need. We first need to isolate what the file could be. Since it is directly after a known footer (PNG footer is `49 45 4e 44 ae 42 60 82`), we can look up the file header of the next file. In our case, our mystery header is `1F 8B 08 00 6B ...`. After a quick google search of these bytes, the `1F 8B` denotes a gzip file. Now we just grab all the bytes up to the next PNG header (denoted by 89 50 4E ...):
![[File Carving - carving.png]]
Then we can copy these bytes into another HxD instance, and create our file `Carve.gz` (as it is a gz file) and extract it with your extractor of choice (I use WinRAR, but use what you want)