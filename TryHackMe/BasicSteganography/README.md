****

# Basic Steganography

![alt text](https://i.imgur.com/BUEK7W9.jpg)

**Source:** Created by SuitGuy on TryHackMe.com

***Description:***

​	A beginners introduction to image Steganography and file extraction.

***Related Hosting Links***

- *TryHackMe.com*
  - Link: https://tryhackme.com/room/basicsteganographyal

***Special Notes:***

​	*The second challenge within this room involves cracking a steganography file. This specific action can take several hours.*



***Instructions:*** 

- **Challenge 1: Basic Extraction**
  - Download this image file and discover the hidden flag
    - ![alt text](https://i.imgur.com/s6MtKfx.jpg)
  - Steganography is a game of checking several avenues and practicing consistency in examining files. In this case, let's go ahead do a basic check. Steghide is a simple tool that allows for hiding files inside other files such as images. Here we'll run the basic steghide extraction command just as a base sanity check.
    - ![alt text](https://i.imgur.com/g85WftR.png)
  - Well, it looks like something was in there! Let's see what it is
    - ![alt text](https://i.imgur.com/KJyfVpr.png)
  - Looks good!
- **Challenge 2: Cracking**
  - Download this image file and discover the hidden flag, this challenge will also require knowledge of password cracking
    - ![alt text](https://i.imgur.com/8bOYP9O.jpg)
  - Seems like this one is going to be focused on cracking the stego file. Let's try stegcracker with rockyou.txt as the wordlist
    - ![alt text](https://i.imgur.com/iKXJxrO.jpg)
    - ![alt text](https://i.imgur.com/U4B82Eq.jpg)
  - Well it seems that all that time was worth it, let's take a look at that output
    - ![alt text](https://i.imgur.com/x1lKCgk.jpg)
  - There we go!
- **Challenge 3: A Little Bit of Everything**
  - Download this image file and discover the hidden flag, this challenge will also require A basic understanding of password cracking and string encoding/decoding.
    - ![alt text](https://i.imgur.com/8QfkMGK.jpg)
  - Hmm, this one looks too be fairly tricky. Let's go ahead and start by seeing if we can crack the file.
    - ![alt text](https://i.imgur.com/PHefZE4.png)
  - After a little bit that appears to have worked, let's see what we have here
    - ![alt text](https://i.imgur.com/qwmCWtS.png)
  - Well now, that's definitely encoded. We'll go ahead and run that through an online decoder
    - In this case, I'll be using this site: https://www.base64decode.org/ 
    - ![alt text](https://i.imgur.com/sCal2fc.png)
  - Closer, this looks almost like a flag. It seems that the text isn't quite right and it might have been rotated. Let's see what all of the potential rotation encryptions look like for this. I'll be using this site for that part: https://www.rot13.com/ 
    - ![alt text](https://i.imgur.com/ASgU408.png)
  - Bingo! There's our flag!









***Flags:***

​	*One within each steganography file provided within this challenge.*
