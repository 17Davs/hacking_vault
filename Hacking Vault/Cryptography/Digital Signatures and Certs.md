   

Digital Signatures and Certs

Digital Signatures and Certs

### What’s a Digital Signature?

Digital signatures provide a way to verify the authenticity and integrity of a digital message or document. Proving the authenticity of files means we know who created or modified them. Using asymmetric cryptography, you produce a signature with your private key, which can be verified using your public key. Only you should have access to your private key, which proves you signed the file. In many modern countries, digital and physical signatures have the same legal value.

The simplest form of digital signature is encrypting the document with your private key. If someone wants to verify this signature, they would decrypt it with your public key and check if the files match. This process is shown in the image below.

![An example of signing a message: Bob encrypts a message with his private key and Alice decrypts it with Bob's public key.](Hacking%20Vault/Attachments/71bf3562b5364e1e91ed46f3dd34b5c0.svg)

Some articles use terms such as electronic signature and digital signature interchangeably. They refer to pasting an image of a signature on top of a document. This approach does not prove the document’s integrity, as anyone can copy and paste an image.

In this task, we use the term _digital signature_ to refer to signing a document using a private key or a certificate. This process is similar to the image shown above, where Bob encrypts a hash of his document and shares it with Alice, along with the original document. Alice can decrypt the encrypted hash and compare it with the hash of the file she received. This approach proves the document’s integrity, unlike pasting a fancy image of a signature. We will cover hashing in the [Hashing Basics](https://tryhackme.com/r/room/hashingbasics "https://tryhackme.com/r/room/hashingbasics") room.

### Certificates: Prove Who You Are!

Certificates are an essential application of public key cryptography, and they are also linked to digital signatures. A common place where they’re used is for HTTPS. How does your web browser know that the server you’re talking to is the real tryhackme.com?

The answer lies in certificates. The web server has a certificate that says it is the real tryhackme.com. The certificates have a chain of trust, starting with a root CA (Certificate Authority). From install time, your device, operating system, and web browser automatically trust various root CAs. Certificates are trusted only when the Root CAs say they trust the organisation that signed them. In a way, it is a chain; for example, the certificate is signed by an organisation, the organisation is trusted by a CA, and the CA is trusted by your browser. Therefore, your browser trusts the certificate. In general, there are long chains of trust.

you can get your own TLS certificates for domains you own using [Let's Encrypt](https://letsencrypt.org/ "https://letsencrypt.org/") for free. If you run a website, it’s worth setting up and switching to HTTPS, as any modern website would do.