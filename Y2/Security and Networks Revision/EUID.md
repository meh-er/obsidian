#SaN 

The **Effective UID** (**EUID)**is the UID the kernel uses to **check permissions** when the process performs actions like reading files, opening network ports, or modifying system settings. In most cases it matches RUID.  
  
Purpose  

- **Permission Enforcement**: Dictates what the process is allowed to do (e.g. can x process write to y file)  
    
- **Privilege Flexibility**: Allows processes to temporarily gain or drop privileges without changing their underlying identity (RUID)
