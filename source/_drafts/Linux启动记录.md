---
title: Linux启动记录
date: 2019-10-17 15:40:49
tags:
  - Linux
---
从0x57到firefox
你一无所知
<!--more-->

作为程序员，刚接触Linux的时候，就老是想着看源码。毕竟Linus大佬也是这样说，

  Talk is cheap, show me the code.

所以，你现在正在使用的那个核心源码我们不说，我们都知道，你看的速度跟不上它更新的速度。
就说，unix v6/linux-1.1/minix 这些源码你这么莽撞地去看，能理清个线索就不错了。

总的来说，就是傻傻看代码其实是不行的。要想理清楚这整个流程，我们首先要从作为用户开始。大家都知道，计算机是分层的，每一层都有上一层为它服务。那我们日常的使用中，到底有哪些服务在默默地付出呢？

硬件就是个讲盒子，我讲不明白也不懂，就讲软件。从系统通电开始：

* BIOS自检，为我们占领内存，引导出bootloader和kernel
* bootloader现在用的是grub 2，曾经见过lilo/grub
* 加载kernel
* kernel调出shell（getty)
* getty 加载Xorg

写出来就发现其实还是不明白。今天就是大致了解了startx的工作流程。从命令行到桌面是一个飞跃啊，到底怎么来的，今天摸了一下。

具体的实验过程是这样的。

* 进入tty，之后先别startx。这会儿你在tty1下面

```
sudo X -retro
```

[注意]不加-retro也可以，但是现在的xorg不知道为什么，进入之后就是黑乎乎的一片，你可能觉得自己当机了。加上-retro会有一个十字架的鼠标，你发现自己进去了。

[注意] X就是Xorg的软链接

* 进入tty2或者tty3，登录，然后打开xterm或者urxvt，或者xclock之类的，方式如下

```
env DISPLAY=:0 urxvt
或
xterm -display :0
```

然后再转到tty1或者那个显示x的终端那边，就可以看到你的实验成果了。

这次实验让我彻底感受到了，X Window是怎么一回事，以前常说X的Server/Client是反的，这么体验一下，你就不会弄错了。

但这只是从用户角度，作为一名开发探险者，你应该稍稍浏览一下xlib的文档。GTK，Qt这些强大的图形库都是基于xlib以及后面的x window的理念的。

在稍稍理解了Linux核心是做什么的之后，也要了解一下我们日常使用最多的UI库到底源自何方。

PS：昨天炫耀了pstree有多么干净，今天把每个进程的作用记录一下吧。

```
[1msystemd,1[m
  |-systemd-journal,304             系统日志
  |-lvmetad,310 -f                  文件管理
  |-systemd-udevd,322               设备管理
  |-systemd-timesyn,388             时间同步
  |   `-{systemd-timesyn},406
  |-dbus-daemon,407 --system --address=systemd: --nofork --nopidfile -...         进程间通信
  |-[1mlogin,410[m                      
  |   `-[1mfish,435[m
  |       `-[1mstartx,8325[m /usr/bin/startx
  |           `-[1mxinit,8347[m /home/loki/.xinitrc -- /etc/X11/xinit/xserverrc :0 vt...
  |               |-Xorg,8348 -nolisten tcp :0 vt1 -keeptty -auth /tmp/serverauth.43g0hYyqM1
  |               |   |-{Xorg},8349             X window Server
  |               |   `-{Xorg},8350
  |               `-[1msh,8352[m /home/loki/.xinitrc
  |                   |-sh,8381 /home/loki/.xinitrc
  |                   `-[1mdwm,8383[m        dwm 窗口管理器as X Window Client
  |                       `-[1murxvt,10299[m
  |                           `-[1mfish,10300[m
  |                               |-[1mpstree,11167[m -apnh
  |                               `-xsel,11168 -b
  |-systemd-logind,413
  |-systemd,429 --user
  |   |-(sd-pam),430        权限管理（好像只有Arch有，有人提了bug)
  |   |-dbus-daemon,506 --session --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
  |   |-at-spi-bus-laun,524           gtk的依赖服务，但是是用来做Accessibilty的
  |   |   |-{at-spi-bus-laun},525     向我这种用法当然不需要，但是它却顽固地在这里
  |   |   |-{at-spi-bus-laun},526     可以杀死，有人报了bug。
  |   |   |-{at-spi-bus-laun},528     但是杀死随便开个gtk程序，它就又起来了。
  |   |   `-dbus-daemon,530 --config-file=/usr/share/defaults/at-spi2/accessibility.conf --nofork --print-address 3
  |   |-at-spi2-registr,539 --use-gnome-session
  |   |   |-{at-spi2-registr},540
  |   |   `-{at-spi2-registr},541
  |   |-ibus-portal,8371
  |   |   |-{ibus-portal},8372
  |   |   `-{ibus-portal},8376
  |   `-dconf-service,9561
  |       |-{dconf-service},9562
  |       `-{dconf-service},9563                                            无线网卡
  |-wpa_supplicant,764 -q -B -P /run/wpa_supplicant-wlp3s0.pid -i wlp3s0 -D nl80211,wext ...
  |-dhcpcd,1038 -4 -q -t 30 -L wlp3s0               ip分配
  |-watchman,1154 --no-pretty get-sockname       facebook的watchman，rn官方推荐，我也是懒得关
  |   |-{watchman},1155
  |   `-{watchman},1175
  |-ibus-daemon,8354 --xim -d                    输入法
  |-ibus-x11,8368 --kill-daemon
  |   |-{ibus-x11},8390
  |   |-{ibus-x11},8392
  |   `-{ibus-x11},8393
  `-bash,9475                                 markdown编辑器在用
      `-Typora,9483
         

```

嗯，就是这些了。玩累了，要做项目了今天晚上。



