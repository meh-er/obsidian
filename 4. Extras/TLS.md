#Theory 
Transport Layer Security is a cryptographic protocol. It provides security, privacy, integrity and authenticity, using certificates between two or more computer applications. It runs in the presentation layer.
It builds on the deprecated Secure Socket Layer (SSL)
The client must request server set up a TLS connection (often using a different port number, e.g. HTTP port 80, HTTPS port 443)
It uses a handshake with an asymmetric cipher to establish a session-specific shared key, further communication is then encrypted using a symmetric cipher.
The server usually provides identification using a digital certificate.