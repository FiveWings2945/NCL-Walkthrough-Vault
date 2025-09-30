Created: 2025-09-29

Challenge Type: #Log_Analysis 
Challenge Difficulty: #Medium
Attachments: browser.sqlite

History
Description
***
Analyze a Firefox sqlite history database and answer questions about what happened. It you are not familiar with SQL you may want to learn more about SQL here: [https://www.tutorialrepublic.com/sql-tutorial/](https://www.tutorialrepublic.com/sql-tutorial/)

Questions
***
For this challenge, you can use either a command-line interface to access the SQL tables, or you can use a database viewer. I personally am still working on learning SQL so I used this [database viewer](https://sqlitebrowser.org/). You can download it on Windows, Mac, and most Linux distros. I personally use Kali for NCL, so in my case, the command was
`sudo apt install sqlitebrowser`

We can then open our database file in this browser. (Note: This challenge will involve no scripting. Just point and click until we grab our answer)

Here's what our view looks like
![[History-DBViewer.png]]

What we will want to do is inspect individual entries of the available tables, so we can go and enter the `browse data` tab near the top. Then the table that will most likely be the most interest to us will be the `moz_places` table.
![[History-moz_places.png]]
Q1
What did the user search for on craigslist?
Q2
What was the current price of bitcoin when the user was browsing?
Q3 
What Bitcoin exchange did the user log in to?
Q4
What is the email that was used to log into the exchange?
Q5 
What was the ID of the Bitcoin transaction that the user looked at?
Q6
What was the total BTC of all the inputs of the Bitcoin transaction?
Q7 
Which bitcoin address received the majority of the Bitcoin in the transaction?