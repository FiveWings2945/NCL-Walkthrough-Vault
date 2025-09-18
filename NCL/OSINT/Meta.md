Created: 2025-09-18

Challenge Type: #OSINT
Challenge Difficulty: #Easy
Attachments: [[Meta.jpg]]

Meta
Description
***
Test your abilities to extract metadata.

Questions
***
Just based on the description, we will be looking at the metadata of an image. You can use a variety of tools, such as [cyberchef.com](https://gchq.github.io/CyberChef) and Exiftool. I prefer Exiftool, since it will give me a much more detailed readout of the image's metadata, but to keep it simple, we will use cyberchef for this walkthrough.
#### Q1
When was the image created? Round down to the nearest minute

Using [cyberchef.com](https://gchq.github.io/CyberChef) Extract EXIF recipe (Multimedia --> Extract EXIF), we can pull up the image EXIF data of the image. This question's answer is under CreateDate
![[OSINT-Meta.png]]
#### Q2
What are the dimensions of the image? (ex: 800x600)

We can get this answer this by using this formula: (*XResolution* x *yResolution*)
#### Q3
What is the make of the camera that took the picture?

This answer will be under Make
#### Q4 
What is the model of the camera that took the picture?

This answer will be under Model
#### Q5
What is the exposure time for the picture? (ex: 1/200)

This one is a little bit different. Exiftool will give us a neat fraction like the answer wants, but cyberchef will give us a decimal. To fix this, I went to a decimal --> fraction converter online and created my fraction to get the answer
#### Q6
What are the GPS coordinates where the was the picture taken? (Any standard format is acceptable)

For this you will need to combine both the GPSLatitude and GPS Longitude for your answer. 
*Note: Sometimes a question will ask for a specific format for the coordinates to be in. If your answer is not in the format being asked, check online for a converter to get it in an acceptable format*