关于
====
这个项目用于存放kwplayer为各个发行版打好了的安装包, 推荐一般用户直接使用
这里的安装包, 因为这最简单, 也最不易出问题.


Debian系
=======
需要下载 python3-xlib_xx.deb, python3-keybinder_xx.deb, kwplayer_xx.deb 这
三个软件包. 直接双击就能安装deb包.

先安装python3-xlib, 之后是python3-keybinder, 最后是kwplayer.

当然, 也可以在终端里安装, 比如:

    # dpkg -i kwplayer_xx.deb
    # apt-get -f install


Fedora系
=======
Fedora 的打包工作是由 FZUG 负责. 目前支持 fc21, fc22. 添加 [FZUG源](https://github.com/FZUG/repo/wiki/FZUG) 后，使用以下命令安装。

```bash
dnf install http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
dnf install kwplayer
```


RHEL系
======
RHEL 的打包工作也由 mosquito 负责. 目前支持 el7.
更多其他开源软件欢迎访问 [myrepo](https://copr.fedoraproject.org/coprs/mosquito/myrepo/) 主页进行查询.

*安装步骤:*

	# yum install epel-release
	# yum-config-manager --add-repo=https://copr.fedoraproject.org/coprs/mosquito/myrepo/repo/epel-$(rpm -E %?rhel)/mosquito-myrepo-epel-$(rpm -E %?rhel).repo
	# yum localinstall http://li.nux.ro/download/nux/dextop/el$(rpm -E %rhel)/x86_64/nux-dextop-release-0-2.el$(rpm -E %rhel).nux.noarch.rpm
	# yum install kwplayer


Arch Linux
==========
Arch Linux用户, 可以直接使用build_arch/PKGBUILD脚本来安装kwplayer, 它是由
MJsaka <qiuxuenan@gmail.com> 维护的. 使用时有什么问题, 可以直接联系他.
非常感谢他做的工作.

*关于桌面歌词无法固定的解决方法(#66)*

因为Extra源中python-cairo的代码来自于[cairo官方](http://www.cairographics.org/pycairo)，不知是太新了还是怎么的，无法和python-gobject的Region补丁兼容。在AUR中有个python-cairo-git，这个包源码来自于[freedesktop](http://cgit.freedesktop.org/pycairo/)，没有问题。先安装python-cairo-git，因为python-gobject依赖python-cairo-git:

	1. 首先安装AUR中的python-cairo-git
		$ yaourt python-cairo-git	   
	2. 然后安装build_arch中打好补丁的pygobject-3.14.0-1.src.tar.gz(因为上面的原因，所以官方Extra源中的python-gobject包应该不会包含这个补丁，可以根据自己的需要安装)，首先解压然后在目录中执行：
		$ makepkg -s PKGBUILD
		# pacman -U *.pkg.tar.xz

Gentoo
======
添加gentoo-zh的overlay，直接安装即可：

layman -a gentoo-zh;emerge kwplayer

ebuild有问题，反馈至：http://github.com/microcai/gentoo-zh


打包时要包含的依赖包
===================
在制作一个发行版里的安装包时, 要包含以下依赖包. 不同发行版里的包名可能不尽相同:

* gnome-icon-theme-symbolic
* gstreamer1.0-libav 音频/视频的解码器
* gstreamer1.0-plugins-base
* gstreamer1.0-plugins-good
* gstreamer1.0-plugins-ugly
* gstreamer1.0-pulseaudio
* gstreamer1.0-x
* gir1.2-gstreamer-1.0,
* gir1.2-gst-plugins-base-1.0
* gir1.2-notify-0.7 - notify 的Gtk绑定.
* python3 
* python3-cairo
* python3-dbus
* python3-gi  -  gkt3的python3绑定
* python3-gi-cairo
* python3-ply - Lex, Yacc的python3实现, kwplayer用它来解析歌词

可选安装包, 安装它们后, kwplayer的功能更完善:

* mutagen - https://github.com/LordSputnik/mutagen, kwplayer用它来转化mp3标签
编码
* python3-xlib - https://github.com/LiuLang/python3-xlib, X的底层接口, 这个是从python-xlib迁移过来的, python3-keybinder需要这个包
* python3-keybinder https://github.com/LiuLang/python3-keybinder, 用于绑定
全局快捷键
* leveldb - 强大的NoSQL数据库(用于缓存数据), kwplayer用它来缓存列表
* python3-leveldb  -  leveldb的python3绑定
* gstreamer1.0-alsa - 如果你的系统里的声音系统是ALSA, 需要安装这个包. 参考[#issue63](https://github.com/LiuLang/kwplayer-packages/issues/63)
