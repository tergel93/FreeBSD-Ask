# 第五节 通过源代码 ports 方式安装软件


>**注意**
>
>ports 和 pkg 可以同时使用，大部分人也是这么用的。但是要注意 pkg 的源必须是 latest，否则会存在一些依赖上比如 lib 库上的问题。latest 的源也比主线上的 ports 要出来的晚（是从中编译出来的），因此即使是 latset 源也可能会出现上述问题，总之有问题出现时就卸载那个 pkg 安装的包，重新使用 ports 编译即可。

## FreeBSD ports 基本用法

>**警告**
>
>FreeBSD 关于在未来弃用 portsnap 的说明：<https://marc.info/?l=freebsd-ports&m=159656662608767&w=2>。
>
>以下是邮件翻译：
>
>我们正计划废除在 ports 中使用 portsnap 的做法。
>
>原因如下 (无特定排序)。
>
>* Portsnap 不支持季度分支，即使在季度分支被创建并改为非 HEAD 软件包的默认值的多年之后。
>
>* 与 svn 或 git 相比，Portsnap 似乎并不节省磁盘空间，如果你算上元数据（存储的）的话。算上元数据（默认存储在 /var/db/portsnap 中），并且你对 svn 或 git 做一个没有历史记录的相同的比较，并且忽略可能的 ZFS 压缩。也就是说，你用 `svn export` 或 `git clone --depth 1`，你会看到这样的磁盘用量：
>
>```
>     342M svnexport
>     426M git
>     477M portsnap
>```
>
>* Portsnap 也不像 git 那样可以离线工作。使用 git，你可以 也可以通过运行 `git pull --unshallow` 轻松添加历史记录。
>
>* 这种从 portsnap 的迁移与计划中的向 git 的迁移很相称。
>
>* 另外，根据我们在 Bugzilla 上看到的补丁，使用使用 portsnap 导致人们很容易意外地提交补丁到 Bugzilla，而这些补丁并不容易应用。
>
>* 由于 portsnap 不支持季度分支，它经常导致用户在错误的分支上进行编译，或最终使用不匹配的软件包。也就是说，他们通过 pkg 从季度分支安装软件包，然后想要定制，因此运行 portsnap 并从 head 编译，这可能会导致问题。正如我们经常看到的那样。即使这种情况没有发生，也会增加故障排除的几率，以确认它没有发生。
>
>我们知道人们已经习惯了 portsnap，但我们相信：
>
>* 人们应该能够轻松地使用在基本系统或 git 来使用 pkg 的 svnlite。(似乎很少有人真正使用 WITHOUT_SVNLITE)。
>
>* 也有可能退回到来获取 tar 或 zip。从 <https://cgit-beta.freebsd.org/ports/>，尽管这确实使更新难度增加。
>
>我们将如何做，按顺序进行：
>
>* 更新 poudriere 以默认使用 svn。这已经完成了：
>
>https://github.com/freebsd/poudriere/pull/764
> 
>https://github.com/freebsd/poudriere/commit/bd68f30654e2a8e965fbdc09aad238c8bf5cdc10
>
>* 更新文档，不再提及 portsnap。这项工作已经在进行中了：
>
>   https://reviews.freebsd.org/D25800
>   
>   https://reviews.freebsd.org/D25801
>   
>   https://reviews.freebsd.org/D25803
>   
>   https://reviews.freebsd.org/D25805
>   
>   https://reviews.freebsd.org/D25808
>   
>   https://svnweb.freebsd.org/changeset/base/363798
>
>   非常感谢那些已经和正在从事这项工作的人们！
>
>* 让 WITHOUT_PORTSNAP 成为默认的基本系统参数。目前还不确定这一点何时会发生。可能在 13.0 之前不会发生，但希望它能生效。
>
>* 最终，portsnap 服务器的使用率会低至可以被禁用。
>
>我们欢迎任何有建设性的反馈。所有的意见都会被听取，如果计划需要修改，我们会在几周内把修改后的计划反馈给你。这个过程将需要一些时间，但希望不会对任何人的正常工作流程造成太大的干扰。
>
>Steve (portmgr@)


### 首先获取 portsnap

`# portsnap auto`

### 使用 whereis 查询软件路径

如 `# whereis python`

输出 `python: /usr/ports/lang/python`

### 如何安装 python3：

```
# cd /usr/ports/lang/python
# make BATCH=yes clean
```

其中 BATCH=yes 的意思是使用默认配置

## FreeBSD ports 多线程编译（推荐）

Linux 如 gentoo 上一般是直接 `-jx` 或者 `jx+1`, `x` 为核心数。

FreeBSD ports 多线程编译

```
FORCE_MAKE_JOBS=yes
MAKE_JOBS_NUMBER=4
```

写入 `/etc/make.conf` 没有就新建。

`4` 是处理器核心数（还是线程数？），不知道就别改。英特尔的处理器搜索 `CPU型号+ARK` 转跳英特尔官网可查询线程数。

### 如何使用多线程下载：

>**警告**
>
>**注意此小节内容不再对 FreeBSD 13 有效，在 2022-10-11 日 axel 由于上游长期停止开发[被移除了](https://www.freshports.org/ftp/axel/)。推荐使用 `www/aria2`**


~`# pkg install axel #下载多线程下载工具#`~

~新建或者编辑 `# ee /etc/make.conf` 文件，写入以下两行：~


```
FETCH_CMD=axel
FETCH_BEFORE_ARGS= -n 10 -a
FETCH_AFTER_ARGS=
DISABLE_SIZE=yes
```


### 进阶

如果不选择 `BATCH=yes` 的方法手动配置依赖：

看看 python 的 ports 在哪：

```
# whereis python
# python: /usr/ports/lang/python
```

安装python3：

`# cd /usr/ports/lang/python`

如何设置全部所需的依赖：

`# make config-recursive`

如何删除当前 port 的配置文件：

`# make rmconfig`

如何一次性下载所有需要的软件包：

`# make BATCH=yes fetch-recursive`

升级 ports

`# portsnap auto

ports 编译的软件也可以转换为 pkg 包

`# pkg create nginx`

### FreeBSD 包升级管理工具

首先更新 Ports 

```
# portsnap auto
```

然后列出过时 Ports 组件
```
# pkg_version -l '<'
```
下边分别列出 2 种 FreeBSD 手册中提及的升级工具:

一、portupgrade

```
# cd /usr/ports/ports-mgmt/portupgrade && make install clean
# portupgrade -ai #自动升级所有软件
# portupgrade -R screen #升级单个软件
```

二、portmaster （推荐）

```
# cd /usr/ports/ports-mgmt/portmaster && make install clean
# portmaster -ai #自动升级所有软件
# portmaster screen #升级单个软件
# portmaster -a -m "BATCH=yes" #或者-D -G –no-confirm 都可以免除确认
```
