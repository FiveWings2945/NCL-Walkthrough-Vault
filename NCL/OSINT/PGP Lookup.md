Created: 2025-09-18

Challenge Type: #OSINT
Challenge Difficulty: #Easy
Attachments: None

PGP Lookup
Description
***
Individuals use PGP to securely encrypt their emails, can you find out more about the following PGP keys?

Questions
***
I will be using [this website](https://keyserver.ubuntu.com/pks/lookup?search=7A39A56B73D1E097D57435CFCDE2DE1DCB2077F2&fingerprint=on&op=index) to complete these challenges. 

Q1 
What is the key fingerprint for security@cpanel.net?

We can enter that email directly into our search bar and get our fingerprint. When you enter the email, you will get two results: Master key and the key related to the security team. You do need to take the security team print.

Q2 
What email address is associated with the key fingerprint `7A39A56B73D1E097D57435CFCDE2DE1DCB2077F2`?

We can enter this fingerprint into our website and get the answer immediately.

Q3
On what date does the above key expire (in UTC)?

This will be in the same output. Look for a date that has not occurred yet.