Created: 2025-09-26

Challenge Type: #Log_Analysis
Challenge Difficulty: #Easy
Attachments: Auth.log

SSH
Description
***
Analyze this ssh log file to answer the following questions.

Questions
***
Whenever doing log analysis, I like to solve it by scripting each individual question. It makes scripting for specific values easier.

However, this log is fairly short and easy to read, so Ill just look over the log quickly and answer questions. (If your interested in log scripting, check out some of the later challenges)

Q1
What is the hostname of the ssh server that was compromised?

This one is easy. We just look at the first line of the log to find our hostname.

Q2 + Q3 + Q4

What was the first, second, and third IPs to attack the server?

This one is also easy. We can just look at the log again and find the first three unique IP addresses.

Q5
Which user was targeted in the attack?

Whichever user is trying to be logged into.

Q6
From which IP address was the attacker able to successfully log in?

You can grep the log to find `Accepted` (or just look at the end of the log...)