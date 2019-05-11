# JoyStick

![alt text](./images/logo.png?raw=true "JoyStick Logo")

**Source:** Created by DarkStar7471 aka J0n

***Description:***

​	Anyone want to play?

***Related Hosting Links***

- *TryHackMe*
  - Hosted for free, medium to hard difficulty.
  - Link: https://tryhackme.com/room/joystick

***Author's Notes:***

NOTE SPOILERS AHEAD, SKIP AUTHOR'S NOTES TO AVOID ANY HINTS

​JoyStick, as the name would imply, consists of a machine that hosts a game server. This game server, specifically a Minecraft 1.13.2 server, does indeed work however it's specifically not built very well. To preface further information, understand that this box was built within a confined mindset.

Drawing upon experience in my youth, JoyStick was constructed by cutting corners after creating intentional issues. For example, several services simply don't work or simply are simply absent from the machine. These include:

- A vsftp FTP server that, while appearing to work upon initial inspection with anonymous login enabled, allows little more than listing the files. This is a direct consequence of misconfigured permissions along with the installation anon user home directory having been moved several times through an intentionally botched installation.

- A web server running with little more than a coming soon message. Examining the source code of this website reveals sensitive information left for another staff member. The staff member's username can also be discovered this way.

- An exposed SSH server which can be enumerated for users.

- Overarching problems which are not resolved properly. Packages are moved around without clean up, directory permissions are set with the 'easy' fix of chmod 777 or with similar unsafe methods.

- The Minecraft server, along with some additional items, run as root with full root permissions. Unprivileged users can interact with several of these items. This represents the common idea among amateur administrators that running something as root is a valid solution to the potential issue of servers not launching when run as unprivileged users. 

A key note to take away from this is that, while the machine itself is nearly completely up to date, issues are still rampant due to the purposeful inexperience injected into the construction.



***Instructions:***

-









***Flags:***

- /home/steve/user.txt
- /home/notch/root.txt
​
