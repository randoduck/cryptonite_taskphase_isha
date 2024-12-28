# PicoCTF- Cookies

## Problem Statement
"Who doesn't love cookies? Try to figure out the best one http://mercury.picoctf.net:27177/"

## Thought Process / Solution 
First instinct was to click on the inspect tab and seach for the cookies section , discovered cookies in applications. After a little tinkering found that the value od of the cookie is editable and entered random values in the input field. I entered a few words followed by cookies and then snickerdoodle. The website changed accordingly , Additionally, a cookie's value went from -1 to 0. Through this i also found out that one could alter the cookie value , after i entered -1 again it displayed the home landing page again . After entering multiple random values , One of the limiting values could be boiled down to 28 . After entering numbers withtin the range of -1 to 28 . Finally obtained the flag int the value **18**.
```bash
picoCTF{3v3ry1_l0v3s_c00k135_cc9110ba}
```
## <3
