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

After racking my brain and iteratively going through all the Data Formats on CyberChef I found a hash that I have never touched or heard of before, Base58:

<img width="960" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/f351cf85-323b-4451-8140-0a61c49a3033">

Saving the decoded text into a file for future use.

# FTP Enumeration #
After attempting the found texts in ftp & ssh I get a successful connection using FTP:


<img width="598" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/d6e315ff-2d24-43d1-aa9d-830a45fef601">


<img width="598" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/d020b926-c393-4962-a674-ca799099fc0b">

Grabbing all the files I will see where else I have access in the system with ftp:

<img width="496" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/92f0bb2c-b221-46d4-894a-c512ed1f7585">

Looks like there is another user that I can add to the users text file.

# Steganography #

Opening all the picture files but Leave_me_alone.png as I was greeted with the following error:

<img width="484" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/7bc4e055-a260-4475-9e3d-f1eb2cf30cba">

After doing some research I see that the magic numbers are improperly set:

<img width="960" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/16366258-743f-4de7-9fe3-7ed774b5cfbf">

What they should be:

<img width="670" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/7af8f76a-7dad-49a6-b5f6-bcbf4486cb0c">

<img width="466" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/3d78b9f6-c2f6-49ac-b076-9e492da4b712">


After adjusting the magic header I can now open the picture revealing a very tough-to-crack password:

<img width="426" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/1e7d14f7-10b4-4590-93c9-5ee3f3dc8b54">

Going through the other files I find that files are hidden in another picture file, using the password found in the previous image I find a zip file and decompress it revealing two more tasty treats:

<img width="496" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/08ceae60-33eb-4018-88c9-9e61677ebfdf">

# SSH Enumeration # 

I will use Hydra to begin brute-forcing an ssh connection using the data gathered thus far:

<img width="955" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/f46e5818-dd59-479b-9a37-83a08ac5398d">

# Initial Access # 

Using the ssh credentials I now have a foothold into the system and capture the user flag:

<img width="643" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/d0e27e0d-157c-4028-9e40-ec9ddff904ca">

After checking for sudo permissions I see that the user can invoke sudo privileges on the binary "/usr/bin/pkexec":

<img width="787" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/e36d789c-ef9f-4019-a934-e244df418f4c">

Luckily for me, I have just the toolkit to make short work of this vulnerability! 

# Priviliedge Escalation # 

Starting up a HTTP server on my Kali machine I pull the PwnKit module written by the awesome security researcher Oliver Lyak:

<img width="960" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/acc81907-c338-41b0-9617-55ffb0dbe71a">

Making this executable and running it will give you root and the root flag! 

<img width="255" alt="image" src="https://github.com/Ethical-Dyl/arrow-verse/assets/66540055/c7a89aae-394e-4048-85f4-be0be8e8e156">


