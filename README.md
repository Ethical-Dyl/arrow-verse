# arrow-verse
This is a writeup on the THM CTF [Lian_Yu]([url](https://tryhackme.com/room/lianyu)https://tryhackme.com/room/lianyu)


# Initial Enumeration # 

Beginning the nmap scan against my target reveals there are 5 ports open on this machine:

<img width="489" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/77738178-0e53-43ac-ab49-2434aab845b0">

Starting up a web fuzzing tool to find some directories while I poke around some of the other services and the webpage

<img width="773" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/176411ec-4887-4242-b973-36f68d3b6011">

Attempting to connect anonymously via ssh and ftp proved futile however dirbuster has found some directories with some useful information.

# Web Enumeration # 

The first directory found also has a subdirectory attached to it navigating to the first directory I see that there is a hidden word on the page:

<img width="960" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/4debd9f7-cc21-47b8-a1dd-bbbde66dd8d8">

Adding this to a text file for future use.

The second directory hosts a webpage with a YouTube URL however viewing the source code I find something interesting:

<img width="382" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/a3c661b4-a84e-412f-8029-cce038435628">

Adding the extension found to my dirbuster scan I find the following:

<img width="387" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/4636c17d-bd04-4c1b-b8d1-463f5e7fa7e9">

Navigating to the file I get a hashed value:

<img width="960" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/aea9fc96-db65-4d1a-95ff-25df9e8582e8">

Using CyberChef I found a hash that I have never touched or heard of before, 

