****

# OhSINT

![alt text](https://i.imgur.com/Gwd93aS.png)

**Source:** Created by tryhackme (ben) on TryHackMe

***Description:***

​	Are you able to use open source intelligence to solve this challenge?

***Related Hosting Links***

- TryHackMe
  - Hosted as a free room at the time of writing!
  - Link: https://tryhackme.com/room/ohsint

***Special Notes:***

​	Be sure to try various combinations of searching with the information you find, the results will vary heavily as you try more and more. 



***Instructions:*** 

- As we begin to conquer this room, we are greeted by the following image
  - ![alt text](https://i.imgur.com/EGk5v7K.jpg)
- At first glance, this simple appears to be the Windows XP iconic default background. Let's go ahead and see what properties it has by running exiftool on it. Exiftool (https://en.wikipedia.org/wiki/ExifTool) is an common first step within steganography challenges, however, in this instance it allows us to view metadata about the photo.
  - ![alt text](https://i.imgur.com/NaeWtHV.png)
- Interesting, it appears to be attributed to someone named "OWoodflint", let's try just googling that name
  - ![alt text](https://i.imgur.com/VIav4JR.png)
- Look's like we have two interesting hits, a blog and a twitter profile. Let's peek at the blog
  - ![alt text](https://i.imgur.com/9XZDX3w.png)
- Seem's fairly empty, let's check out the source code. Considered to be incredibly poor coding practice, some web designers will hide information for their own usage within comments on the source code. 
  - ![alt text](https://i.imgur.com/Xehh8p6.png)
- Bingo! Yeah, that's not a great place to store your password! We'll check the rest of the site, look's like he's traveling at the moment but I'm not seeing anything else here. Let's pivot to his twitter page
  - ![alt text](https://i.imgur.com/uDChtv5.png)
- A strange thing to tweet but interesting none the less, looks like he's tweeted a BSSID for a wifi point near where he lives. We'll check wigle.com, a site where war-drivers can share observed access points, to see if there's a chance that a wardriver has also spotted this access point. If you would like to learn about about wigle, check out their website to see if your wifi router has been marked and play around from there.
  - ![alt text](https://i.imgur.com/vI5C0L3.png)
  - ![alt text](https://i.imgur.com/TyOKXSl.png)
- Looks like we're in luck! (If you have any difficulties with this, zoom far out and you'll see a purple icon appear.)  Hmm, let's see if we can find any other profiles associated with him. Let's see if he's submitted anything to github.
  - *To provide some context to this pivot, it is fairly common to check all social media platforms (i.e. twitter, facebook, etc.) to find any profiles. In this case and given the technical nature of the individual we are performing recon on, we can assume with a fair amount of confidence that they have a github profile.*
  - ![alt text](https://i.imgur.com/6RS4deH.png)
- Sure enough, there's his profile
  - ![alt text](https://i.imgur.com/O1JYega.png)
- Creepy, right? Be careful what you post online!







***Flags:***

- Twitter
  - <https://twitter.com/OWoodflint>
- GitHub
  - <https://github.com/OWoodfl1nt>
- WordPress
  - <https://oliverwoodflint.wordpress.com/>
