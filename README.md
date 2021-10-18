# DEADFACE CTF Network Traffic Analysis Write Up
<p align="center">
<img src="https://cdn.discordapp.com/attachments/777172077673054228/899740210601029632/logo_deadface_2021.png" width="750" height="750">
</p>

*Note: This write up contains these challenges: Monstrum ex Machina, The SUM of All FEARS, Release the Crackin'!, Luciafer, You Clever Little Devil!, Luciafer's Fatal Error, A Warning*

## 1st Challenge **Monstrum ex Machina**

**Here's the description of the challenge:**

> Our person on the "inside" of Ghost Town was able to plant a packet sniffing device on Luciafer's computer. Based on our initial analysis, we know that she was attempting to hack a computer in Lytton Labs, and we have some idea of what she was doing, but we need a more in-depth analysis. This is where YOU come in.
We need YOU to help us analyze the packet capture. Look for relevant data to the potential attempted hack.
To gather some information on the victim, investigate the victim's computer activity. The "victim" was using a search engine to look up a name. Provide the name with standard capitalization: flag{Jerry Seinfeld}.

We were given a pcap to solve this challenge.

Let's start with opening the pcap file in wireshark.
![image](https://user-images.githubusercontent.com/61091272/137784780-e7e13241-0295-4c07-9f3f-298a77d65dda.png)

Let's start with adding this filter: **http.request** so we could look at the http traffic.

As I was scrolling through the http traffic I found this:
![image](https://user-images.githubusercontent.com/61091272/137785685-2f1fecbf-6d2c-423e-8f2f-905def4de590.png)

As you can see we got a name there: **Charles Geschickter**

Which is also the name we were looking for!

So the flag is: **flag{Charles Geschickter}**

## 2nd Challenge **The SUM of All FEARS**

**Here's the description of the challenge:**

> After hacking a victim's computer, Luciafer downloaded several files, including two binaries with identical names, but with the extensions .exe and .bin (a Windows binary and a Linux binary, respectively).
What are the MD5 hashes of the two tool programs? Submit both hashes as the flag, separated by a |: flag{ExeMD5|BinMD5}


I started off by adding this filter: **ftp-data** 

So I could see the ftp traffic that was captured.
![image](https://user-images.githubusercontent.com/61091272/137787632-ddc4f433-1e38-4e78-8206-0d84b8a35825.png)

I started scrolling through it and found these two **lytton-crypt.bin** and **lytton-crypt.exe**
![image](https://user-images.githubusercontent.com/61091272/137787910-25711955-3907-440a-b53d-d5f3907d0e3e.png)

I decided to make a folder so I could export the tcp stream data:

![image](https://user-images.githubusercontent.com/61091272/137788330-b7f5c119-7b12-4275-9b88-a4d1f2ae8c34.png)

I started exporting the tcp streams into the folder I just made:
![image](https://user-images.githubusercontent.com/61091272/137788744-120db550-06d3-4810-ad4f-61d5b3a46c74.png)

I saved them as **sumexe** and **sumbin**

Then ran this command to find the md5 hash: **md5sum**

![image](https://user-images.githubusercontent.com/61091272/137789293-ca329e01-ad40-4062-8b75-375da7c9af6f.png)

**That's it, challenge solved!**

Here's the flag: **flag{9cb9b11484369b95ce35904c691a5b28|4da8e81ee5b08777871e347a6b296953}**

## 3rd Challenge **Release the Crackin'!**

**Here's the description of the challenge:**

> Luciafer cracked a password belonging to the victim. Submit the flag as: flag{password}.

I started off with adding this filter: **ftp**

![image](https://user-images.githubusercontent.com/61091272/137790799-375b11a7-da11-4bf0-84f7-9791f7f71045.png)

Then I pressed Ctrl+F and typed in **password** and started going through it until I ran into this:
![image](https://user-images.githubusercontent.com/61091272/137791300-199c7c26-1de9-4378-920c-d5c7148b5c4d.png)

We can see that they were able to login with the password: **darkangel**

Which also is the flag we were looking for!

The flag: **flag{darkangel}**

## 4th Challenge **Luciafer, You Clever Little Devil!**

**Here's the description of the challenge:**

>Luciafer gains access to the victim's computer by using the cracked password. What is the packet number of the response by the victim's system, saying that access is granted? Submit the flag as: flag{#}.
NOTE: Use the packet response from her login, not from the password cracker.

As the description is telling us we need to get the packet's number which says access is granted.

I left on the same filters from the previous challenge.
![image](https://user-images.githubusercontent.com/61091272/137792521-a5806c7d-3eae-43f7-b538-14592884f191.png)

The flag: **flag{159765}**

## 5th Challenge **Luciafer's Fatal Error**

**Here's the description of the challenge:**

>Luciafer, consummate hacker, got cocky and careless. She made a fatal mistake, and in doing so, gave control of her computer to... someone. She ran a program on her computer that she shouldn't have.
What is the md5sum of the program? Submit the flag as: flag{MD5}.

I started with adding this filter: **ftp-data**

And started looking through it and found this:
![image](https://user-images.githubusercontent.com/61091272/137795002-d76c20c5-0a1f-4380-851d-c26904b56c1c.png)

Then I followed the TCP stream and exported it to the folder I made before:
![image](https://user-images.githubusercontent.com/61091272/137795227-fdc22e3f-ad09-44ee-a2ac-bd56d90cc184.png)

After that I ran the **md5sum** command on it and got the program's md5sum we were told to find:
![image](https://user-images.githubusercontent.com/61091272/137795553-7063f6d9-aa97-492e-9f97-ac941869067e.png)

**Challenge solved!**

The flag: **flag{42e419a6391ca79dc44d7dcef1efc83b}**

## 6th Challenge **A Warning**

**Here's the description of the challenge:**

>Luciafer is being watched! Someone on the inside of Lytton Labs can see what she is doing and is sending her a message.
One of them says: "Stay away from Lytton Labs... you have been warned."
To find the flag, find the message. You'll know it when you see it. Submit the flag as flag{flag-goes-here}.

Started off by putting on this filter: **http.request**

Then I pressed **Ctrl+F** to bring up the Find section and typed in **warning** and this popped up:
![image](https://user-images.githubusercontent.com/61091272/137796805-7acbfc0c-2022-473f-a616-a8f3488a5444.png)

Then I did this: **File > Export Objects > HTTP**

Scrolled all the way down and clicked on **da-warning-message.jpg** and saved it to the folder I made before:
![image](https://user-images.githubusercontent.com/61091272/137798502-968dcf93-18bc-4a9a-a577-34e0997bf6e7.png)

Then I went into the folder and opened the image:
![image](https://user-images.githubusercontent.com/61091272/137799049-07a896cc-c391-42a7-8bc7-9260b4c3f805.png)

And boom! There's the flag!

The flag: **flag{angels-fear-to-tread}**

