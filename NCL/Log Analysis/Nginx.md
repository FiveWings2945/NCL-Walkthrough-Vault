Created: 2025-09-26

Challenge Type: #Log_Analysis
Challenge Difficulty: #Medium
Attachments: access.log

Nginx
Description
***
Analyze a nginx access log and answer questions about what happened.

Questions
***
Whenever doing log analysis, I like to solve it by scripting each individual question. It makes scripting for specific values easier.

For reference, this is what one line from the file looks like
`91.196.50.33 - - [29/Sep/2015:21:22:48 -0400] "GET http://testp3.pospr.waw.pl/testproxy.php HTTP/1.1" 404 136 "-" "Mozilla/5.0 (Windows NT 5.1; rv:32.0) Gecko/20100101 Firefox/31.0"`

Q1
How many different IP addresses reached the server?

IP addresses can follow this format
`###.###.###.###`
so we can add some regex to dynamically grab each IP in the line. To check how many unique IP's we have, we add some comparison logic and add unique IP's to a list.

Our Regex will be

`\b\d{1,3}(?:\.\d{1,3}){3}\b`

`\b` : Ensure no partial matches 
`\d{1,3}` : 1-3 digits
`(?:\.\d{1,3})` : `.` followed by 1-3 digits
`{3}` : do the above 3 times

And our python will be:
```python
import re

ips = []
pattern = re.compile(r"\b\d{1,3}(?:\.\d{1,3}){3}\b")

with open("access.log", "r") as file:
	for line in file:
		
		#Grab the first match
		matches = pattern.search(line)
		if matches:
			unique = True
			
			#Prevent Duplicates
			for ip in ips:
				if matches.group() == ip:					
					unique = False
			if unique:
				ips.append(matches.group())

print("Num IP's: ", len(ips))
```

Q2 + Q3
How many requests yielded a 200 and 400 status?

So we need to just grab the status code from the log. Just by looking at the log, we see the status code comes after the Request, which is surrounded in quotes. So lets grab the 3 numbers that show up after the second quotation.

Heres our regex
`^(?:[^"]*"){2}[^0-9]*?(\d{3})`

`(?:[^"]*")`: skip everything up to a quote
`[^0-9]`: only get digits
`*?(\d{3})`: Get the first 3 digits

Lets update our python

```python
import re

ips = []
status200 = 0
status400 = 0
ipP = re.compile(r'\b\d{1,3}(?:\.\d{1,3}){3}\b')
statusP = re.compile(r'^(?:[^"]*"){2}[^0-9]*?(\d{3})')

with open("access.log", "r") as file:
	for line in file:
		#IP
		#Grab the first IP match
		matchesIP = ipP.search(line)
		if matchesIP:
			unique = True
			
			#Prevent Duplicates
			for ip in ips:
				if matchesIP.group() == ip:					
					unique = False
			if unique:
				ips.append(matchesIP.group())
		
		#Status Codes
		#Grab the status code
		matchesS = statusP.search(line)
		if matchesS:
			status = matchesS.group(1) 
			print(status)
			if status == "200":
				status200 += 1
			elif status == "400":
				status400 += 1
			

print("Num IP's: ", len(ips))
print("Num 200 Status: ", status200)
print("Num 400 Status: ", status400)

```

Q4
What IP address rang at the doorbell?

This one is pretty easy. All we have to do is filter for the word `doorbell` in our line and grab the IP for that line.

Lets add that to our loop line:

```python
			...
			if status == "200":
				status200 += 1
			elif status == "400":
				status400 += 1
				
		if "bell" in line.lower():
			print(matchesIP.group(), "rang the doorbell")
		
		...
```
(Note: I had it compare to `bell` because the doorbell is misspelled in the log. You could find this out by running `cat access.log | grep "bell"`)

Q5
What version of the Googlebot visited the website?

