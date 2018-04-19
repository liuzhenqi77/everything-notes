# Shadowsocks 配置

## 环境

* Ubuntu 16.04+
* KVM 虚拟环境

## 配置 SSR 服务器端

在 cmd 中用 ssh 连接至服务器并按照提示输入密码
```bash
ssh root@服务器地址
```

更新软件包列表，安装必要软件
```bash
apt update
apt install git
```

下载 ssr 文件
```bash
git clone https://github.com/ssrbackup/shadowsocksr.git
```

使用`ls -alh`查看当前目录下文件（确认包含下载的ss），运行脚本在`shadowsocksr/shadowsocks/`下

复制默认配置文件
```bash
cd shadowsocksr/
cp config.json shadowsocks/config.json
cd shadowsocks/
```

修改配置文件
```bash
nano config.json
```

修改为如下内容，替换服务器地址，设定密码

```json
{
    "server": "服务器地址",
    "server_ipv6": "::",
    "server_port": 443,
    "local_address": "127.0.0.1",
    "local_port": 1080,

    "password": "密码",
    "method": "none",
    "protocol": "auth_chain_a",
    "protocol_param": "",
    "obfs": "tls1.2_ticket_auth",
    "obfs_param": "cloudflare.com, cloudfront.net",
    "speed_limit_per_con": 0,
    "speed_limit_per_user": 0,

    "additional_ports" : {}, // only works under multi-user mode
    "additional_ports_only" : false, // only works under multi-user mode
    "timeout": 120,
    "udp_timeout": 60,
    "dns_ipv6": false,
    "connect_verbose_info": 0,
    "redirect": "",
    "fast_open": true
}
```

## 配置 SSR 客户端

Windows 客户端 [下载地址](https://github.com/ssrbackup/shadowsocksr-csharp/releases)

Android 客户端 [下载地址](https://github.com/ssrbackup/shadowsocksr-android/releases)

下载后按照前面配置文件填好设置即可

## 开启 TCP BBR 拥塞控制算法（可选）

通过尽量使用带宽的方法减少延迟，适合视频、游戏等需要低延迟场合。

使用`uname -r`查看内核版本，如果在4.9及以前，需要先更新内核

更新内核（使用 Hardware Enablement Stack (HWE)，自动更新内核。未验证，如失败可采用之后的方法）
```bash
apt install --install-recommends linux-generic-hwe-16.04
apt autoremove
```

对14.04及以前的系统，也可使用以下步骤
> 安装 4.14 内核（4.10+ 均可）
> ```bash
> wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.14.12/linux-image-4.14.12-041412-generic_4.14.12-041412.201801051649_amd64.deb
> ```
> 移除旧内核
> ```bash
> dpkg -l | grep linux-image 
> apt-get purge 旧内核
> ```
> 更新引导，重启
> ```bash
> update-grub
> reboot
> ```

使用`uname -r`验证内核版本为4.9+

执行`lsmod | grep bbr`如果结果中没有`tcp_bbr`的话就先执行

```bash
modprobe tcp_bbr
echo "tcp_bbr" >> /etc/modules-load.d/modules.conf
```
执行

```bash
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
```

使用`sysctl -p`保存生效

执行

```bash
sysctl net.ipv4.tcp_available_congestion_control
sysctl net.ipv4.tcp_congestion_control
```

如果结果里有`bbr`，则开启成功。
执行`lsmod | grep bbr`, 看到有`tcp_bbr`模块即说明 bbr 已启动
