Created: 2025-09-18

Challenge Type: #Cryptography
Challenge Difficulty: #Easy
Attachments: [[Strings.jpg]]

Strings
Description
***
The hackers have hidden a message in this image. Find out what it is.

Questions
***
This challenge is based on the term Steganography. An attacker can hide words or interesting data in an image file without you even knowing. A very common way to do this is through LSB encryption. However, just by looking at the image we are given, it looks to corrupt after a certain pixel. This is a tell-tale sign the picture was edited directly, not subtly changed through LSB encryption.

The first thing when inspecting a steganography challenge is to look at the hexdump of the image itself. We can do this through a variety of tools, both online and console. The tool I use in Linux is `xxd`, but for a more visual online tool, I will be using [Hexed.it](https://hexed.it/). I will go over both quickly in this guide

#### Hexed.it
First, lets import the image into Hexedit to get the hexadecimal of the image itself. 
![[Crypto- Strings.png]]
Once there, we know that our flag format is SKY-@@@@-####, so Ill search for those bytes in the image using the search function. Once I do that, I find that those bits have indeed been edited and the flag is right there in plain sight.

#### xxd
To get a hexdump of a file, we use:
`xxd string.jpg > hexdump.txt`

This will display an unfiltered hexdump to a file hexdump.txt. We then can either search for the string in the text editor, or we can simply filter the output using `grep`

`xxd strings.jpg | grep "SKY"`

This will output the line that contains the flag. If you want to get even more granular, you can filter it further by using regex for the pattern to get the whole flag.

`xxd strings.jpg | grep -E "SKY-[A-Z]{4}-[0-9]{4}"`