# Racing 1
## Challenge Description
![Screenshot 2025-01-12 175634](https://github.com/user-attachments/assets/b056fb80-131c-4b0c-8592-4538fa446141)  

![Screenshot 2025-01-12 175802](https://github.com/user-attachments/assets/456ad84a-8952-4f95-bd89-8f3161048e72)  
After connecting to the machine through ssh, I do ls to list all files and search for any file that might stores a flag. Then, I try to cat the **flag.txt** but it did not work.   
Only admin or super user has the read permission on **flag.txt**.  
  
**Given Source Code:**
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

int main(int argc, char **argv)
{
    if (setuid(0) != 0)
    {
        perror("Error setting UID");
        return EXIT_FAILURE;
    }

    char *fn = "/home/user/permitted";
    char buffer[128];
    char f[128];
    FILE *fp;

    if (!access(fn, R_OK))
    {
        printf("Enter file to read: ");
        fgets(f, sizeof(f), stdin);
        f[strcspn(f, "\n")] = 0;

        if (strstr(f, "flag") != NULL)
        {
            printf("Can't read the 'flag' file.\n");
            return 1;
        }

        if (strlen(f) == 0)
        {
            fp = fopen(fn, "r");
        }
        else
        {
            fp = fopen(f, "r");
        }

        fread(buffer, sizeof(char), sizeof(buffer) - 1, fp);
        fclose(fp);
        printf("%s\n", buffer);
        return 0;
    }
    else
    {
        printf("Cannot read file.\n");
        return 1;
    }
}
```
The given source code basically means the program will only run if the file directory **/home/user/permitted** is readable and it will prompt user for a file to read

## Solution
![Screenshot 2025-01-13 000118](https://github.com/user-attachments/assets/ac03f497-495f-4af0-844a-2f3911f707be)  
I created a symbolic link between **/flag.txt** and **/home/user/permitted** in order to run the **chal** program in the **/challenge** directory.  

![Screenshot 2025-01-13 000135](https://github.com/user-attachments/assets/e536f449-a9e3-4fe7-90d6-68a306fa989f)  
When executing the program, it prompt us a file directory to read which will be the **/home/user/permitted**. This is because the file directory has a symlink with the **/flag.txt**.
When the program read the **/home/user/permitted**, it will set the uid to 0 which is root and you will be able to read the **flag.txt** file.  

## Challenge Flag
uoftctf{r4c3_c0d1t10n5_4r3_c00l}
