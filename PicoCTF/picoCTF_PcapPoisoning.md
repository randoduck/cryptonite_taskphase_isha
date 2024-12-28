# PCAP Poisoning

## Challenge
How about some hide and seek heh?
*Download this file and find the flag.*

## Thought Process and Solution
 The first Step was to download the file and check the file type and it was clear that it was a PCAP File. Network traffic is stored and captured in a PCAP file (Packet capture), with a program like tcpdump or Wireshark (both based on libpcap). Then next instinct was to use `exiftools` which wasn't really helpful but we had to be sure . Since it's a PCAP File it could further be analysed using Wireshark . 

Since for this particular challenge I didn't have access to wireshark because of the absence of my laptop . I looked into other approaches 
like using the `cat` command which just gave me  what looks like a Binary file with Headers. So I used `strings` command to obtain human readable characters from the file, which gave me a very long almost repetitive output .  Then I tried installing tcpdump on the web shell on pico which didn't go as planned. On reading the challenge title again, it seemed like we were supposed to find the next clue amongst the packets . This led to me trying the `grep` command along with `strings` to find the flag and that's how I obtained the flag for this challenge.


picoCTF{P64P_4N4L7S1S_sU55355FUL_f621fa37}

## <3