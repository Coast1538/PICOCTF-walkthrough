# [Jauth](https://play.picoctf.org/practice/challenge/177)

## Problem Statement
Authenticate as an admin user to access protected resources.

## Hints
1. What is that cookie?
2. Have you heard of JWT (JSON Web Tokens)?

## Key Concepts
- **JWT (JSON Web Token)**: A secure way to transmit user information between client and server
- **JWT Components**: Header.Payload.Signature
  - **Header**: Token type and hashing algorithm
  - **Payload**: User claims (username, role, permissions, etc.)
  - **Signature**: Cryptographic signature to verify authenticity
- **Cookie Security**: If the secret key is weak or known, attackers can forge valid tokens
- **Role Escalation**: Changing the `role` claim from `user` to `admin` can grant unauthorized access

## Solution

### Step 1: Setup Burp Suite
1. Launch Burp Suite
2. Click **Next** → **Start Burp**
3. Go to **Proxy** tab
4. Enable **Intercept is on** toggle
5. Click **Open browser** to launch Burp's built-in browser

### Step 2: Access the Challenge Website
1. In Burp's browser, paste the Jauth challenge URL
2. The browser will begin intercepting requests
3. Go back to Burp Suite's **Proxy** tab and click **Forward** for each request
4. Continue until you reach the Jauth login page

### Step 3: Login with Provided Credentials
1. On the Jauth login page, you should see credentials:
   - **Username:** `test`
   - **Password:** `Test123!`
2. Enter these credentials and click **Login**
3. In Burp Suite, click **Forward** on the login request
4. The server will respond with a JWT cookie in the response headers
5. **Note the JWT**: It will be in a `Set-Cookie` header and contain three Base64-encoded parts separated by dots

### Step 4: Capture the JWT Cookie
1. In Burp Suite, go to **HTTP History**
2. Find the most recent request (usually at the **bottom**)
3. Look for a request with:
   - **URL:** `/private` or similar protected resource
   - **Method:** GET or POST
4. In the response, you should see the JWT in the `Set-Cookie` header
5. Right-click the request and select **Send to Repeater**

### Step 5: Install JWT Editor Extension
1. In Burp Suite, go to **Extensions** tab
2. Click **BApp Store**
3. Search for **JWT Editor**
4. Click **Install**
5. The extension will now appear in your Extensions tabs

### Step 6: Examine and Decode the JWT
1. Go to the **Repeater** tab
2. Look at the HTTP response from the login request
3. Find the JWT token in the `Set-Cookie` header
4. Copy the JWT token (the part between `auth=` and the semicolon)
5. Open the **JWT Editor** extension
6. Click the **Decoder** tab
7. Paste the JWT and click **Decode**

### Step 7: Analyze the Payload
The decoded JWT should show:
- **Header**: `{"alg":"HS256","typ":"JWT"}`
- **Payload**: Something like `{"username":"test","role":"user"}`
- **Signature**: The cryptographic signature

**Goal**: Change `"role":"user"` to `"role":"admin"`

### Step 8: Craft the Admin JWT
1. In the **Repeater** tab, click on the **JSON Web Token** tab
2. Click the **Payload** section
3. Change `"role":"user"` to `"role":"admin"`
4. Change the algorithm if needed (find what algorithm the server uses - typically `HS256`)
5. Click the **Sign** button
6. The extension will sign the token with the (possibly weak) secret key
7. If successful, you'll get a new signed JWT

### Step 9: Send the Forged JWT
1. In the **Repeater** tab, replace the old JWT cookie with the new one
2. Modify the request to include your new JWT in the `Cookie` header
3. Click **Send**
4. If the signature is valid, the server will accept your request as an admin

### Step 10: Access Admin Resources and Get the Flag
1. Look at the **Response** from the request with the admin JWT
2. You should now have access to admin-only content
3. Search the response for `pico` or look for a flag in the page content
4. The flag should be visible in the response

## Vulnerability Explanation

**Weak Secret Key**: The JWT is likely signed with a weak or guessable secret (like an empty string, common words, or simple patterns). By modifying the payload to claim `"role":"admin"` and signing it with the weak secret, you can impersonate an admin without knowing the actual password.

## Security Lessons
- ✅ Use strong, cryptographically random secret keys
- ✅ Validate JWT signatures on every request
- ✅ Store secrets securely (never hardcode them)
- ✅ Use HTTPS to prevent cookie interception
- ✅ Implement proper role-based access control (RBAC) on the server side
