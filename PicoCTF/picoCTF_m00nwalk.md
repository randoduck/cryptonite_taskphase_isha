# m00nwalk
## challenge 
*Decode this message from the moon.*
Hint:*How did pictures from the moon landing get sent back to Earth?*
Hint2:*What is the CMU mascot?, that might help select a RX option*
## Thought Process

I am using QSSSTV to decode an SSTV image embedded in a WAV file. By loading the audio file into the software, I can analyze the sound signals, which contain the encoded picture, and convert them back into a visible image. This process allows me to extract visual information sent as audio over radio frequencies.

```bash
randoduck@DESKTOP-2PM3SNS:~$ sudo apt-get install pavucontrol
randoduck@DESKTOP-2PM3SNS:~$ sudo apt-get install qsstv
randoduck@DESKTOP-2PM3SNS:~$  pactl load-module module-null-sink sink_name=virtual-cable
22
```
After Installation I opened `qsstv` and `pavucontrol` on two different tabs and for both a GUI interface popped up. On the interface I had to make sure of a few things :

- In pavucontrol "Output Devices" tab must be set to  "Null Output" device.

- In qsstv to "Options" -> "Configuration" -> "Sound" and select the "PulseAudio" Audio Interface

- In Pavucontrol , select the "Recording" tab and specify that QSSTV should capture audio from the Null Output

- The mode must be set to Scottie 1 , thanks to the hint 

It should look somewhat like this :
![Screenshot (178)](https://github.com/user-attachments/assets/443df0dc-c2f8-4e85-b011-e78289536ab1)

After executing this command :
```bash
paplay -d virtual-cable message.wav
```
we get the final flag as :
![moon](https://github.com/user-attachments/assets/7775a179-8a31-4e95-9a54-e27337b0e996)
picoCTF{beep_boop_im_in_space}
## <3
