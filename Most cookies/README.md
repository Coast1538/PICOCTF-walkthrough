[Most Cookies](https://play.picoctf.org/practice/challenge/177)

## problem statement
Alright, enough of using my own encryption. Flask session cookies should be plenty secure!
Additional details will be available after launching your challenge instance.

## Hint
1. How secure is a flask cookie?


## Solution
1. Install the Cracking Tool
<br<br>

On Kali Linux, you need a tool that can read and "re-sign" Flask cookies which is `pip3 install flask-unsign[wordlist] --break-system-packages` .

2. Create the "Guessing" Wordlist
<br><br>

This is the most important part. The server's need "secret key" and one out of 28 specific cookie names is it. so how we do it is through script which can do it by create `nano wordlist.txt`, which script i use for it [wordlist.txt](script.py)

3. Get cookie value
<br><br>

Now, go to website go to and right click and hit `inspect -> application -> storage -> cookie` which you should see vaule of cookie which copy that 

4. Find the Secret Key (Brute-Force)
which tool you install before will help you in next step (your need current cookie (from your browser) and the list of words you just made with `wordlist.txt`. which when run command it will run every word until find right one
<br><br>

Run this command: `flask-unsign --unsign --cookie 'eyJ2ZXJ5X2F1dGgiOiJibGFuayJ9.afJ_ow.kwC0cfqBSOOfe0efTFzRxajdXbg' --wordlist wordlist.txt`
<br?<br>

The result: will tell secrey key that for website

5. Forge the Admin Cookie
<br><br>

Now that you have the secret key, you can "sign" your own cookie and the server will believe it is real.
Run this command:
`flask-unsign --sign --cookie "{'very_auth': 'admin'}" --secret 'pinwheel`

The result: The terminal will give you a new long string, Copy it.

6. when you copy it go in website and `inspect -> application -> storage -> cookie`

after you that go to value in cookie and change value to secret key given then refresh website after that you should get the flag

