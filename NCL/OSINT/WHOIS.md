Created: 2025-09-18

Challenge Type: #OSINT
Challenge Difficulty: #Easy
Attachments: None

WHOIS
Description
***
Conduct open source intelligence data collection about **cityinthe.cloud**. Answer the following questions as they relate to the **cityinthe.cloud** domain.

Questions
***
You could use an online service to complete these challenges, but for demonstration, I will be using the `whois` command on linux. This is our command

`whois cityinthe.cloud`

I will also use grep to filter for certain fields

`whois cityinthe.cloud | grep '[FIELD]'`

Q1
Who is the registrar of this domain?

Found under the `Registrar` field

Q2 
On what day was this domain first registered?

Found under the `Creation Date` field

Q3 
What is this domain's registry domain ID?

Found under the `Registry Domain ID` field

Q4 
What is the Top-Level Domain (TLD) of this domain?

This is the suffix found after the domain name

Q5 
What organization manages the TLD used by cityinthe.cloud?

This is found by running a whois command on the TLD itself and using grep for `organisation` (That spelling). Will be the first option that appears