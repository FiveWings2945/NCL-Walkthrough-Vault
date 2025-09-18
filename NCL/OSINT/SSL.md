Created: 2025-09-18

Challenge Type: #OSINT
Challenge Difficulty: #Medium
Attachments: None

SSL
Description
***
Solve the following questions about the Cyber Skyline SSL certificate.  
  
_Note: if you see references to "BitDefender" in the process of solving this challenge, that means your BitDefender software is intercepting your SSL/TLS connection and will produce incorrect results._

Questions
***
SSL information on a website can be found just by checking in your web browser. Whenever you see a Lock Icon by the website address, there is a good chance that website has a valid SSL certificate/key.

To get the information you need, open your favorite web browser and check out the URL [cyberskyline.com](https://cyberskyline.com). Then you need to look for the certificates of that site, usually denoted by a lock symbol near the search bar.
![[OSINT-SSL.png]]
Q1 
Who is the issuer for Cyber Skyline's SSL certificate?

Inside of the certificate details that you pull up, you see a handful of information. The fields you are looking for is the *Issued By* field.

Q2
How many bits long is the SSL key?

The SSL key is a SHA-256 key, which uses 256 bytes of hexadecimal characters to create a key. Now all you have to do is multiply using this equation: $1\ byte = 8 bits/byte$ to get the number of bits in the key.

Q3
How many certificates are in the certificate chain?

This can be viewed by looking at details and checking out the Certificate Hierarchy. The number of certificates that show up in that hierarchy is the answer. 