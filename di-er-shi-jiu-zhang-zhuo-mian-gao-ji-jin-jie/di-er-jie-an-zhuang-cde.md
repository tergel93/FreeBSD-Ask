# 第二节 安装 CDE

>**CDE 是通用桌面环境的缩写。历史悠久的桌面环境，常被用于商业的 Unix 发行版。**

## 安装软件依赖

在 shell 中执行：

```
# pkg install -y xorg iconv bdftopcf libXScrnSaver ksh93 open-motif tcl86 xorg-fonts xorg-fonts-100dpi cde
```

## 开启各项服务

1. 在 shell 中执行：

   ```
   # sysrc rpcbind_enable="YES"
   # sysrc dtspc_enable="YES"
   # sysrc dtcms_enable="YES"
   # ln -s /usr/local/dt/bin/Xsession ~/.Xsession 
   # env LANG=C startx
   ```

   需要用哪个用户登录 CDE，就用哪个用户执行最后两行。

2. 将以下内容追加到 `/etc/rc.local`

   ```
   /usr/local/dt/bin/dtlogin
   ```

3. 重启系统。
