# Hideme
## Challenge 
*Every file gets a flag.*
*The SOC analyst saw one image been sent back and forth between two people. They decided to investigate and found out that there was more than what meets the eye here.*

## Thought Process
Initially I saw a png file and tried to put it through steghide, which did not turn out as i expected. 
![image](https://github.com/user-attachments/assets/6f1efe7d-9e47-420f-a359-e9c9cd1627a1)

## Solution
Then I had to resort to the first principle of forensics which was file carving .
```bash 
randoduck@DESKTOP-2PM3SNS:~$ exiftool flag.png
ExifTool Version Number         : 12.76
File Name                       : flag.png
Directory                       : .
File Size                       : 43 kB
File Modification Date/Time     : 2023:03:16 03:15:31+00:00
File Access Date/Time           : 2024:12:22 17:21:26+00:00
File Inode Change Date/Time     : 2024:12:22 17:21:19+00:00
File Permissions                : -rw-r--r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 512
Image Height                    : 504
Bit Depth                       : 8
Color Type                      : RGB with Alpha
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Warning                         : [minor] Trailer data after PNG IEND chunk
Image Size                      : 512x504
Megapixels                      : 0.258
randoduck@DESKTOP-2PM3SNS:~$ binwalk flag.png

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 512 x 504, 8-bit/color RGBA, non-interlaced
41            0x29            Zlib compressed data, compressed
39739         0x9B3B          Zip archive data, at least v1.0 to extract, name: secret/
39804         0x9B7C          Zip archive data, at least v2.0 to extract, compressed size: 2858, uncompressed size: 3015, name: secret/flag.png
42897         0xA791          End of Zip archive, footer length: 22
```
`binwalk` command shows the embedded files which can be extracted using `binwalk -e flag.png`. We find `_flag.png.extracted` in the directory. On repeatedly navigating the files and opening, we come across a png file. To open this png file directly from ubuntu I installed an Advanced Image Editor called GIMP, using the following commands:
```bash
sudo apt update
sudo apt install gimp
```
and opened the file using 
```bash
gimp flag.png
```
![Screenshot (191)](https://github.com/user-attachments/assets/5ef202e3-7fb4-4378-ba83-94557ac8bce6)
![Screenshot (193)](https://github.com/user-attachments/assets/50420741-956d-4c26-9e51-6ac7685c3e9a)
picoCTF{Hiddinng_An_imag3_within_@n_ima9e_96539bea}
## <3
