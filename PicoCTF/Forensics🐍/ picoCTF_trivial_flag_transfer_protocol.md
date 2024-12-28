# Trivial Flag Transfer Protocol

## Challenge
*Figure out how they moved the flag.*
Hint: *What are some ways to hide data..*

## Thought Process and Solution
I think this was one of most exciting challenges I've come across. We were initially given a flag to download, it turned out to be a `pcapng` file. I used this particular resource to learn about and tamper with this file :
https://trailofbits.github.io/ctf/forensics/
A `pcapng` file would require *packet capture file analysis*.  Network traffic is stored and captured in a PCAP file (Packet capture), which can be analysed using programs like `tcpdump` or Wireshark (both based on libpcap). 

![image](https://github.com/user-attachments/assets/3024c9d7-50ce-46a9-9604-27d5bd1a2d5c)

After immediately downloading Wireshark and opening the `tftp.pcapng` file using wireshark, I resorted to the first principle of digital forensics - file carving . The resource that was jsut referred to had some text on `packetcarving` . "packet carving" is a term sometimes used to describe the extraction of files from a packet capture. There are expensive commercial tools for recovering files from captured packets, but one open-source alternative is the Xplico framework. Wireshark also has an "Export Objects" feature to extract data from the capture (e.g., File -> Export Objects -> HTTP -> Save all) which I just executed to find this .
![image](https://github.com/user-attachments/assets/b25e6f24-ffdd-4d8a-82f4-91f224d9dcfe)

There were in total :
- 3 Bitmap: (picture1.bmp,picture2.bmp,picture3.bmp) 
- 2 Text files: (Instructions.txt, plan.txt) 
The two text files very cleary contained rot13 cipher and after decryption was left with the following:
![image](https://github.com/user-attachments/assets/c4343839-d45d-4879-99fb-104e8bd33a19)

Now the texts clearly say that the flag is hidden within the Images, and after looking into the metadata and finding nothing the obvious approach would be stenography . Steganography could be implemented using any kind of data as the "cover text," but media file formats are ideal because they tolerate a certain amount of unnoticeable data loss (the same characteristic that makes lossy compression schemes possible). A few good tools would be Stegsolve, steg and Steghide. I went with Steghide and followed this tutorial to download and extract data :
https://sourceforge.net/projects/steghide/
https://www.youtube.com/watch?v=CYjc3Ib12EQ
used the commands after changing into the directory in which the pictures were located:
```cmd
steghide extract -sf picture3.bmp
```
but discovered that I didn't know what the passpharase was in order to execute the extraction, after a little thought anf going through the hints provided the the passphrase turned out to be DUEDILIGENCE which worked for the third picture with cute sheep in it. and finally the `flag.txt` was made available in my folder :picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}
![image](https://github.com/user-attachments/assets/2e1bd9a0-7cd1-48d3-a167-0744f3a14c93)


## <3
