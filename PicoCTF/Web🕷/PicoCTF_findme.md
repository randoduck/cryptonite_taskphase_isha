# findme
## Challenge
Help us test the form by submiting the username as test and password as test!
Additional details will be available after launching your challenge instance.

## Thought Process 
After Reading the challenge description it was evident that one must use Burpsuite. On connecting the server to Burp, I tinkered around a bit, with not much success. 
![Screenshot (232)](https://github.com/user-attachments/assets/23d45e7c-8df3-490a-960b-3da38364c0e3)

On Inspecting the Requests after pressing forward multiple times, I highlighted the New page Id , which Immediately gave me what looked like the Second half of the flag itself.  Realising the First Half must also be present , Tried tracing back my steps . On switching to the tab on Chrome a Different Page Id was visible, which I decoded using a Base 64 decoder. 

After Login:
![Screenshot (233)](https://github.com/user-attachments/assets/a759c694-0e7a-40e6-914d-bcb782a25f6d)

The Proxy Tab :
![Screenshot (234)](https://github.com/user-attachments/assets/99f81102-3e35-4d4b-9ba5-0307b7158c37)

On Highlighting Using cursor the Inspector was able to Identify the Encoding and decode it for me:
![Screenshot (238)](https://github.com/user-attachments/assets/da2ceb83-db39-47d3-80da-1f34cd584d10)

Page Id on the Chrome Tab :
![Screenshot (236)](https://github.com/user-attachments/assets/88ae003c-0c49-4804-aa7e-f1fcb896cc5c)

Using the Base 64 Decoder:
![Screenshot (237)](https://github.com/user-attachments/assets/480d2e32-6eaa-4a71-9e60-81e6ce36feb2)

The Final Flag  : picoCTF{proxies_all_the_way_25bbae9a}
## <3
