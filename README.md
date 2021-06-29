欢迎来到Lean的Openwrt源码仓库！
=

[English](./README_EN.md)

如何编译自己需要的 OpenWrt 固件
-
注意：
-
1. **不**要用 **root** 用户进行编译！！！
2. 国内用户编译前最好准备好梯子
3. 默认登陆IP 192.168.1.1 密码 password


编译命令如下:
-
1. 首先装好 Ubuntu 64bit，推荐 Ubuntu 20.04 LTS x64

2. 命令行输入 `sudo apt-get update` ，然后输入
   `
   sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch python3 python2.7 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler g++-multilib antlr3 gperf wget curl swig rsync realpath
   `

3. 使用 `git clone https://github.com/coolsnowwolf/lede` 命令下载好源代码，然后 `cd lede` 进入目录

4. ```bash
   ./scripts/feeds update -a
   ./scripts/feeds install -a
   make menuconfig
   ```

5. `make -j8 download V=s` 下载dl库（国内请尽量全局科学上网）

6. 输入 `make -j12 V=s` （-j1 后面是线程数。第一次编译推荐用单线程）即可开始编译你要的固件了。

本套代码保证肯定可以编译成功。里面包括了 R21 所有源代码，包括 IPK 的。

你可以自由使用，但源码编译二次发布请注明我的 GitHub 仓库链接。谢谢合作！
=

二次编译：
```bash
cd lede
git pull
./scripts/feeds update -a && ./scripts/feeds install -a
make defconfig
make -j8 download
make -j12 V=s
```

如果需要重新配置：
```bash
rm -rf ./tmp && rm -rf .config
make menuconfig
make -j$(($(nproc) + 1)) V=s
```
文件清理
清除旧的编译产物（可选）


 `make clean`

在源码有大规模更新或者内核更新后执行，以保证编译质量。此操作会删除/bin和/build_dir目录中的文件。
清除旧的编译产物、交叉编译工具及工具链等目录（可选）


`make dirclean`

更换架构编译前必须执行。此操作会删除/bin和/build_dir目录的中的文件(make clean)以及/staging_dir、/toolchain、/tmp和/logs中的文件。
清除 Open­Wrt 源码以外的文件（可选）


`make distclean`

除非是做开发，并打算 push 到 GitHub 这样的远程仓库，否则几乎用不到。此操作相当于make dirclean外加删除/dl、/feeds目录和.config文件。
还原 Open­Wrt 源码到初始状态（可选）


`git clean -xdf`

如果把源码改坏了，或者长时间没有进行编译时使用。
清除临时文件


`rm -rf tmp`

删除执行make menuconfig后产生的一些临时文件，包括一些软件包的检索信息，删除后会重新加载package目录下的软件包。若不删除会导致一些新加入的软件包不显示。
删除编译配置文件


`rm -f .config`

在不删除的情况下如果取消选择某些组件它的依赖组件不会自动取消，所以对于需要调整组件的情况下建议删除。
编译完成后输出路径：bin/targets

特别提示：
------
1. 源代码中绝不含任何后门和可以监控或者劫持你的 HTTPS 的闭源软件， SSL 安全是互联网最后的壁垒。安全干净才是固件应该做到的；

2. 如有技术问题需要讨论，欢迎加入 QQ 讨论群： OP 共享技术交流群 ,号码 297253733 ，加群链接: 点击链接加入群聊【 OP 共享技术交流群】：[点击加入](https://jq.qq.com/?_wv=1027&k=5yCRuXL "OP共享技术交流群")

## 捐贈

如果你觉得此项目对你有帮助，可以捐助我们，以鼓励项目能持续发展，更加完善

### 支付宝

![alipay](doc/alipay_donate.jpg)

### 微信

![wechat](doc/wechat_donate.jpg)
