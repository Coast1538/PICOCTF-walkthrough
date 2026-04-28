

Step 1: Access the Site
Open up the challenge website: http://picoctf.net:?????
Step 2: Head to Admin
Click the menu button (the one with the three horizontal lines) and navigate to the Admin Login page.
Step 3: Inspect the Page
Right-click on the page and select Inspect. Go to the Elements tab and hit Ctrl + F to bring up the search bar.
Step 4: Turn on Debugging
Search for "debug" in the search bar. Find the line for the debug name and change value="0" to value="1".
Step 5: Check for Encryption
Enter any random password and hit enter. If you look closely at the debug output, the text looks like ROT13. This tells us the server is rotating our input.
Step 6: Inject the Payload
Go back to the login page. Since the server is using ROT13, you need to "pre-rotate" your SQL injection. Enter ' BE 1=1; as the password. Because of the rotation, the server will read this as ' OR 1=1;.
Step 7: Get the Flag
Submit it, and the flag should be yours!
