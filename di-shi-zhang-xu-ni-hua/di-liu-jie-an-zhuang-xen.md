# 第六节 安装 XEN



XEN 是一种虚拟化技术。Xen 项目管理程序是一个开源的第一类或裸管理程序。它使在一台机器（或主机）上并行运行一个操作系统的许多实例或不同的操作系统成为可能。不同的操作系统在一台机器（或主机）上并行运行。Xen 项目的管理程序是作为开源的软件来说的唯一的第一类管理程序。它被用作许多不同的商业和开源应用的基础。成为开源应用的基础，例如：服务器虚拟化、基础设施即服务（IaaS）、桌面虚拟化(IaaS)、桌面虚拟化、安全应用、嵌入式和硬件设备。——<https://www.freshports.org/emulators/xen-kernel>

## 安装

```
# pkg install -y xen-kernel xen-tools
```

## 参考资料

 - <https://wiki.freebsd.org/Xen>
 - <https://handbook.bsdcn.org/di-22-zhang-xu-ni-hua/22.7.-shi-yong-freebsd-shang-de-xen-xu-ni-ji.html>
