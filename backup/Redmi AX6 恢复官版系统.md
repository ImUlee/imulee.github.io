1. 通过网线电脑与路由器连接，使用 MobaXterm 来连接，将解压后的两个 ubi 格式文件（mibib.bin、appsbl.bin）上传至 /tmp 目录下
2. SSH 输入以下命令查看分区确认 `mtd1` 和 `mtd7` 的分区是否存在

    `cat /proc/mtd`

    会出现以下详细列表：
    ````
    root@lede:~# cat /proc/mtd
    dev: size erasesize name
    mtd0: 00100000 00020000 “0:sbl1”
    mtd1: 00100000 00020000 “0:mibib”
    mtd2: 00300000 00020000 “0:qsee”
    mtd3: 00080000 00020000 “0:devcfg”
    mtd4: 00080000 00020000 “0:rpm”
    mtd5: 00080000 00020000 “0:cdt”
    mtd6: 00080000 00020000 “0:appsblenv”
    mtd7: 00100000 00020000 “0:appsbl”
    mtd8: 00080000 00020000 “0:art”
    mtd9: 00080000 00020000 “bdata”
    mtd10: 00080000 00020000 “crash”
    mtd11: 00080000 00020000 “crash_syslog”
    mtd12: 023c0000 00020000 “rootfs”
    mtd13: 023c0000 00020000 “rootfs_1”
    mtd14: 01ec0000 00020000 “overlay”
    mtd15: 00080000 00020000 “rsvd0”
    ````
3. 确认 `mtd1` 和 `mtd7` 存在无误后开始刷写，SSH 连接路由器依次输入以下
    ```
    mtd erase /dev/mtd1
    mtd write /tmp/mibib.bin /dev/mtd1
    mtd erase /dev/mtd7
    mtd write /tmp/appsbl.bin /dev/mtd7
    ```

4. 输入完命令一分钟后，路由器断电并设置电脑 iP 为 `192.168.31.100`，确保通过网线电脑与路由器连接
5. 电脑退出杀毒软件以及 Win10 的自带 Windows Defender 杀毒，修复工具才会传包给路由器修复
6. 打开小米路由修复工具，按住路由器 Reset 开机后修复工具选择 `192.168.31.100` 的网卡，修复进入救砖待机界面，再次断电，重新按住 Reset 键插电橙灯闪烁后松手。

最后，看到救砖软件里面开始上传固件后等待蓝灯闪烁等待1分钟断电、重新插电即可恢复到官方系统。


- [right - ax6 ax3600刷uboot后恢复官方系统方法](https://www.right.com.cn/forum/forum.php?mod=viewthread&tid=8236039&extra=&highlight=uboot&page=1)