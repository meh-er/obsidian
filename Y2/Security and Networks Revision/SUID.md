#SaN 

The **Saved UID (SUID)** acts as a 'privilege backup' for the EUID. IT is initialised when the process **starts** and **stores a copy** of the EUID at **execution time**. This allows the process to temporarily drop privileges (by changing EUID) and later **safely regain them** using the saved value.  
  
Purpose  

- **Privilege Reclamation**: Enables process to drop EUID to a lower-privilege UID for security, then restore EUID to the saved value when needed.  
    
- **Prevents Permanent Loss of Privileges**: Without SUID, a process that drops EUID (e.g. from root to a user) could not regain root privileges later.