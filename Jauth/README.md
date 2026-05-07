# [Jauth](https://play.picoctf.org/practice/challenge/177)

## Problem Statement
Authenticate as an admin user to access protected resources.

## Hints
1. What is that cookie?
2. Have you heard of JWT (JSON Web Tokens)?

## Solution

### Step 1: launch Burp suite

1. Launch Burp Suite
2. Click **Next → Start Burp**
3. Go to **Proxy → turn Intercept is on → Open browser** to launch Burp's built-in browser

### Step 2: Access the Challenge Website

1. In Burp's browser, paste the Jauth challenge URL 
3. after that Go back to Burp Suite's **Proxy** tab and click **Forward** for each request done (when website need to update)

### Step 3: Login with Provided Credentials

1. On the Jauth login page, you should put credentials:
   - **Username:** `test`
   - **Password:** `Test123!`
2. click **Login** after you put it in
4. The server will respond with a JWT cookie in the response headers

### Step 4: Capture the JWT Cookie

1. In Burp Suite, go to **HTTP History**
2. Find the most recent request (usually at the **bottom**)
3. Look for a request with:
   - **URL:** `/private` 
5. Right-click the request and select **Send to Repeater**

### Step 5: Install JWT Editor Extension (If you don't have it)

1. In Burp Suite, go to **Extensions → Bapp Store → JWT editor → insatall** 
5. The extension will now appear in your Extensions tabs

### Step 6: Craft the Admin JWT

2. Go to the **Repeate → JSON web token** tab
2. Click the **Payload** section
3. Change `"role":"user"` to `"role":"admin"`
4. after doing that press **attack → change algorithm to none**
5.. Click **Send** 
6. If the signature is valid, the server will accept your request as an admin

### Step 10: Access Admin Resources and Get the Flag
1. Look at the **Response** from the request with the admin JWT
2. You should now have access to admin-only content
3. Search the response for `pico` by `Ctril + f` or by look for a flag in the page content
4. which then you should get the picoCTF{This_is_not_the_flag}

      
