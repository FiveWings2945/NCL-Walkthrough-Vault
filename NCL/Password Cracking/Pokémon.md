Created: 2025-09-19

Challenge Type: #Password 
Challenge Difficulty: #Medium 
Attachments: None

Pokémon
Description
***
Our analysts have obtained password dumps storing hacker passwords. After obtaining a few plaintext passwords, it appears that they are based on Pokemon.

Questions
***
First we look at the description of the puzzle and the title. We can see that there have already been some plaintext passwords decrypted, and they all seem to be pokemon of some sort. In order to solve this puzzle, we will need to find a way to get a wordlist that consists of pokemon. Thankfully we can find a website that will generate a list of all the pokemon that are currently out (https://pokemondb.net/tools/text-list. All we do is generate a list with these parameters and we get a plaintext list of all the pokemon available.
![[Pokemon List Generator.png]]

Once we get our pokemon list (pokemon.txt), we can build our hashcat command:

`-m 0`: Hash-mode 0 - md5 hash
`-a 0`: Standard Attack mode (\[wordlist] Incremental ASCII)
`hashes.txt`: list of hashes
`pokemon.txt`: Our pokemon list
`--show`: Display the cracked hashes, or any uncracked passwords

When we run this in our terminal, we will get the cracked hashes.


| Name   | Hash                             | Hash Type? |
| ------ | -------------------------------- | ---------- |
| Elliot | a532443f3e04a9e00295a8cd2a75e080 | md5        |
| Justin | 54c10b9736b70e75c6e505f340b6e2f1 | md5        |
| Lena   | b8a24794813a47521b4be55747e0665a | md5        |
| Chris  | 83b020b0a7b3c353e1c11b1647b53cda | md5        |
| Ade    | 999cae1e22fe69d89d6f56e3050f18cb | md5        |

