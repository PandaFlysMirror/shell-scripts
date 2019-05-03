# Linux Shell Scripts
wget --no-check-certificate https://raw.githubusercontent.com/kuoruan/shell-scripts/master/ovz-bbr/ovz-bbr-installer.sh
chmod +x ovz-bbr-installer.sh
./ovz-bbr-installer.sh
另外，有些人的vps是用来做网站或者云盘的，这个时候需要添加BBR加速端口。

安装的时候只配置了一个加速端口，但是你可以配置多端口加速，配置方法非常简单。 修改文件

1
# vi /usr/local/haproxy-lkl/etc/port-rules
进入后按“i”

在文件里添加需要加速的端口，每行一条，可以配置单个端口或者端口范围，以 # 开头的行将被忽略。

例如：8800 或者 8800-8810 配置完成之后，按“esc”键退出，然后输入“：wq”保存退出。

再重启 haproxy-lkl 即可。

使用 systemctl 或者 service 命令来启动、停止和重启 HAporxy-lkl：

1
systemctl {start|stop|restart} haproxy–lkl
1
service haproxy–lkl {start|stop|restart}
/usr/local/haproxy–lkl/etc/haproxy.cfg 这个文件是通过 port-rules 自动生成的，每次启动都会重新生成，所以直接修改它的配置没用。 如果想要自定义配置，请修改启动文件：

1
/usr/local/haproxy–lkl/sbin/haproxy–lkl
注意，在实际的安装中发现，部分VPS安装后无法上网，这里可以用下面的卸载命令：

./ovz-bbr-installer.sh uninstall

一些 Linux 脚本

```sh
$ tree
├── kcptun
│   └── kcptun.sh # kcptun 一键安装脚本
└── ovz-bbr
    └── ovz-bbr-installer.sh # OpenVZ BBR 一键安装脚本
```

## Kcptun 一键安装脚本

* 安装命令：

```sh
wget --no-check-certificate https://github.com/kuoruan/shell-scripts/raw/master/kcptun/kcptun.sh
sh kcptun.sh
```

* 帮助信息

```sh
# sh kcptun.sh help
请使用: kcptun.sh <option>

可使用的参数 <option> 包括:

    install          安装
    uninstall        卸载
    update           检查更新
    manual           自定义 Kcptun 版本安装
    help             查看脚本使用说明
    add              添加一个实例, 多端口加速
    reconfig <id>    重新配置实例
    show <id>        显示实例详细配置
    log <id>         显示实例日志
    del <id>         删除一个实例

注: 上述参数中的 <id> 可选, 代表的是实例的ID
    可使用 1, 2, 3 ... 分别对应实例 kcptun, kcptun2, kcptun3 ...
    若不指定 <id>, 则默认为 1

Supervisor 命令:
    service supervisord {start|stop|restart|status}
                        {启动|关闭|重启|查看状态}
Kcptun 相关命令:
    supervisorctl {start|stop|restart|status} kcptun<id>
                  {启动|关闭|重启|查看状态}
```

## OpenVZ BBR 一键安装脚本

* 安装命令：

```sh
wget --no-check-certificate https://github.com/kuoruan/shell-scripts/raw/master/ovz-bbr/ovz-bbr-installer.sh
sh ovz-bbr-installer.sh
```

* 卸载命令

```sh
sh ovz-bbr-installer.sh uninstall
```
