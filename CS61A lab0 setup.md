https://www.bilibili.com/video/BV1s3411G7yM/?p=3&spm_id_from=pageDriver&vd_source=f46fe1487e2cdbb08f85ea89fd2cbbf0

# 查看TLS版本
```
from json import loads; from urllib.request import urlopen; loads(urlopen('https://www.howsmyssl.com/a/check').read().decode('UTF-8'))['tls_version']
```

测试