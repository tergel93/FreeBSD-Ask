# 第一节 游戏

## 经典游戏

### 五分钟游戏

注：斜体为暂未打包的游戏

|       | Gnome/GTK          | KDE/Qt      | 备注      |
|:-----:|:------------------:|:-----------:|:-------:|
| 数独    | gnome-sudoku       | ksudoku     | 逻辑/益智游戏 |
| 数壹    | hitori             |             | 逻辑/益智游戏 |
| 扫雷    | gnome-mines        | kmines      | 益智游戏    |
| 2048  | gnome-2048         | 2048-qt     | 益智游戏    |
| 贪吃蛇   | gnome-nibbles      |             | 休闲游戏    |
| 国际象棋  | gnome-chess        | knights     | 益智游戏    |
| 五子棋   |                    | bovo        | 益智游戏    |
| 拼图    | gnome-taquin       |             | 益智游戏    |
| 配对拼图  | gnome-tetravex     |             | 益智游戏    |
| 对对碰   | gnome-mahjongg     | *kajongg*   |         |
| 俄罗斯方块 | quadrapassel       | kblocks     | 限时消除类游戏 |
| 机器人   | gnome-robots       |             |         |
| 黑白棋   | iagno              | kreversi    | 翻转棋     |
| 吃豆人   |                    | kapman      |         |
| 华容道   | *gnome-klotski*    |             |         |
| 宝石迷阵  | swell-foop         | kdiamond    | 消除类游戏   |
| 快艇骰子  | tali               | kiriki      |         |
| 四子棋   | four-in-a-row      | kfourinline |         |
| 炸弹人   |                    | granatier   |         |
| 珠玑妙算  | *gnome-mastermind* |             | 逻辑/益智游戏 |
|       |                    | klines      | 彩色线条游戏  |
| 纸牌接龙  | aisleriot          |             |         |
|       | atomix             | katomic     | 解谜游戏    |

更多逻辑/益智游戏请访问[网页谜题](https://cn.puzzle-sudoku.com/)，及[本地小游戏](https://gottcode.org/)。

### 经典开源游戏

## Wine / PlayOnBSD 游戏

## Renpy 游戏


`Renpy` 是一款视觉小说引擎，可以很方便地拿来制作互动视频游戏。由于游戏骨架是 `Python` 语言，因此可以很方便地移植到不同的系统平台上，如 Windows 及 Linux。

虽然 `Renpy` 暂时未对`FreeBSD`作系统适配，但是 `FreeBSD` 自己对其作了二次打包。如此一来，就可以在 FreeBSD 上畅玩互动游戏了么？显然不是！不过，我们可以作一番小小的尝试。


### 操作

1. 安装 renpy 

    `# pkg install renpy`
    
2. 下载游戏

    这里以[心跳文学社！](https://teamsalvato.itch.io/ddlc)为例，其它游戏也可同样操作。选择附有 Linux 版本的游戏解压。
    
3. 运行 renpy
    
    在引擎界面左侧`工程(Projects)`处可以看到列出来刷新的游戏`DDLC-1.1.1`，点击该游戏后，选择右下角的`启动工程(Launch Project)`即可加载游戏。

### 补充

- 游戏分发站： [itch](https://itch.io/)

- 尽量选择附有 Linux 版本的游戏

    如果游戏仅支持 Windows 系统，可通过 renpy 引擎打包 Linux 版本。
    
- rpa 文件解包：[unrpa](https://github.com/Lattyware/unrpa)

    `python3 unrpa -mp "解包目录" "XXX.rpa"`
    
- rpyc 文件解包：[unrpyc](https://github.com/CensoredUsername/unrpyc)

    `python3 unrpyc -c "XXX.rpyc"` 
    
    这一步非必要，仅为了方便翻译成其它语言。
    
## Godot 游戏

## 其它
