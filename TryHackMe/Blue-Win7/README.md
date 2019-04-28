****

# Windows 7 Capture the Flag

![alt text](https://i.imgur.com/VO2P4Tm.gif)

**Source:** DarkStar7471 aka J0n

***Description:***

​	A realistic (at the time of writing) Windows box that is relatively simple in complexity. 

***Related Hosting Links***

- *TryHackMe.com*
  - Hosted currently as a free room! Recommended for beginners.
  - Link: https://tryhackme.com/room/blue

***Special Notes:***

​	If using VMware, use NAT. This can be very picky about being on host-only for whatever reason and often times just doesn't work. You'll notice the IP of both the attack box and the target vulnerable box change in this case 	



***Instructions:*** 

- Start by first checking the IP address of the Kali (or other attack box) you are attacking from
  - ifconfig
  - ![alt text](https://i.imgur.com/vA01pmM.png)
- Following finding the IP address of our attack box, we can move onto discovering the address of the vulnerable box we will be attacking. This can be done either via netdiscover or nmap. Nmap is demonstrated below with a few select flags added for vulnerability discovery.
  - nmap 
  - ![alt text](https://i.imgur.com/iWmqxQI.png)
  - -vv : Very verbose
  - -sS : Syn scan (can also use -sV for version numbers)
  - --script vuln : Check for vulnerabilities using the nmap scripting engine
- After waiting a bit, we can see the our results have been generated:
  - ![alt text](https://i.imgur.com/EdrB4PX.png)
  - General port information
  - ![alt text](https://i.imgur.com/z7YkpXq.png)
  - Looks like the target system is vulnerable to ms17-010, otherwise known as Eternal Blue! We can exploit this to run arbitrary code on the target system
- Let's start Metasploit
  - ![alt text](https://i.imgur.com/WPE5Jjb.png)
- And find ms17-010 related exploits
  - ![alt text](https://i.imgur.com/QUgAPqt.png)
- Our search results
  - ![alt text](https://i.imgur.com/8Crb3UQ.png)
- Let's go ahead and use this one
  - ![alt text](https://i.imgur.com/MRU21Q3.png)
- Before we continue, we should check what options we must set before running this exploit
  - ![alt text](https://i.imgur.com/D6KlTo1.png)
  - ![alt text](https://i.imgur.com/JZUEOXU.png)
- Looks like we'll have to set the RHOST, remote host
  - ![alt text](https://i.imgur.com/tOefr2A.png)
- That should be everything, let's go ahead and run it!
  - ![alt text](https://i.imgur.com/B2vZLXQ.png)
  - ![alt text](https://i.imgur.com/NbWkwJs.png)
  - **This can occasionally fail, try running it a couple times after rebooting this vulnerable machine if necessary.*
- For now, let's go ahead and background this dos shell. We're going to upgrade it to a meterpreter shell, something quite a bit more powerful for our purposes!
- Let's go ahead and set our current module to the converter and check the options we'll have to set
  - ![alt text](https://i.imgur.com/8I7dZpp.png)
  - ![alt text](https://i.imgur.com/LMYGcIC.png)
- Looks like we'll have to set which session we need to convert, let's list our sessions
  - ![alt text](https://i.imgur.com/0JAAzN0.png)
- Looks like we'll have to set it to session 1
  - ![alt text](https://i.imgur.com/iAYMIEA.png)
- Looks good! Let's go ahead and launch our converter
  - ![alt text](https://i.imgur.com/5ymX5HJ.png)
  - ![alt text](https://i.imgur.com/O4H6Nw6.png)
- Let's go ahead and make sure we have system level privileges
  - ![alt text](https://i.imgur.com/rmH7hnM.png)
  - ![alt text](https://i.imgur.com/yBEAqpV.png)
- We'll go ahead and background this shell since we've confirmed that we have elevated permissions. Let's get ready to dump any password hashes on the system.
- First, let's list all of the processes running on the system. Just because we have system level privileges doesn't mean our process does! We'll have to migrate to a new process that does have those permissions
  - ![alt text](https://i.imgur.com/OoafyEJ.jpg)
- Look for a process running as nt authority\system from this list generated
  - Good candidates here are powershell and cmd or programs such as word that may have been left running on this system
- Once a process is found, type migrate PROCESSID, where PROCESSID is the id of the process we are migrating to (left column of the ps table generated previously)
  - This migration process may fail, migrating processes is only successful realistically about 25% of the time.
  - ![alt text](https://i.imgur.com/rSBRzLz.jpg)
- Once you control a higher-privileged process, type hashdump
  - ![alt text](https://i.imgur.com/wq07Eh6.jpg)
  - This will display the password hashes stored in the SAM database of the unit 
  - This password can be copied to text file and cracked. The specific one in use at the time of writing is within rockyou.txt
  - ![alt text](https://i.imgur.com/8yxFAk1.jpg)
  - Hash file created and hashes copied in. File name is arbitrary here. 
- Look for the three flags spread throughout the system!









***Flags:***

​	Three spread throughout the system in the following locations:

1. The root of the C drive, meant to represent initial contact with the system and a good sanity check for pen testers.
   1. ![alt text](https://i.imgur.com/7Lxd89R.jpg)
2. C:\Windows\System32\config, this is the actual location of the SAM database
   1. ![alt text](https://i.imgur.com/8QtrJb6.jpg)
3. Admin's (Jon's) documents folder, elevated user's and staff documents can be very useful in prolonged engagements.
   1. ![alt text](https://i.imgur.com/cHfepkx.jpg)
