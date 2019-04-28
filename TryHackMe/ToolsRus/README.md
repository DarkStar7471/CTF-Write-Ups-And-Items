****

# ToolsRus

![alt text](https://i.imgur.com/fAFiFoI.png)


**Source:** Created by tryhackme (ben) on TryHackMe

***Description:***
	

	Practice using tools such as dirbuster, hydra, nmap, nikto and metasploit

***Related Hosting Links***

- TryHackMe
  - Hosted as a subscriber only room at the time of writing.
  - Link: https://tryhackme.com/room/toolsrus

***Instructions:*** 

- As we start most boxes, let's begin with some scanning! For this, let's use nmap.
  - ![alt text](https://i.imgur.com/5zVSS46.png)
  - ![alt text](https://i.imgur.com/VrGnz6z.png)
- Looks like we have a few normal services open including SSH and HTTP on their normal ports (22  and 80 respectively) but there's also something weird running on port 1234. Let's go ahead and investigate the http website using firefox.
  - ![alt text](https://i.imgur.com/n7n9MPS.png)
- Well that's no good! At least some of the other parts are still functional, let's go ahead and find those using dirb!
  - ![alt text](https://i.imgur.com/OnQqoWb.png)
  - ![alt text](https://i.imgur.com/Wc4mUkK.png)
- Let's go ahead and check out both of those pages
  - ![alt text](https://i.imgur.com/0gUCbOA.png)
- And /protected/?
  - ![alt text](https://i.imgur.com/amssFbd.jpg)
- Well, that's definitely protected, just not very well! Let's try using hydra to brute force that password. I'll attempt this using the user that was mentioned on the guidelines page, bob.
  - ![alt text](https://i.imgur.com/JiS7xom.png)
  - ![alt text](https://i.imgur.com/b9p8oFy.png)
- There's our password!  Let's log in and see what we're working with
  - ![alt text](https://i.imgur.com/s1g4lSc.png)
- Well, this is probably what's running on port 1234. Let's go ahead and run nikto against this port so we can find our new login page. 
  - ![alt text](https://i.imgur.com/kgtRQhw.png)
- There's a manager page, let's try logging into that
  - ![alt text](https://i.imgur.com/LkuYKav.png)
- Here's those files found by nikto as well!
  - ![alt text](https://i.imgur.com/h1GM3K3.png)
- Let's go ahead and run an additional credentialed scan on this system to see if we can locate any additional components running on this system
  - ![alt text](https://i.imgur.com/htdRLy3.jpg)
  - ![alt text](https://i.imgur.com/zLlgHHl.jpg)
    - *It's worth nothing this scan can take a while to run, take stock of my total scan time on my results*
- After looking around in this application, reviewing our service versions from our nmap scan, and doing a little research online we can find that this version of Apache Tomcat is pretty oudated and has a lovely vulnerability we can exploit to get a shell
  - Link to exploit notes: https://charlesreid1.com/wiki/Metasploitable/Apache/Tomcat_and_Coyote
- We'll go ahead and start up metasploit and use the following exploit package. For a few more details on this exploit, check out the aforementioned link above. 
  - ![alt text](https://i.imgur.com/ZKdhF6j.png)
  - ![alt text](https://i.imgur.com/WxqJYgf.png)
  - ![alt text](https://i.imgur.com/J0nKFYU.png)
- Set the options for this exploit as follows, make sure to fill in the password we found earlier for bob:
  - ![alt text](https://i.imgur.com/cApDY8y.png)
- And run!
  - ![alt text](https://i.imgur.com/Qp6gTpE.png)
  - ![alt text](https://i.imgur.com/WDmjwol.png)
- There's our flag! Don't run outdated servers as root! 



***Flags:***

1. Root directory on the toolsrus server. 
