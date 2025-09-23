Created: 2025-09-19

Challenge Type: #Password
Challenge Difficulty: #Medium 
Attachments: None

Windows
Description
***
Our analysts have obtained Windows password dumps storing hacker passwords. Can you crack them?

Questions
***
First we analyze the description and the title. From the description it looks like we will be working with Windows NTLM hashes. These are usually crackable through rainbow tables. I used two different methods to crack these, which I will go over, but I will highly recommend pursuing the second option if you encounter these in the field as it is much quicker and less resource intensive.

#### [Hashes.com](https://hashes.com/en/decrypt/hash)
Hashes.com cracks a large amount of different hashes through a database of pre-cracked hashes. Now, this database is **MASSIVE** so I would recommend checking this database before pursuing another cracking method.

To crack, all you have to do is paste the hashes into the box and run the lookup.
![[Hashes.com Windows.png]]

Note: This one is a little tricky as the hashes you see may not be the first part of the hash in the challenge. Note how they are divided by a colon in the challenge. This is because some of the cracked hashes are LM hashes, and some are cracked NTLM hashes.

#### Ophcrack
Ophcrack is a free windows cracking software that can run on any machine. It works by running each of the hashes through a rainbow table and tries to crack both the LM and NTLM hashes. 

First, we store each of the hashes in a hashes.txt file. Then we download a rainbowtable of common Windows passwords and hashes. [This is the one that I used.](https://ophcrack.sourceforge.io/tables.php) Once you have done that, you run ophcrack. Youll be greeted by this GUI
![[Ophcrack.png]]
Section 1: Loaded Hashes
Section 2: Loaded tables

As you can see, I have loaded the XP Free tables. (Note: You may have to configure Ophcrack to use the imported tables. Go into the tables tab and in the popup, make sure your table is enabled. If it isnt, the software wont run your table!)

Once I load the hashes using `Load → PWDump File`, I can go ahead and hit 'Crack' and let it run. Eventually, you will get a list of the cracked hashes that ophcrack was able to get. If you dont get all the passwords, you may need to load more than one rainbow table
![[Ophcrack Cracked.png]]

| Name    | Hash                                                              | Hash Type? |
| ------- | ----------------------------------------------------------------- | ---------- |
| Jenny   | 21259DD63B980471AAD3B435B51404EE:1E43E37B818AB5EDB066EB58CCDC1823 | NTLM       |
| Nan     | 11CB3F697332AE4C4A3B108F3FA6CB6D:13B29964CC2480B4EF454C59562E675C | NTLM       |
| Justen  | 65711C079DC4CD3CC2265B23734E0DAC:47F747C5190DC0F0B921AA4A07F06285 | NTLM       |
| Patrick | FBBDA33FC12E83FB0C240E84A183686E:DDE9DC6E34E2E6E11EF9E51C6B27ED96 | NTLM       |
| Rachel  | 21C4E7C2EFE8E8D1C00B70065ED76AA7:A7A0F9AFD4A78F531A1CF4C42E531BBF | NTLM       |
| Ade     | E85B4B634711A266AAD3B435B51404EE:FD134459FE4D3A6DB4034C4E52403F16 | NTLM       |
| Kristy  | BA756FB317B622DBAAD3B435B51404EE:C8405270B10B13AE8A24612BB853567A | NTLM       |
| Lindsay | 199C926FA387EAB7AAD3B435B51404EE:F196F77BF8BB15781BA8364C649C5FD4 | NTLM       |
| Cassie  | FE4AACAAAD7D986AAAD3B435B51404EE:3928E16F614E2316CA51C336FA5B3011 | NTLM       |
| Zoe     | 3613F7EC15407F56AAD3B435B51404EE:C82E164316183AA3AF3EA6BAA642A237 | NTLM       |

