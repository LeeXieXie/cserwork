**在 `win11` 系统中运行 `ws2 子系统`出现以下问题：**

> 占位程序接收到错误数据。 Error code: Wsl/Service/0x800706f7 Press any key to continue...

解决方案： 用管理权限打开 `cmd` 命令窗口，执行以下代码：
```shell
netsh winsock reset
```

然后重新进入 `ubuntu wsl2 子系统`即可，无需重启计算机。