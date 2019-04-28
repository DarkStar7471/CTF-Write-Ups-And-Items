****

# Windows 7 Capture the Flag

![alt text](./images/logo.gif?raw=true "Logo")

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
  - ![alt text](./images/ifconfig.png?raw=true "ifconfig")
- Following finding the IP address of our attack box, we can move onto discovering the address of the vulnerable box we will be attacking. This can be done either via netdiscover or nmap. Nmap is demonstrated below with a few select flags added for vulnerability discovery.
  - nmap 
  - ![alt text](./images/nmap-cmd.png?raw=true "nmap-cmd")
  - -vv : Very verbose
  - -sS : Syn scan (can also use -sV for version numbers)
  - --script vuln : Check for vulnerabilities using the nmap scripting engine
- After waiting a bit, we can see the our results have been generated:
  - ![alt text](./images/nmap-results-1.png?raw=true "nmap-results-1")
  - General port information
  - ![alt text](./images/nmap-results-2.png?raw=true "nmap-results-2")
  - Looks like the target system is vulnerable to ms17-010, otherwise known as Eternal Blue! We can exploit this to run arbitrary code on the target system
- Let's start Metasploit
  - ![alt text](./images/msfconsole.png?raw=true "msfconsole")
- And find ms17-010 related exploits
  - ![alt text](./images/search-blue.png?raw=true "search-blue")
- Our search results
  - ![alt text](./images/search-blue-results.png?raw=true "search-blue-results")
- Let's go ahead and use this one
  - ![alt text](./images/use-blue.png?raw=true "use-blue")
- Before we continue, we should check what options we must set before running this exploit
  - ![alt text](./images/options-blue.png?raw=true "options-blue")
  - ![alt text](./images/options-blue-results.png?raw=true "options-blue-results")
- Looks like we'll have to set the RHOST, remote host
  - ![alt text](./images/set-rhost.png?raw=true "set-rhost")
- That should be everything, let's go ahead and run it!
  - ![alt text](./images/exploit.png?raw=true "exploit")
  - ![alt text](./images/win.png?raw=true "win")
  - *\*This can occasionally fail, try running it a couple times after rebooting this vulnerable machine if necessary.*
- For now, let's go ahead and background this dos shell. We're going to upgrade it to a meterpreter shell, something quite a bit more powerful for our purposes!
- Let's go ahead and set our current module to the converter and check the options we'll have to set
  - ![alt text](./images/meterpreter.png?raw=true "meterpreter")
  - ![alt text](./images/met-options.png?raw=true "met-options")
- Looks like we'll have to set which session we need to convert, let's list our sessions
  - ![alt text](./images/sessions.png?raw=true "sessions")
- Looks like we'll have to set it to session 1
  - ![alt text](./images/set-session.png?raw=true "set-session")
- Looks good! Let's go ahead and launch our converter
  - ![alt text](./images/exploit-meterpreter.png?raw=true "exploit-meterpreter")
  - ![alt text](./images/sessions-result.png?raw=true "sessions-result")
- Let's go ahead and make sure we have system level privileges
  - ![alt text](./images/get-system.png?raw=true "get-system")
  - ![alt text](./images/shell-whoami.png?raw=true "shell-whoami")
- We'll go ahead and background this shell since we've confirmed that we have elevated permissions. Let's get ready to dump any password hashes on the system.
- First, let's list all of the processes running on the system. Just because we have system level privileges doesn't mean our process does! We'll have to migrate to a new process that does have those permissions
  - ![alt text](./images/ps.jpg?raw=true "ps")
- Look for a process running as nt authority\system from this list generated
  - Good candidates here are powershell and cmd or programs such as word that may have been left running on this system
- Once a process is found, type migrate PROCESSID, where PROCESSID is the id of the process we are migrating to (left column of the ps table generated previously)
  - This migration process may fail, migrating processes is only successful realistically about 25% of the time.
  - ![alt text](./images/migrate.jpg?raw=true "migrate")
- Once you control a higher-privileged process, type hashdump
  - ![alt text](./images/hashdump.jpg?raw=true "hashdump")
  - This will display the password hashes stored in the SAM database of the unit 
  - This password can be copied to text file and cracked. The specific one in use at the time of writing is within rockyou.txt
  - ![alt text](./images/save-hashes.jpg?raw=true "save-hashes")
  - Hash file created and hashes copied in. File name is arbitrary here. 
- Look for the three flags spread throughout the system!









***Flags:***

​	Three spread throughout the system in the following locations:

1. The root of the C drive, meant to represent initial contact with the system and a good sanity check for pen testers.
   1. ![alt text](./images/flag1.jpg?raw=true "flag1")
2. C:\Windows\System32\config, this is the actual location of the SAM database
   1. ![alt text](./images/flag2.jpg?raw=true "flag2")
3. Admin's (Jon's) documents folder, elevated user's and staff documents can be very useful in prolonged engagements.
   1. ![alt text](./images/flag3.jpg?raw=true "flag3")
