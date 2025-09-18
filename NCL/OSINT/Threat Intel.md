Created: 2025-09-18

Challenge Type: #OSINT 
Challenge Difficulty: #Easy 
Attachments: None

Threat Intel
Description
***
Answer the following questions about security issues.

Questions
***
Most of these can be solved through just googling the answers, or by using threat intelligence databases like [MITRE ATT&CK](https://attack.mitre.org/) and SearchSploit. I include notes below each question to add some extra information about each answer (open source research is important in IDR environments like a SOC team).

Q1
What is the CVE of the original POODLE attack?
- Stand for Padding Oracle on Downgraded Legacy Encryption
- The attacker can capture SSL 3.0 packets and decrypt them easily assuming the sender can send them multiple times

Q2
What version of VSFTPD contained the smiley face backdoor?
- CVE-2011-2523
- This version contained a backdoor that will create a reverse shell

Q3
What was the first 1.0.1 version of OpenSSL that was NOT vulnerable to heartbleed?
- CVE-2014-0160
- Involved a buffer overflow attack that was a result of improper input validation

Q4
What was the original RFC number that described Telnet?
- Published in May 1983.
- Established the standard for Telnet

Q5
How large (in bytes) was the SQL Slammer worm?
- CVE-2002-0649
- A buffer overflow attack that allowed attackers RCE
- So small it could fit in a single packet

Q6
Complete the sentence: "Samy is my..."
- Exploited a XSS vulnerability
- Notably named the "Samy" worm, it allowed itself to propagate through hidden javascript in a user's description