Also easy. Instead of trying to use regex to extrapolate the exact version, we can just pull the line a read it ourselves
```python
		...
		if "google" in line.lower():
			print("Googlebot:", line)
		...
```


Q6
Which IP address attempted to exploit the shellshock vulnerability?

This vulnerability is CVE-2014-6271. This allowed attackers to execute arbitrary commands on a remote system through carefully crafted commands. Since this is a webserver, we can probably assume the attacker tried to use the vulnerability through the URL, which we can search for. This can be solved similar to Q4. Here we can search for keywords like `/bin/bash` or `shell` or `sh`

```python
		...
		if "/bin/bash" in line.lower() or "shell" in line.lower():
			print("Shellshock IP:", matchesIP.group())
		...
```

Q7
What was the most popular version of Firefox used for browsing the website?

Looking back at our Log line
`91.196.50.33 - - [29/Sep/2015:21:22:48 -0400] "GET http://testp3.pospr.waw.pl/testproxy.php HTTP/1.1" 404 136 "-" "Mozilla/5.0 (Windows NT 5.1; rv:32.0) Gecko/20100101 Firefox/31.0"`

We see that the version is the last digits of the line. So we can build some regex for that
`(\d{2}\.\d)"$`

`(\d{2}\.\d)`: Matches our version number
`"$`: Matches the quote at the end and will anchor our regex to the end of the line.

Lets update our python
```python
	versions = {}
...
	versionP = re.compile(r'(\d{2}\.\d)"$')
...
		
		matchesV = versionP.search(line)
		if matchesV:
			version = matchesV.group(1)
			if version in versions:
				versions[version] += 1
			else:
				versions[version] = 1
...

print(versions)
```

Q8 + Q9
What is the most and second most common HTTP method used?

Going back to our sample line:
`91.196.50.33 - - [29/Sep/2015:21:22:48 -0400] "GET http://testp3.pospr.waw.pl/testproxy.php HTTP/1.1" 404 136 "-" "Mozilla/5.0 (Windows NT 5.1; rv:32.0) Gecko/20100101 Firefox/31.0"`

We see it comes directly after our date. This makes this easy. Since our date is enclosed in brackets, we can simply use regex to snag just that
`.*\[.+?\]\s"([A-Z]{3})`
`.*`: Skip everything to the first bracket
`\[.+?\]`: Match our date
		- `.+`: will match 1 or more of any character
		- `?\]`: Will only match up to the first bracket
`\s"`: Match the space and quote before the request
`([A-Z]{3})`: Match our request (group 1)
		- `[A-Z]`: Match a uppercase letter
		- `{3}`: Do it 3 times
		  
Now that we have that, lets update our python to print out the occurrence of different requests

```python
requests = {}
requestP = re.compile(r'.*\[.+?\]\s"([A-Z]{3})')
...
#with open ...
	#for line in file
		...
		matchesR = requestP.search(line)
		if matchesR:
			request = matchesR.group(1)
			if request in requests:
				requests[request] += 1
			else:
				requests[request] = 1
		...
print(requests)

```

Q10 - 10 points

How many requests were for \x04\x01\x00P\xC6\xCE\x0Eu0\x00?

Well this one is pretty simple. We just add a counter variable, and if the request has this in it, increment the counter

```python
			...
			if '\\x04\\x01\\x00P\\xC6\\xCE\\x0Eu0\\x00' in line:
				specificRequests += 1
			...
print("Requests for \x04\x01\x00P\xC6\xCE\x0Eu0\x00:", specificRequests)
```
(Note: You probably also tried using grep to get the answer, but it didnt return. The reason is because `\x04`, as an example, is actually unicode and will be interpreted as such. Therefore, you must escape the unicode using another backslash for the program to register the string as itself.)


Sweet, with that out of the way, we have our fully compiled Python script to analyze this log. I wont attach it here for people who want to go through and build it themselves, but if you want to check yours against a working script, I linked it [[Nginx Python Script|here]].
