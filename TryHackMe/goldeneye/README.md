****

# GoldenEye

![alt text](https://i.imgur.com/ECOSSjY.png)
![alt text]()

**Source:** Created by Creosote on Vulnhub, ported by ben to TryHackMe

***Description:***
	
​	Practise using tools such as dirbuster, hydra, nmap, nikto and metasploit

***Related Hosting Links***

- TryHackMe
  - Hosted as a subscriber only room at the time of writing.
  - Link: https://tryhackme.com/room/goldeneye
- VulnHub
  - Link: <https://www.vulnhub.com/entry/goldeneye-1,240/>

***Special Notes:***

​	



***Instructions:*** 

- As we start most boxes, let's begin with some scanning! For this, let's use nmap.
  - ![alt text](https://i.imgur.com/r0KrXDp.png)
  - ![alt text](https://i.imgur.com/tsn6A6G.png)
  - ![alt text](https://i.imgur.com/vmZPEoL.png)
- Looks like we have ports 25, 80, 55007, and 55006 open. Let's go ahead and check out that web server running on port 80
  - ![alt text](https://i.imgur.com/usZGDR5.png)
- And the source code? We'll go ahead and check out the JavaScript file mentioned in that. 
  - ![alt text](https://i.imgur.com/ht8YzFX.png)
- Well, looks like there's an ASCII encoded password for what we can assume the login page at /sev-home/. Let's go ahead and check out that login page
  - ![alt text](https://i.imgur.com/jzxKYty.png)
- There's our login! Let's go ahead and decrypt that ASCII text. For this, I'll be using this site: https://www.dcode.fr/ascii-code
  - ![alt text](https://i.imgur.com/FwLVMh1.png)
- Nice password, let's go ahead and log in. We'll use that boris user that we saw in the site source code
  - ![alt text](https://i.imgur.com/YpxehCf.png)
- 









***Flags:***

1. 

