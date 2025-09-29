```python
import re

ips = []
status200 = 0
status400 = 0
versions = {}
requests = {}
specificRequests = 0

ipP = re.compile(r'\b\d{1,3}(?:\.\d{1,3}){3}\b')
statusP = re.compile(r'^(?:[^"]*"){2}[^0-9]*?(\d{3})')
versionP = re.compile(r'(\d{2}\.\d)"$')
requestP = re.compile(r'.*\[.+?\]\s"([A-Z]{3})')

with open("Downloads/access.log", "r") as file:
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
			#print(status)
			if status == "200":
				status200 += 1
			elif status == "400":
				status400 += 1
		
		#Look for the doorbel ringer		
		if "bell" in line.lower():
			print(matchesIP.group(), "rang the doorbell")
		
		#Look for the google bot
		if "google" in line.lower():
			print("Googlebot:", line)
		
		#Look for shell shock
		if "/bin/bash" in line.lower():
			print("Shellshock IP:", matchesIP.group())
		
		#Look for a log firefox versions
		matchesV = versionP.search(line)
		if matchesV:
			version = matchesV.group(1)
			if version in versions:
				versions[version] += 1
			else:
				versions[version] = 1
		
		#Look for and log Request types
		matchesR = requestP.search(line)
		if matchesR:
			request = matchesR.group(1)
			if request in requests:
				requests[request] += 1
			else:
				requests[request] = 1
		
		#Look for our specific request		
		if "\\x04\\x01\\x00P\\xC6\\xCE\\x0Eu0\\x00" in line:
				specificRequests += 1
			

#Print our results
print("Num IP's: ", len(ips))
print("Num 200 Status: ", status200)
print("Num 400 Status: ", status400)
print("Versions:", versions)
print("Requests:", requests)
print("Requests for \\x04\\x01\\x00P\\xC6\\xCE\\x0Eu0\\x00:", specificRequests)
```