# [Jauth](https://play.picoctf.org/practice/challenge/236)

## Problem Statement
Most web application developers use third party components without testing their security. 
Some of the past affected companies are:

-Equifax (a US credit bureau organization) - breach due to unpatched Apache Struts web framework CVE-2017-5638

-Mossack Fonesca (Panama Papers law firm) breach - unpatched version of Drupal CMS used

-VerticalScope (internet media company) - outdated version of vBulletin forum software used

Can you identify the components and exploit the vulnerable one?
Additional details will be available after launching your challenge instance.

## Hints
1. Use the web browser tools to check out the JWT cookie.
2. The JWT should always have two (2) . separators.

## Solution

### Step 1: Launch Burp Suite

1. Launch Burp Suite
2. Click **Next → Start Burp**
3. Go to **Proxy → turn Intercept on → Open browser** to launch Burp's built-in browser

### Step 2: Access the Challenge Website

1. In Burp's browser, paste the Jauth challenge URL
2. Go back to Burp Suite's **Proxy** tab and click **Forward** for each request made (when the website needs to update)

### Step 3: Login with Provided Credentials

1. On the Jauth login page, enter the following credentials:
   - **Username:** `test`
   - **Password:** `Test123!`
2. Click **Login** after entering them
3. The server will respond with a JWT cookie in the response headers

### Step 4: Capture the JWT Cookie

1. In Burp Suite, go to **HTTP History**
2. Find the most recent request (usually at the **bottom**)
3. Look for a request with:
   - **URL:** `/private`
4. Right-click the request and select **Send to Repeater**

### Step 5: Install JWT Editor Extension (If you don't have it)

1. In Burp Suite, go to **Extensions → Bapp Store → JWT editor → Install**
2. The extension will now appear in your Extensions tabs

### Step 6: Craft the Admin JWT

1. Go to the **Repeater → JSON web token** tab
2. Click the **Payload** section
3. Change `"role":"user"` to `"role":"admin"`
4. After doing that, press **Attack → Change algorithm to none**
5. Click **Send**
6. If the signature is valid, the server will accept your request as an admin

### Step 7: Access Admin Resources and Get the Flag

1. Look at the **Response** from the request with the admin JWT
2. You should now have access to admin-only content
3. Search the response for `pico` using `Ctrl + F` or look for a flag in the page content
4. You should then get the `picoCTF{This_is_not_the_flag}`
