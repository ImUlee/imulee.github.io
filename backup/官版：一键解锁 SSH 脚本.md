目测本论坛最强小米/红米路由器一键ssh工具, 刷机告别ttl, 也不需要另外一个路由器了(比如ax6). 已经测试过CR880X, AX6, AX6S, AX5JDC, AX3000.

### 使用方法:
Win 和 Linux 可以运行
1. 运行 run.bat (linux跑run.sh)
2. 主菜单选1输入目标路由器ip地址
3. 主菜单选2开启ssh (注意此时ssh并没固化,重启会失效,要固化做第四步,也可以直接开始刷分区和uboot)
4. (可选)主菜单选8再选7固化ssh.

默认账号&密码：`root/root`
修改root密码：`passwd`

### 补充：

ssh默认的密码会改成root. ssh即使固化之后,重启之后密码可能会被恢复成sn算出来的那个, 原因不明, 可能小米有保护机制.
想要永久固化的话, 在/etc/rc.local最后一行上面加一行‘替换root为新密码’
````
vi /etc/rc.local
echo -e 'root\nroot' | passwd root
````

下载地址：https://github.com/ImUlee/imulee.github.io/releases/tag/RedmiAX6