[Most Cookies](https://play.picoctf.org/practice/challenge/177)

## problem statement
Alright, enough of using my own encryption. Flask session cookies should be plenty secure!
Additional details will be available after launching your challenge instance.

## Hint
1. How secure is a flask cookie?


## Solution
1. Install the Cracking Tool
<br><br>

On Kali Linux, you need a tool that can read and "re-sign" Flask cookies.
<br><br>

`pip3 install flask-unsign[wordlist] --break-system-packages`

2. Create the "Guessing" Wordlist
 
This is the most important setup step. The server's "secret key" is one of 28 specific cookie names. You use the cat command to create a dictionary file that the tool will use to guess the password.
<br><br>

so you need to run a `nano wordlist.txt` which here it is if you need it [script.py](script.py)

3. Find the Secret Key (Brute-Force
<br><br>

Now, you give the tool your current cookie (from your browser) and the list of words you just made. It will test every word until it finds a match.
Run this command: `flask-unsign --unsign --cookie 'eyJ2ZXJ5X2F1dGgiOiJibGFuayJ9.afJ_ow.kwC0cfqBSOOfe0efTFzRxajdXbg' --wordlist wordlist.txt`

The result: will tell secrey key that for website

5. Forge the Admin Cookie
<br><br>

Now that you have the secret key, you can "sign" your own cookie and the server will believe it is real.
Run this command:
`flask-unsign --sign --cookie "{'very_auth': 'admin'}" --secret 'pinwheel`

The result: The terminal will give you a new long string, Copy it.

6. when you copy it go in website and `inspect -> application -> storage -> cookie`

after you that go to value in cookie and change value to secret key given

