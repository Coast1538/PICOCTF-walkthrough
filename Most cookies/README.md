# [Most Cookies](https://play.picoctf.org/practice/challenge/177)

## Problem Statement
Alright, enough of using my own encryption. Flask session cookies should be plenty secure!
Additional details will be available after launching your challenge instance.

## Hint
1. How secure is a Flask cookie?

## Solution

### 1. Install the Cracking Tool

On Kali Linux, you need a tool that can read and "re-sign" Flask cookies:

open termical and put in this 
```bash
pip3 install flask-unsign[wordlist] --break-system-packages
```

**Explanation:**
- `pip3` installs packages
- `flask-unsign` is the tool
- `[wordlist]` adds wordlist support
- `--break-system-packages` forces installation

### 2. Create the "Guessing" Wordlist

This is the most important part. The server needs a "secret key," and one of 28 specific cookie names is it. Create a wordlist by running:

```bash
nano wordlist.txt
```

**Explanation:**
- `nano` is a text editor
- `wordlist.txt` is the file you're creating to store potential secret keys

Use this [wordlist.txt](script.py) script, which contains 28 cookie names and displays them.

### 3. Get Cookie Value

Go to the website, right-click, and select **Inspect → Storage → Cookies**. You should see the cookie value. Copy it.

**Explanation:**
- `Inspect` opens the browser's developer tools
- `Application` tab shows stored data like cookies
- `Storage → Cookies` displays all cookies for the current website

### 4. Find the Secret Key (Brute-Force)

The tool you installed will help with this step. You'll need the current cookie from your browser and the wordlist you created. The command will test every word until it finds the right one.

Run this command:

```bash
flask-unsign --unsign --cookie '(cookie value you got from website)' --wordlist wordlist.txt
```

**Explanation:**
- `flask-unsign` is the cracking tool you installed
- `--unsign` tells it to try to crack/decode the cookie
- `--cookie '(cookie value you got)'` is the cookie string you copied from your browser
- `--wordlist wordlist.txt` tells it which wordlist file to use for guessing

The result will show the secret key for the website.

### 5. Forge the Admin Cookie

Now that you have the secret key, you can "sign" your own cookie, and the server will believe it is real.

Run this command:

```bash
flask-unsign --sign --cookie "{'very_auth': 'admin'}" --secret '(the cookie it give you on step 4)'
```

**Explanation:**
- `flask-unsign` is the tool you installed
- `--sign` tells it to create/forge a new cookie (opposite of `--unsign`)
- `--cookie "{'very_auth': 'admin'}"` is the cookie content you want to forge (claiming you're an admin)
- `--secret 'pinwheel'` is the secret key you discovered in step 4

The terminal will output a new long string. Copy it.

### 6. Replace the Cookie Value

Go to the website and select **Inspect → Storage → Cookies**. Replace the cookie value with the new signed cookie you just created in terminal, then refresh the website. You should get the flag.

