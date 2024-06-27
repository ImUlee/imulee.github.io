## 挂载 overlay

1. 创建文件 /etc/init.d/miwifi_overlay , (可vi /etc/init.d/miwifi_overlay, i, 粘贴, :wq)

    ````
    #!/bin/sh /etc/rc.common

    START=00

    . /lib/functions/preinit.sh

    start() {
            [ -e /data/overlay ] || mkdir /data/overlay
            [ -e /data/overlay/upper ] || mkdir /data/overlay/upper
            [ -e /data/overlay/work ] || mkdir /data/overlay/work

            mount --bind /data/overlay /overlay
            fopivot /overlay/upper /overlay/work /rom 1

            #Fixup miwifi misc, and DO NOT use /overlay/upper/etc instead, /etc/uci-defaults/* may be already removed
            /bin/mount -o noatime,move /rom/data /data 2>&-
            /bin/mount -o noatime,move /rom/etc /etc 2>&-
            /bin/mount -o noatime,move /rom/ini /ini 2>&-
            /bin/mount -o noatime,move /rom/userdisk /userdisk 2>&-

            return 0
    }

    ````

2. 依次执行 每段一次：

    ````
    chmod 755 /etc/init.d/miwifi_overlay

    /etc/init.d/miwifi_overlay enable

    sync

    reboot

    ````
重启完之后分区就可读写了, 更新固件后请1~5再来一次





## 安装 Zerotier

1. 将 Zerotier 文件夹上传到 `/data` 目录下

2. ssh 执行 `chmod +x /data/Zerotier/zero && /data/Zerotier/zero`



- 修改配置文件 `vi /etc/config/zerotier` 修改 `list join 'a84ac5c10a5d04b3'`  a84ac5c10a5d04b3 为网络ID
> [!TIP]
> 启动命令：/etc/init.d/zerotier start
> 停止命令：/etc/init.d/zerotier stop
> 开机自启：/etc/init.d/zerotier enable
> 启动状态：/etc/init.d/zerotier status

----
下载地址：https://github.com/ImUlee/imulee.github.io/releases/tag/RedmiAX6