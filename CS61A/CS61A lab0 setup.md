---
link: https://www.notion.so/CS61A-lab0-setup-2bd71fa0dca64cccb1021c8ee98d14bb
notionID: 2bd71fa0-dca6-4ccc-b102-1c8ee98d14bb
---
https://www.bilibili.com/video/BV1s3411G7yM/?p=3&spm_id_from=pageDriver&vd_source=f46fe1487e2cdbb08f85ea89fd2cbbf0

# 查看TLS版本
```
from json import loads; from urllib.request import urlopen; loads(urlopen('https://www.howsmyssl.com/a/check').read().decode('UTF-8'))['tls_version']
```

测试