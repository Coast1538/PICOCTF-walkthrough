[JaWT Scratchpad](https://play.picoctf.org/practice/challenge/25)

## problem statement
Check the admin scratchpad!
Additional details will be available after launching your challenge instance.

## Hint
1. What is that cookie?
2. Have you heard of JWT?


## Solution
1. Open Burp Suite
2. when you open burpsuite `go to proxy →  turn on intercept → then open browser`
3. After you open browner put in website the JaWT Scratchpad Give you and make sure you press forward every time you do 
4. After you are on website put anything in log in access page and press enter (remember to press forward in burpsuite)
5. after that go to `extensions → BApp Store → download JWT Editor` after you download the JWT editor go to it (it to the right of extensions tab)
6. after that make press Symmetric Key than press generate key
7. after that go cyberchef and get “to base64” than put “ilovepico” into it
8. after that go back to Symmetric key you generator and put base64 encryption you got into k (it should look like this)
9. after you do that go back to website on burpsuite and refresh the  page (remember to press forward in burpsuite)
10. after you do that go HTTP history and right click the tag that all the way the bottom make sure it has
`method as GET 
URL as / 
and is green` 
11. after you do that right click it press send to Repeater
12. after you send it to the Repeater go to Repeater
13. after you do that go to JSON Web token and change the payload with user name to `admin`
14. after you do that press sign all the button than click ok
15. after you do all that press SEND and you should get a Response
16. after you get Response go to search tab at bottom and look up pico
17. after you do all that you should get the flag
