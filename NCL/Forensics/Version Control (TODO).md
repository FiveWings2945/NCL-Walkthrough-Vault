Created: 2025-09-25

Challenge Type: #Forensics
Challenge Difficulty: #Easy
Attachments: git_backup.zip

Version Control
Description
***
One of our employee's computer was compromised and we saw this backup file leave the network, but we couldn't find anything other than a simple README.md file in it. Help us found out what information the hackers got.

Questions
***
Based on the title, we will be working with Git. There is the command line option, but thankfully GitHub has a GUI for working with git repositories ([GitHub Desktop](https://desktop.github.com/download/)). For the sake of demonstration, I will work through both.
### GUI
We can open our repository in this GUI environment and start exploring.
![[VC-Github Desktop.png]]

Q1
What is the email address of the employee who was compromised?

We can assume that the employee is the one who owns this repository. For this we will examine the actual contents of the .git folder we imported. 

One file that will always pique my interest when looking for things related to forensics will be `logs`. And it turns out my hunch is right. By check in `logs→HEAD`, we will find an email that is the one we are looking for.
(Note, hang onto this file. Itll be helpful later on)

Q2
Each employee is assigned a flag. What is the flag that was compromised?

Here we can go back to Github Desktop, and check the history tab. This will show us the history of changes in available branches. When we see the files that have been changed, FLAG.txt looks interesting

![[VC-FLAG.txt.png]]

Q3
Greg thinks that he may have had additional account credentials that were compromised. What's the name of the service provider for that other compromised account?

If we go back to our `log/HEAD` file, we will see an interesting commit:
`commit: Backup passwords`
Maybe theres a password file somewhere here too. However, looking at history, we dont see any mention of a password file. If we go one line up in our log file though, we see this line
`checkout: moving from master to next`
Interesting. This repository has multiple branches. A branch is essentially a sub-directory of a repository. If we go back to GitHub Desktop and change our branch, we can see if our file is here.

![[VC-Next Branch.png]]

Bingo! Theres our service, and a password too.

Q4
What was the password on that compromised account?

See the file above

### CMD (TODO)