## 功能与特性

### 重要事项
* 添加 `shadow-utils` 组件（用于方便新建用户），导致管理页面上的 `更改密码` 功能失效。 
请使用 SSH 工具，使用空密码登陆后，执行 `passwd` 命令并根据提示设置密码。
* 采用 FriendlyWrt 的默认的 WAN/LAN 口绑定。现在 WAN 口绑定在远离电源接口的那一个 RJ45 上。

### 安全性
* 防火墙设置为默认拒绝来自 WAN 口入站数据和转发。
* 未安装 ttyd 组件（网页终端）。因为该组件默认开放端口，且不使用 HTTPS ；同时该组件默认免密码 root 身份登录到 shell ，此为安全隐患。  
* 固件默认密码为空，建议刷机后尽快更改密码。
* Dropbear 默认监听了所有接口，建议刷机后尽快更改为只监听 LAN 口。

### 常用功能
|  |  |  |  |  |  |
| :---: | :---: | :---: | :---: | :---: | :---: |
| NetData监控 | WireGuard | 释放内存 | 定时重启 | ZeroTier | AdGuard Home |
| SSRP | OpenClash | PASSWALL | 动态DNS | 硬盘休眠 | WOL网络唤醒 |
| uHTTPd配置 | Samba4 | Aria2 | UPnP配置 | IP/MAC绑定 | SQM |
| 流量监控 | BBR (1) | FullCone NAT (2) | Offloading (2) | ChinaDNS-NG | SmartDNS |

1. BBR 已默认启用。  
2. SFE Offloading 和 FullCone NAT 已默认启用（其选项在防火墙设置页面中）；软件 Offloading 需要在防火墙设置页面中，默认没有启用。注意：SFE Offloading 和软件 Offloading 只能**二选一**，**不能同时开启**。  
3. FTP 支持由 vsftpd-tls 提供。没用图形界面，须使用命令行手工配置。建议开启TLS以提高安全性。  
4. 以下组件在本固件中不包含：  
ttyd（网页终端）、Docker、单线/多线多拨、KMS 服务器、访问时间控制、WiFi 排程、beardropper（SSH 公网访问限制）、应用过滤、三代壳 OLED 程序、Server 酱、网易云音乐解锁、USB 打印机、迅雷快鸟、pandownload-fake-server、frpc/frps 内网穿透、OpenVPN、京东自动签到、Transmission、qBittorrent。

### 命令行特性
* 添加 `shadow-utils` 组件，便于配置文件共享时新建用户。
* `cmp`、`find`、`grep`、`gzip`、`gunzip`、`ip`、`login`、`md5sum`、`mount`、`passwd`、`sha256sum`、`tar`、`umount`、`xargs`、`zcat` 等命令替换为 GNU 实现或其他更标准的实现。
* SSH 客户端由 OpenSSH 提供（而不是 Dropbear），提供更标准的 SSH 连接体验。（服务端仍然是 Dropbear）
* F2FS、EXT4、FAT32、BTRFS 文件系统支持。EXT4 支持 acl 和 attr 。
* Python3、Perl、Node.js 解释型语言支持。C 语言支持由 GCC 和 make 提供。
* Git 版本控制工具。
* `curl` 和 `wget` 两大常用工具。
* 由 openssh-sftp-server 提供 SFTP 协议文件传输功能。由 lrzsz 提供终端内小文件传输功能。由 openssh-keygen 提供 SSH 密钥对生成。
* 常用命令行工具：bc、file、htop、lsof、nohup、pv、timeout、tree、xxd、split。
* 文本编辑器：nano、vim。其中 vim 已添加一个[简单的配置文件](./PRECONFS/vimrc)。
* 终端复用工具：screen、tmux。其中 screen 已添加一个[简单的配置文件](./PRECONFS/screenrc)。
* 网络相关工具：dig、ethtool、host、ifstat、iftop、iperf3、ncat、nmap、nping、ss。
* 压缩工具：zstd、unzip、bzip2、xz。
* 文件同步工具：rsync。
* 密码学工具：GnuPG。
* 压力测试工具：stress。
* 硬盘自检工具：smartmontools。
* 磁盘分区工具：fdisk、cfdisk（MBR/GPT 分区表均支持）。
* 其他工具：oath-toolkit、qrencode、sqlite3-cli。

### OpneSSL
* 支持签发自签名证书。

### 无线网卡
* 理论上支持部分 USB 无线网卡，未测试。

### 三代壳OLED相关
* 未安装 OLED 的 luci-app 和对应的程序。  
需要 OLED 功能的用户，自行寻找/选择适合的软件包安装即可。也可从源代码，利用本固件自带的 GCC 编译。同时不要忘记安装依赖包 i2c-tools。
