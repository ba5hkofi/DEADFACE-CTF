# DEADFACE CTF Traffic Analysis Write Up

Let's start with Traffic analysis challenges!

## 1st Challenge **Monstrum ex Machina**

**Here's the description of the challenge:**

> Our person on the "inside" of Ghost Town was able to plant a packet sniffing device on Luciafer's computer. Based on our initial analysis, we know that she was attempting to hack a computer in Lytton Labs, and we have some idea of what she was doing, but we need a more in-depth analysis. This is where YOU come in.
We need YOU to help us analyze the packet capture. Look for relevant data to the potential attempted hack.
To gather some information on the victim, investigate the victim's computer activity. The "victim" was using a search engine to look up a name. Provide the name with standard capitalization: flag{Jerry Seinfeld}.

We were given a pcap to solve this challenge.

Let's start with opening the pcap file in wireshark.
![image](https://user-images.githubusercontent.com/61091272/137784780-e7e13241-0295-4c07-9f3f-298a77d65dda.png)

Let's start with adding this filter so we could look at the http traffic: **http.request**

Then I found this:
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

I saved them as **sumexe* and **sumbin**

I then ran this command to find the md5 hash: **md5sum**
