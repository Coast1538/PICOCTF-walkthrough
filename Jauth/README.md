Jauth walkthrough

1. make sure to launches the website instance on demand.
2. after doing that go burpsuite since we need jwt edior for this one (if you have jwt edior you won't need this step but this way i did it)
3. when open burp suite perss -> next -> start burp since we don't need to worry about other stuff
4. after it lautch go to proxy -> turn on interecpt -> open browser
5. <img width="1631" height="910" alt="image" src="https://github.com/user-attachments/assets/625687c2-a4bb-48bd-ad72-d2ee0afa58c4" />

6. after you open brower put the website by right click -> copy link addresss then put on burpsuirte brower (which after you paste website make sure to back to proxy and foward it you need to do this for every action that update website)
7. <img width="1610" height="895" alt="image" src="https://github.com/user-attachments/assets/ac894bdf-94eb-4374-a1ca-e5a71999d8de" />

8. <img width="1916" height="914" alt="image" src="https://github.com/user-attachments/assets/63b8887f-46e8-48e9-a1a3-a73ff00cd708" />
9. this how website should look like and need put username and password the thing provide which is
   username: test
    password Test123!
10.  after you put in username and password and forawt it it should look like this
11.  <img width="1912" height="903" alt="image" src="https://github.com/user-attachments/assets/21e1cece-01b4-4385-b618-57859f9b5049" />
12. go back to burpsuite -> HTTP history then find the most recent time (always on bottom) or one that has /private
13. after you do that right click it and hit send to repeater
14. if you have after that you need to install jwt editor by going to extenstions -> Bapp Store -> JWT editor -> install <img width="1904" height="1014" alt="image" src="https://github.com/user-attachments/assets/62a6c01d-6a5a-454b-8f2a-cfa115b5719a" />
15. when you do this go to repeater -> JSON web token
16. when do this you need to change attack tgsdgsdgsdgsd and role: user -> role: admin to think your admin and not take to long to find algorithm
17. <img width="779" height="869" alt="image" src="https://github.com/user-attachments/assets/2f0bda96-2ee7-4865-8101-64189cfa4d48" />

