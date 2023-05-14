# 1 下载
[MySQL官网](https://www.mysql.com/)  
先进官网下载所需版本Mysql

# 2 解压缩
自行解压到自己要存放MySQL的盘

# 3  配置

进入解压好的MySQL文件夹----查看有无my.ini文件（只看到my或者无法修改my文件后缀的，点击左上方查看，勾选文件扩展名）  
将以下配置信息复制粘贴到my.ini文件中
![](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202305141149438.png)
**注意：basedir以及datadir填自己MySQL存放的路径**

```
[mysqld]
# 设置3306端口
port=3306
# 设置mysql的安装目录   ----------是你的文件路径-------------
basedir=D:\DB\mysql-8.0.31-winx64
# 设置mysql数据库的数据的存放目录  ---------是你的文件路径data文件夹自行创建
#datadir=D:\DB\mysql\data
# 允许最大连接数
max_connections=200
# 允许连接失败的次数。
max_connect_errors=10
# 服务端使用的字符集默认为utf8mb4
character-set-server=utf8mb4
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
# 默认使用“mysql_native_password”插件认证
#mysql_native_password
default_authentication_plugin=mysql_native_password
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8mb4
[client]
# 设置mysql客户端连接服务端时默认使用的端口
port=3306
default-character-set=utf8mb4
```

# 4  新建系统环境变量
此电脑→属性→高级系统配置→环境变量→新建系统变量

如果遇到以下问题：
![](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202305141150782.png)
可以用这个办法解决：
![image.png](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202305141151680.png)
相同的前缀进行聚合
