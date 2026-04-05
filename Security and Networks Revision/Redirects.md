#SaN 

## Unvalidated redirects and forwards
- WEb apps often allow ***redirections*** which
	- Send users off-site with a polite message
	- Reroute them immediately
- or *forwards* which
	- redirect internally to different parts of the same site
- Attackers can craft URLs that **fool users**
- These kind of **open redirect** links are favourites for phishing attacks, especially as ultimate destinations can be concealed in URL encodings.
- So, preventing open redirects is a typical example of a **community-wide** desirable security measure - good practice of all provides security for others.