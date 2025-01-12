# Funny Cipher
## Challenge Description

![Screenshot 2025-01-12 180736](https://github.com/user-attachments/assets/efbbb980-e277-4629-bf0d-4bf400f27116)

It was given a cipher text :  
__60_ZMZ_GBWKNREM_KRA__LQM}WEPRGQL__Q_{RWW_M_KIAGPMNMRXDLM_FMWLDQ0BOIAMNPG_


## Solution 
As the challenge description has mentioned **wheelburrow**, I search through the internet and find out there is a cipher decryptor called **Burrows-Wheeler Transform**  
Link: https://www.dcode.fr/burrows-wheeler-transform  
  
After Decrypting the cipher text, it will have 4 results  
![image](https://github.com/user-attachments/assets/b12a28db-f737-4145-b991-f53d28b93afa)

By comparing the flag format **uoftctf{}**, you will find out only the second's result match to the format
After analyzing the cipher text, I assume it will be some kind of substitution cipher, so I decided to throw it into [quipquip](https://quipqiup.com/) and give it a clue _LWPMGMP = uoftctf_  

![image](https://github.com/user-attachments/assets/15acd663-c1ca-4dde-ad29-907f3d7ed836)

![image](https://github.com/user-attachments/assets/7680c20a-c236-4e07-93a3-20ef1676d6da)
The first will be the result as the others did not form english words. However, when I submit the flag it was incorrect. So I look back to the cipher text and noticed that there was a **600** being left out from the decrypted result. After adding the 600 back, the challenge solved :D.

## Challenge flag 
uoftctf{did_you_know_the_first_substitution_cipher_dates_back_to_600_bc}


