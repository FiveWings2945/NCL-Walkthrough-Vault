Created: 2025-09-18

Challenge Type: #OSINT 
Challenge Difficulty: #Easy
Attachments: None

Lookup
Description
***
Answer these questions about DNS. **Make sure you enter the record type and not the description of the record type.**

Questions
***
There are multiple ways that you can look up DNS records and information. Since the challenges seem to be simple questions about DNS, we can simply just google these answers.

Q1
What type of DNS record holds the DNSSEC public signing key?
- This DNS record is incredibly important for verifying signed DNS data.
- It holds the public signing key used to check the digital signatures in RRSIG records

Q2
What type of DNS record is used to map hostnames to IPv6 addresses?
- There are two different DNS records that map hostnames to IP addresses
- These records are responsible for allowing you to look up the answers to these questions in the first place!

Q3
What type of DNS record is used to delegate a DNS zone?
- This record sets up a path of delegation between domains and subdomains
- Allows for child subdomains to point to a parent domain