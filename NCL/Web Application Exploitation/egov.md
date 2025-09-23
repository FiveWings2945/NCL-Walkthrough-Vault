Created: 2025-09-23

Challenge Type: #Web_App_Exploitation
Challenge Difficulty: #Easy
Attachments: Website path

egov
Description
***
Conduct a security audit on the [egov login panel](https://0d135339f0ee66818b58f73265b01639-egov.web.cityinthe.cloud/).  
  
**Note: Your scope is limited to HTTPS. You may use automated tools that make educated guesses for this challenge, blind automated brute force is not permitted.**

Questions
***
First lets boot up Burpsuite and take a look at our website through our [[Proxy]]. It looks like all we are given is an admin page, and the [[Target]] module does not provide any other resources for us to look at.
![[Egov-Website.png]]
We could start with SQL injection, but since it is an easy challenge, maybe it is a little easier than that. We can flip on the intercept mode on our proxy and just try to login with default credentials `admin:admin`
![[Egov-Burpsuite1.png]]
We can then right click the request in the view window, select `Do Intercept → Response to this Request`. This will intercept the response to the request we sent.
![[Egov-Burpsuite2.png]]

When we get our response, we see the website doing something quite interesting with the response.
![[Egov-Burpsuite3.png]]
We can see that the server is setting a cookie on our computer to make admin=false. Since its a plaintext cookie, we can go into our cache and check to see if editing this value will affect anything with the website. 

We can go into our proxy browser and inspect the site, opening up the browser inspector. This will open up a variety of options, but the one we are interested in is the `Application` tab in Burpsuite proxy, more commonly the `Storage` tab in most other browsers. This will contain information that your browser has cached about the website. In the proxy, you will open the Application tab, and in the menu on the left look for `Storage` then `Cookies`.  If we open this up, we will find the cookie that our browser has set. We can go ahead and set this cookie to `true` and see if refreshing our browser will do anything.
![[Egov-Burpsuite4.png]]

Refreshing didn't do anything helpful. Maybe we just have to try logging in again? We'll try `admin:admin`.
![[Egov-Cracked.png]]
And just like that, we're in.

Q1
What is the flag obtained from logging in?

Located under the text `New Flag` in the blue box