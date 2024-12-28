# SOAP
## Challenge
*The web project was rushed and no security assessment was done. Can you read the /etc/passwd file?*
*Additional details will be available after launching your challenge instance.*
*The web project was rushed and no security assessment was done. Can you read the /etc/passwd file?*
Hint: *XML external entity Injection*

## Thought Process

The hint was pretty clear that we will have to implemnet a XML external entity Injection.XML External Entity (XXE) Injection is a security vulnerability that allows an attacker to manipulate or exploit XML input to access sensitive information, execute remote code, or cause a denial of service. It occurs when an application processes XML data containing external entities (references to external files or resources) without proper validation or restrictions. By injecting malicious XML code, attackers can exploit these entities to read server files, access restricted data, or even compromise the server. The presence of an XXE file was confirmed by looking into the source code . Anyway I had to refer to a few resources in order to implement this :
https://youtu.be/iGDJ695dUEM?si=v-7o0QNB6NBhMTid
 https://youtu.be/t1yHqIhhemI?si=0BPHx9geFXKNJSfr

I tried implementing XML Injection through the Newtork tab available in the developer tools for the web page , which did not quite workout as I was unable to send POST requests from there . Hence I downloaded this tool called `Burpsuite`. Burp Suite is a cybersecurity tool for testing web application security. It includes features like an intercepting proxy, vulnerability scanner, and tools for manual testing. Security professionals use it to find issues like SQL injection and XSS. I used this Installation guide for it to work :
https://youtu.be/VK3n5xgPB20?si=-7QHZUSYdoufyL30

![image](https://github.com/user-attachments/assets/f6fba6cb-30a6-46a2-bc15-dc6989cd3a6a)

One more tool that I used to make this process easier was `Foxy Proxy` which helped me connect to Burp with just a click . The FoxyProxy extension manages proxy server settings for your browser. It allows users to quickly switch between proxies, route specific traffic through a proxy, and configure advanced proxy rules for improved privacy, security, or access to restricted content. I added the Burp Proxy on it for easier access and this is what it looked like :
![Screenshot (183)](https://github.com/user-attachments/assets/e2e9b661-f5e3-4ede-956c-d0ae8e80cd00)

## Solution
Firstly I navigated to the challenge and started the Instance , On starting the Instance I copied the address and pasted it in the `Open Browser` section under `Proxy` tab and just to make sure everything goes smoothly . I switched to `Burp` proxy in the `Foxy Proxy` extension after opening the web page and switched to mobile hotspot as well as attempts while being connected to my own wifi were unsuccessful.

![image](https://github.com/user-attachments/assets/f23e6a90-7ad8-4012-bf02-d1054c4839b8)

Once you open the webpage and Click on any of the boxes labeled as `Details` and going back to Burpsuite , this is what you get :
![image](https://github.com/user-attachments/assets/37634117-add0-4471-a619-92c7faa94cd1)

After clicking on right clicking on `POST request` and selecting `transfer to Repeater` option . I Navigated to the Repeater tab and Injected my custom XXE payload as follows and clicked on `send` which ultimately resulted in me getting the flag .
```html
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE xxe [<!ENTITY passwd SYSTEM "file:///etc/passwd">]>
<data><ID>&passwd;</ID></data>
```
![image](https://github.com/user-attachments/assets/5ce5a75c-ac22-4e38-9d8b-53e0bea4365b)
And after lots of trail and error, the flag was finally obtained in the response box.
*picoCTF{XML_3xtern@l_3nt1t1ty_e5f02dbf}*

## <3
