****

# bookface

![alt text](https://i.imgur.com/lbYrx0Y.png)


**Source:** Created by ben on TryHackMe

***Description:***
	
​	Are you able to root this machine? Jerry is a new developer and has made a few mistakes!

***Related Hosting Links***

- TryHackMe
  - Hosted as a subscriber only room at the time of writing.
  - Link: https://tryhackme.com/room/bookface

***Special Notes:***

​	*Scanning this specific box is a little different from most rooms. I highly recommend coming into this room with having set up Nessus or a similar higher-end scanning tool in order to produce better overall recon. Additionally, at the time of writing, this box has a fair amount of brute-forcing. Be prepared to solve this box over the series of several hours to a few days.* 



***Instructions:*** 

- As we start most boxes, let's begin with some scanning! For this, let's use nmap.
  - ![alt text](https://i.imgur.com/pKgOHHo.jpg)
  - ![alt text](https://i.imgur.com/mypkUn4.jpg)
- Well that's odd. After allowing this scan to run to completion, I found that every port on this box is reporting as open. Within this instance, if we allow nmap to complete we can see this isn't entirely true, but nmap clearly isn't helping us in this case. Let's go ahead and try Nessus. 
  - ![alt text](https://i.imgur.com/tLDPafd.png)
- Nessus is a commonly used scanning tool within the field of penetration testing. Nessus is installed as a server and offers a free home version, which, for our use case is incredibly useful. For more information, check out this link: https://www.tenable.com/products/nessus-home
- Since nmap isn't giving us great results with our typical scan, we'll go ahead and run a basic network scan with Nessus. I'll be using the following settings for this scan:
  - Scan Type: Basic Network Scan
  - Discovery: All Ports
  - Advanced: Scan low bandwidth links*
    - *This is useful for our case as we are scanning over a vpn connection
    - *It is also worth noting that running UDP and ACK scans will also find near identical results to Nessus. UDP will find DNS and ACK will identify FTP*
- Let's go ahead and take a look at the results of this scan
  - ![alt text](https://i.imgur.com/IYtcKF3.jpg)
- Interesting, it looks like both DNS and FTP services are reporting on the target box. We'll revisit DNS later, for now let's try and brute force the FTP credentials. For this, we'll be using hydra. Additionally, we'll be using jerry as our test user since he was listed above as the developer.
  - ![alt text](https://i.imgur.com/NWEVh9O.jpg)
  - ![alt text](https://i.imgur.com/U4B82Eq.jpg)
- Success! We have our FTP password!
- Let's go ahead and log in:
  - ![alt text](https://i.imgur.com/I2TljWj.jpg)
- There's our first flag and a lovely note. Let's check out that note
  - ![alt text](https://i.imgur.com/nBlENjB.jpg)
- Looks like we'll need to revisit that DNS service. Let's try a dig lookup against the box
  - ![alt text](https://i.imgur.com/Ojs2fVC.jpg)
  - ![alt text](https://i.imgur.com/g1rg23D.jpg)
- And there's our second flag with some interesting ports listed in an odd order. Let's giving port knocking this a try! We'll go ahead and use the knockd package (apt install knockd)
- Through a little bit of testing of different login methods with the credentials we've previously gained, we find that we can run this port knocking script and then immediately attempt to log into the newly exposed ssh port. We can run this as such:
  - ![alt text](https://i.imgur.com/8irj8ZK.jpg)
- Success! Looks like Jerry's home directory is being served directly by the ftp server, whoops!
  - ![alt text](https://i.imgur.com/I67Zh8z.jpg)
- First, let's see what other users we have present on the machine by checking the home directory
  - ![alt text](https://i.imgur.com/y6H7ctN.jpg)
- Bingo! There's our third flag! Looks like no other users than jerry and root, let's move on to enumeration. For this specific instance, we'll cover all of our bases by using a Priv Esc checklist. I'll be using this specific version: 
  - https://failingsilently.wordpress.com/2017/08/07/privesc/
- We'll go ahead and run the following to check all of the binaries for anything out of the ordinary on the system
  - ![alt text](https://i.imgur.com/Is1kPyH.png)
  - ![alt text](https://i.imgur.com/13jdpkU.png)
- It appears that we have an outdated version of screens installed, upon looking online we find the following vulnerability
  - ![alt text](https://i.imgur.com/RnHZ5Wx.jpg)
  - Link: https://www.exploit-db.com/exploits/41154
- Now to run this! Let's go ahead and pull it from our box using SimpleHTTPServer again, notes that I have created a script named 'screenEsc.sh' and have added the contents of the screen exploit script to this file. Additionally, this SimpleHTTPServer is hosted within the same directory as the screenEsc.sh.
  - ![alt text](https://i.imgur.com/679ctap.png)
  - *Modification locations for screenEsc.sh*
  - ![alt text](https://i.imgur.com/bIa1uVk.png)
- We'll pull and run this script with the following command
  - ![alt text](https://i.imgur.com/CWeDIOG.jpg)
  - ![alt text](https://i.imgur.com/gKpeayg.png)
- Looking good! Let's check for our final flag in root's home directory
  - ![alt text](https://i.imgur.com/nimI0o8.png)









***Flags:***

1. On the FTP server, specifically within the flag1 file.
2. Within the DNS txt records, listed as a txt record along with some port information.
3. In the home directory of the bookface box.
4. In the root directory of the bookface box.

