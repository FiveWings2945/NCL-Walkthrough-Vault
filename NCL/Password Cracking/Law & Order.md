Created: 2025-09-22

Challenge Type: #Password
Challenge Difficulty: #Hard
Attachments: None

Law & Order
Description
***
Our analysts have obtained password dumps storing hacker passwords. It appears that they are based off of Law and Order: SVU episodes and end in 2 digits.

Questions
***
First step is to examine the description and the Title. The description says that the passwords are:
- Based on Law and Order: Special Victim Units Episodes
- End in 2 digits.

Unfortunately, chat gpt couldnt help me get the list due to length and copyright issues, so instead I went to[ this wiki page](https://en.wikipedia.org/wiki/List_of_Law_&_Order:_Special_Victims_Unit_episodes_(seasons_1%E2%80%9319)) to get every available episode. I then fed the output to a python script that would remove the excess and output the episode list. Just in case, I also added some lines to take each individual word and create separate entries for the episodes.
```
import re

def process_titles(input_file, output_file):
    with open(input_file, "r", encoding="utf-8") as infile, open(output_file, "w", encoding="utf-8") as outfile:
        for line in infile:
            # Extract title inside quotes
            match = re.search(r'"(.*?)"', line)
            if match:
                title = match.group(1)

                # Title versions
                title_capitalized = title
                title_lower = title.lower()

                # Split words
                words_capitalized = "\n".join(title.split())
                words_lower = "\n".join(title_lower.split())

                # Write output
                outfile.write(f"{title_capitalized}\n")
                outfile.write(f"{title_lower}\n")
                outfile.write(f"{words_capitalized}\n")
                outfile.write(f"{words_lower}\n\n")  # blank line between episodes


# Example usage
process_titles("episodes.txt", "output.txt")

```
This script takes a line like
`2 2 "A Single Life" Lesli Linka Glatter Miriam Kazdin September 27, 1999 E0903 13.06[13]`
And will turn it into
```
A Single Life 
a single life 
A 
Single 
Life 
a 
single 
life
```

(Note: There are ways to capitalize certain letters in a wordlist, but for simplicity's sake, I made the python do it for me)
(Note2: When generating a wordlist, you want to make sure you cover your bases. For example, maybe some passwords use the full episode title, while other passwords only use a single word from the episode title)

Once I have that wordlist, I then create my hashcat command
`-m 0`: hashmode 0 - md5 hash (looks like a md5 hash, but a quick check with hashcat will confirm this)
`-a 6`: attack mode - hybrid wordlist + mask attack 
`hashes.txt`: hash file
`LawNOrder.txt`: wordlist file
`'?d?d'`: mask
`--show`: show decrypted hashes

| User   | Hashes                           | Hash Type? |
| ------ | -------------------------------- | ---------- |
| Zoe    | 6475c851b56004eb96ab1404252c3a34 | md5        |
| Nan    | abe6591e06aafc3cf1b0783b120f685e | md5        |
| Ade    | 1e1612db8bdeebc7e8d56f8f30b39456 | md5        |
| Lena   | 3dd9dd0e352df4433aadf2273e269287 | md5        |
| Rachel | 08038f679de74982bfb9bac43d46271a | md5        |