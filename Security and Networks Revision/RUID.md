#SaN 

The **Real UID (RUID)** is the UID of the user who **started the process**. It identifies the 'original' user behind the process and is typically set when the process is created, it rarely changes afterwards.  
  
Purpose:  

- **Audit Trail**: Tracks who initiated the process  
    
- **Identity Anchor**: Serves as a fixed reference to the user, even if privileges change dynamically