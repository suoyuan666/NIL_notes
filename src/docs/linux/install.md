# Linux 发行版安装指南

## 准备工作

### 获取系统安装镜像并验证

第一步就是获取系统安装镜像，这里没什么要说的，你想安装什么系统就去对应的网站下载系统安装镜像。

如果你没想好安装哪个发行版，可以参考[Linux 发行版介绍](../distro_intro)

值得一提的是 USTC 镜像源提供了部分 Linux 发行版的下载服务，可以访问 [USTC Open Source Software Mirror](https://mirrors.ustc.edu.cn/) 点击右侧的**获取安装镜像**即可使用 USTC 的镜像源下载。USTC 镜像源提供了 Debian、Kali、Ubuntu、Arch Linux、Fedora、OpenSUSE 等常见发行版的系统安装镜像下载服务。

在下载完成后可以去官网验证这个安装镜像是否正确，Linux 发行版的 wiki 或下载页面都会提供如何验证安装镜像的说明，比如：

- [Arch wiki](https://wiki.archlinux.org/title/Installation_guide#Verify_signature)
- [Verifying authenticity of Debian images](https://www.debian.org/CD/verify)
- [Gentoo Linux amd64 Handbook](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/Installation#Verifying_the_downloaded_files)

或者你选择不验证。

在获取到了系统安装镜像后，就要为发行版制作一个启动盘，这里推荐两个方案

- [pbatard/rufus](https://github.com/pbatard/rufus) 
    - rufus 用来将 U 盘做成系统启动盘，访问[官网](https://rufus.ie/)下载使用即可
- [ventoy/Ventoy](https://github.com/ventoy/Ventoy)
    - ventoy 与 rufus 不同的是， ventoy 本身就是一个可以引导的系统，它用来将 U 盘做成多系统的启动盘，并且很好的保留了 U 盘的存储功能，用户依旧可以用来存放文件。
    - 访问[官网](https://www.ventoy.net/cn/index.html)下载即可
    - ventoy 默认启用了安全启动的支持，用户可以查看[官网上的 wiki](https://www.ventoy.net/cn/doc_secure.html) 操作。

U 盘大小推荐不小于 16 GB

### 设置 BIOS

需要在 BIOS 中关闭安全启动和快速启动，并开启从 USB 中启动，但大多数时候可以不关闭安全启动，但快速启动需要关闭。

如何进入 BIOS，不同厂商有不同的方式，可以对应区搜索。

> 安全启动是 UEFI(Unified Extensible Firmware Interface) 标准中的一个安全手段，用来防止未经系统中信任的密钥签名的系统被启动。基本上 x86 的硬件都被写上了 Microsoft 的 key。
>
> Debian、Fedora、Deepin 等发行版的系统也使用了 Microsoft 的密钥签名，所以如果要安装这些发行版，不关闭安全启动也可以。
>
> 各家发行版的 wiki 中的 secure boot 界面介绍了它们对安全启动的支持，比如 [Fedora 上的](https://fedoraproject.org/wiki/Secureboot)和 [Debian 上的](https://wiki.debian.org/SecureBoot)

## 开始安装

开始安装，需要在启动时通过按键进入系统启动项选择界面，这个按键也是因厂商而异。

选择了从 U 盘启动后，如果是 rufus 做的启动盘就已经启动了系统安装镜像了，如果使用的是 ventoy，那么启动后通过方向键选择要启动的系统安装镜像即可。

接下来假设是图形化安装系统的方式，而非传统 Arch Linux、Gentoo Linux 等需要手敲指令安装系统的方式。

首先是语言选择界面，这里推荐选择英文，之后启动后在系统中切换成中文，当然也可以直接选中文。

> 选中文有一个坏处，安装后你用户下的下载、图片等文件夹都是中文命名，这会导致你在终端模拟器中操作目录的时候还需要切换输入法，略显麻烦
>
> 但如果安装时选择英文，之后再切换成中文，这时候的换名就是一个可选的选择，系统会提示你时候要更改名称，你可以选择不改
>
> 如果安装时选英文，也可以在安装后改成英文，只需要在终端模拟器中执行 `LC_ALL=en_US.UTF-8 xdg-user-dirs-update --force` 即可
>
> 这个文件夹名称是标准的 xdg-user-dir，应用在使用下载这个文件夹时会读取用户配置，然后读取用户配置中下载对应的文件夹（如果这个应用也实现的标准的话）

选择完语言后，可能涉及到网络设置，正常联网即可

说一下硬盘设置和桌面环境选择

**硬盘设置**

这里值得一提的是 Windows 双系统的问题，不过问题不大

部分发行版提供了默认的方案，可以直接和 windows 双系统启动，比如 Ubuntu。

如果你想自己设置的话，你至少需要两个分区

- /boot 是引导分区，文件系统应该是 FAT32，也就是说你应该有一个 512 MB 或者多少大小（无需太大）的空间，挂载点是 /boot，或者 /efi，或者是 /boot/efi，文件系统选择 FAT32。
- / 是根目录分区，也就是真正我们感知到的文件系统。
    - 这里挂载点就是 `/`

除了这两个之外，还可以设置交换分区，交换分区可以让内存中不常用的数据存在硬盘中，增加效率，一般认为内存 16 GB 以下可以设置交换分区，一般认为：

```
内存 <= 4g：Swap 至少 4G
内存 4~16G：Swap 至少 8G
内存 16G~64G：Swap 至少 16G
内存 64G~256G：Swap 至少 32G
```

当然也可以不设置交换分区，Fedora 默认就不设置交换分区，而是设置一个 **RAM/2** 大小的 zram

分区可以分的更加细致，如果你对根目录都有什么不清楚的话，可以参考 Linux 基金会维护的 [Filesystem Hierarchy Standard](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html)

这个标准适用于一般情况，对于现代的 Linux 发行版来说，/bin 只是 /usr/bin 的链接，/sbin、/lib 等同理，合并这些目录对用户和开发者更加友好，也是现在 [systemd 的要求](https://lists.freedesktop.org/archives/systemd-devel/2022-September/048352.html)

> systemd 是现代化的 init 系统，虽然有批评认为 systemd 有很多 init 不需要有的东西（比如后文提到的 systemd-boot），但不得不说 systemd 还很不错，绝大多数发行版都选择了 systemd 作为 init 系统。
>
> zram 用于压缩内存，可以用来当 SWAP，比正常未加密的 SWAP 可能带来的隐私泄漏来说，zram 会更好

推荐选择硬盘加密，一般 Linux 下使用的是 [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt)，ext4 文件系统也支持加密，但文件系统的加密是对某些目录的加密，而 dm-crypt 这是整个硬盘分区的加密

由于 GRUB 对 LUKS2 的加密算法支持仍不完全，所以如果为了更好的安全性选择了 LUKS2 的 [argon2id](https://en.wikipedia.org/wiki/Argon2) 算法的话，可以选择 systemd-boot 作为 bootloader

当然，如果是图形化安装界面的话也无法选择具体的算法，并且一般都为 GRUB 作为 bootloader

**文件系统选择**

根目录的文件系统推荐三个 ext4，btrfs，xfs。

三个文件系统中，ext4 和 xfs 相对于 btrfs 有更久的历史，稳定性也经过了时间的验证。

btrfs 是一个有很多特性的文件系统（虽然被一些 BSD 爱好者评价为 ZFS 的拙劣模仿品）。透明压缩、快照、子卷、RAID，这些都是 btrfs 的特性。透明压缩可以让 btrfs 用更小的空间去存储，快照让系统更加的稳定。

以上对 btrfs 的优点评价均为理想情况，部分用户认为 btrfs 还是个实验性的文件系统，还不可以在生产环境下使用。大多数日常使用 Linux 的用户对该文件系统还是表示欢迎。Fedora 和 OpenSUSE 默认的根目录文件系统就是 btrfs。

**桌面环境选择**

部分发行版安装时不能选择桌面环境，比如 Ubuntu 安装时就是 GNOME，Fedora 也一样，需要安装其他桌面环境的安装镜像才能安装对应的桌面环境。

目前只有两个桌面环境可供选择：[KDE Plasma](https://kde.org/plasma-desktop/) 和 [GNOME](https://www.gnome.org/)

发行版可能还提供 [Xfce](https://xfce.org/) 桌面环境的选项，但这里并不推荐该桌面环境，开发进度仍没有跟上其他桌面环境的开发进度，甚至现在还不支持 Wayland。

目前我们推荐使用 Wayland 协议的桌面环境，也就是 KDE Plasma 和 GNOME。

system76 正在开发 [cosmic](https://system76.com/cosmic/) 桌面环境，这是一个用 Rust 编写的桌面环境，可以期待一下该项目正式发布

从 KDE Plasma 的官网中可以看出，KDE Plasma 的美术风格不如 GNOME，不过 KDE Plasma 对于中文用户来说，有一个好处，那就是对 Wayland 输入法协议的完整支持。

GNOME 并没有对所有 Wayland 输入法协议的完整支持，它只支持 text-input-v3，但很长一段时间，Chromium 浏览器内核都只支持 text-input-v1，导致必须附加 `--gtk-version=4` 参数启动 Chromium 开启了 GTK4 的支持才能正常使用输入法，但是 Electron 至今没有实现 GTK4。但是现在 Chromium 已经可以通过 `--wayland-text-input-version=3` 参数开启对 text-input-v3 的支持，并且新版的 Electron 的也对应支持该参数。所以问题在于使用旧版 Electron 的应用，可能还无法正常的在 GNOME 下使用 Wayland 的时候正常的使用中文输入法

但 KDE Plasma 实现了对所有 Wayland 输入法协议的支持，所以不存在问题

但不得不说，上述说明的问题只是 [CJK](https://en.wikipedia.org/wiki/CJK_characters) 问题，也可以说是我们在输入中文时的问题，正常英文该怎么用还怎么用

## 安装完成
