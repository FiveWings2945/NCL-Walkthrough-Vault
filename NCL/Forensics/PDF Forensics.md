Created: 2025-09-25

Challenge Type: #Forensics
Challenge Difficulty: #Easy
Attachments: api.pdf

PDF Forensics
Description
***
Our analysts managed to get hold of a document that we believe has a flag on it. Can you recover it?

Questions
***
Looks like we got a redacted pdf here. Its hard to get much information from looking at it, so lets look at a few things.

First thing I will run is a binwalk scan, in case there are any hiding files here:
```sh
┌──(kali㉿kali)-[~/Downloads]
└─$ binwalk api.pdf      

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PDF document, version: "1.7"
374335        0x5B63F         Zlib compressed data, default compression
376580        0x5BF04         Zlib compressed data, default compression
376896        0x5C040         Zlib compressed data, default compression
377111        0x5C117         Zlib compressed data, default compression
377328        0x5C1F0         Zlib compressed data, default compression
377548        0x5C2CC         Zlib compressed data, default compression
377766        0x5C3A6         Zlib compressed data, default compression
377999        0x5C48F         Zlib compressed data, default compression
378219        0x5C56B         Zlib compressed data, default compression
378467        0x5C663         Zlib compressed data, default compression
378686        0x5C73E         Zlib compressed data, default compression
378907        0x5C81B         Zlib compressed data, default compression
379133        0x5C8FD         Zlib compressed data, default compression
379409        0x5CA11         Zlib compressed data, default compression
379627        0x5CAEB         Zlib compressed data, default compression
379867        0x5CBDB         Zlib compressed data, default compression
380106        0x5CCCA         Zlib compressed data, default compression
380325        0x5CDA5         Zlib compressed data, default compression
380541        0x5CE7D         Zlib compressed data, default compression
380696        0x5CF18         Zlib compressed data, default compression
380840        0x5CFA8         Zlib compressed data, default compression
383897        0x5DB99         Zlib compressed data, default compression
```

Woah, thats a lot of data. Before we dive into that, lets check out our file metadata as well. Maybe it can tell us whats going on with all this extra data. I will use exiftool for this, but you can use your favorite online metadata viewer too
[[PDF Forensics - exiftool output]]

(I had to add it in a separate note because the output was quite long)

Just a quick glance at our metadata shows a large amount of very helpful information.

Q1
What is the name of the program that exported this PDF file?

Our metadata will answer this for us. We can look to the field `Creator Tool`

Q2
What PDF version is this file?

We can answer that with our binwalk or metadata output. 

Q3
What software was used to redact the file and insert a watermark?

For this one, we have to go in and remove a few of our black boxes. I will use Libreoffice Draw since its free and will offer fairly simple editing. All we have to do is open up our file in Draw, drag away our boxes, and voilà, we can see the watermark.

Q4
You can either continue with the black box in Libreoffice, or you can inspect the metadata one last time. Its in there plain as day.