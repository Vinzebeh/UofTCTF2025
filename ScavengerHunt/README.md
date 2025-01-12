# Scavenger Hunt
## Challenge Description

![Screenshot 2025-01-12 175621](https://github.com/user-attachments/assets/b062af98-4ad6-47da-8169-bb7dd43b689f)

It was given a link to a webpage and the webpage looks like this:  
![Screenshot 2025-01-12 175134](https://github.com/user-attachments/assets/35e5b315-c653-4428-8672-6c9dd40df875)
After clicking the **Start Huntung** button, it shows
![Screenshot 2025-01-12 175143](https://github.com/user-attachments/assets/2123414c-d9fa-49d2-9d4d-cdcb394a3375)
This indicates that there are total 7 parts of flag that hidden inside the website and we need to find all parts to form a complete flag.  

  
## Solution
### Source Code Inspection
Inspect the source code of this website by pressing **F12** in your keyboard.  
**Part 1**  
![Screenshot 2025-01-12 175235](https://github.com/user-attachments/assets/9fec623a-3ffe-4b02-ae28-7f9ba5e9dbb4)  

**Part 5**  
![Screenshot 2025-01-12 175248](https://github.com/user-attachments/assets/3efcae2f-a0ed-4bd0-ab3f-95dd799b1581)    
______________________________________________________________________________________  
### Subdirectories  
![Screenshot 2025-01-12 175355](https://github.com/user-attachments/assets/3009bfb8-5ee4-455b-a6ad-4691d5333a2c)  
There is a comment line **sourceMappingURL=app.min.js.map**, so I decided to locate to the app.min.js.map subdirectory of the webpage  

**Part 7**
![image](https://github.com/user-attachments/assets/0dac56d9-6719-4c4d-8fd9-aab896b88e90)  
______________________________________________________________________________________  
### robots.txt
A robots.txt file tells search engine crawlers which URLs the crawler can access on your site.  
**Part 4**  
![Screenshot 2025-01-12 175439](https://github.com/user-attachments/assets/2ee237a3-6be0-486f-8f6f-f63ffa6c9fc1)  
By accessing robots.txt of the website, there is part 4 of the flag and also a subdirectory that disallowed from normal user. Therefore, I decided to go into the **/hidden_admin_panel** to get some info.    

As expected, access was denied inside the **/hidden_admin_panel**.  
![Screenshot 2025-01-12 175518](https://github.com/user-attachments/assets/1de68175-473d-44c2-8f3b-70a28dea209d)  
______________________________________________________________________________________  
### Cookies
Since only admin can access the **/hidden_admin_panel** and no login function in the webpage, the only way to access the webpage is by editing the cookie's value.  
**Part 3**  
![Screenshot 2025-01-12 175530](https://github.com/user-attachments/assets/269f5090-daa2-4193-993f-ab0af625753d)  
Inside the cookie tab, there is a flag_part3 cookie and a guest user cookie.  

**Part 6**  
![Screenshot 2025-01-12 175546](https://github.com/user-attachments/assets/785bcf96-c2ae-4405-8310-e55433fa136d)  
Edit the guest cookie value to admin and refresh the page, the part 6 will be visible now.  
______________________________________________________________________________________  

### Network
I have been finding part 2 of the flag for a while, then when I inspect the network tab on this webpage, I found something weird...  
**Part 2**  
![image](https://github.com/user-attachments/assets/dcf54d07-64a9-44df-8368-58a63029d6f5)  
______________________________________________________________________________________  

From now on, we have collected all 7 parts of the flag, yeahh!!  

## Challenge Flag  
uoftctf{ju57_k33p_c4lm_4nd_1n5p3c7_411_7h3_4pp5_50urc3_c0d3!!}



