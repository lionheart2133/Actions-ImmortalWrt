# Github Actions ImmortalWrt WR30U
- fork自[这个项目]([https://github.com/padavanonly/immortalwrt-mt798x-24.10](https://github.com/Ljzkirito/Actions-ImmortalWrt)。搞不懂github的机制所以断了fork链以便自己随意修改。
- ImmortalWrt源码是[237大佬的24.10](https://github.com/padavanonly/immortalwrt-mt798x-24.10)。
- Github Actions来自于[P3TERX/Actions-OpenWrt](https://github.com/P3TERX/Actions-OpenWrt)，[中文教程](https://p3terx.com/archives/build-openwrt-with-github-actions.html)。
- 编译目标为WR30U
- 主要集成：homeproxy+uu加速器

恩山237大佬的wr30u固件就挺好用的了，唯一蛋疼的问题就是编译的时候少了uu加速器需要的那几个依赖，索性我才折腾出这个项目的。
目前我个人已稳定使用5个月，uu加速器在5月编译时是没有界面的(luci-app-uugamebooster)，在路由器后台根据[官方教程](https://router.uu.163.com/app/html/online/baike_share.html?baike_id=5f963c9304c215e129ca40e8)进行了重新安装，稀里糊涂就有了。
后面修改了config加上了luci-app-uugamebooster，但5月版本一直很稳定，没断流，千兆也一直能跑满，homeproxy也整挺好，就没换过固件。后面编译的版本都是同步上游的定时编译，本人纯小白，没有解决问题的能力，如有相关问题需自行解决。

## Config文件生成参考

- `make menuconfig` 可参考[OpenWrt MenuConfig设置和LuCI插件选项说明](https://mtom.ml/827.html)，一般先选`Target System`，`Subtarget`，`Target Profile`，再选`LUCI`插件。
- .config文件生成可借助WSL（Ubuntu-22.04）或虚拟机，执行以下命令
```
sudo sed -i 's#http://archive.ubuntu.com#https://mirrors.huaweicloud.com#' /etc/apt/sources.list
sudo sed -i 's#http://security.ubuntu.com#https://mirrors.huaweicloud.com#' /etc/apt/sources.list
sudo apt update
sudo apt upgrade -y
sudo apt-get -y install build-essential unzip libncurses-dev subversion
git clone --depth=1 https://github.com/hanwckf/immortalwrt-mt798x.git
cd immortalwrt-mt798x
./scripts/feeds update -a && ./scripts/feeds install -a
cp -f defconfig/mt7981-ax3000.config .config
make menuconfig
make defconfig
./scripts/diffconfig.sh > seed.config
```
进入目录`\\wsl$\Ubuntu*\home\*\immortalwrt-mt798x`复制一下这个`seed.config`的文本内容到项目根目录的`.config`文件中，方便查看修改。
- 差分文件seed.config[参考来源](https://github.com/coolsnowwolf/lede/issues/2288)


## 相关参考

- [超简单云编译](https://github.com/281677160/build-openwrt)
- [借助 GitHub Actions 的 OpenWrt 在线集成自动编译](https://github.com/KFERMercer/OpenWrt-CI)
- [qughij/openwrt-xiaoyu_xy-c5](https://github.com/qughij/openwrt-xiaoyu_xy-c5)
- [SuLingGG/OpenWrt-Rpi](https://github.com/SuLingGG/OpenWrt-Rpi)
- [IvanSolis1989/OpenWrt-DIY](https://github.com/IvanSolis1989/OpenWrt-DIY)
- [garypang13/OpenWrt](https://github.com/garypang13/OpenWrt)
- [zlxj2000/Openwrt-firmware](https://github.com/zlxj2000/Openwrt-firmware)
- [SuLingGG/Action-OpenWrt-Plus](https://github.com/SuLingGG/Action-OpenWrt-Plus)
- [Lancenas/Actions-Lean-OpenWrt](https://github.com/Lancenas/Actions-Lean-OpenWrt)
- [Lancenas/actions-openwrt-helloworld](https://github.com/Lancenas/actions-openwrt-helloworld)
- [xiaorouji/openwrt-passwall](https://github.com/xiaorouji/openwrt-passwall)
- [kenzok8/openwrt-packages](https://github.com/kenzok8/openwrt-packages)
- [kenzok8/small](https://github.com/kenzok8/small)
- [基本的Git技能](https://www.liaoxuefeng.com/wiki/896043488029600)
- [面向小白的Github_Action使用workflow自动编译lean_openwrt教程](https://zhuanlan.zhihu.com/p/94402324)
- [关于Github Action自动编译Lean_Openwrt的配置修改问题](https://zhuanlan.zhihu.com/p/94527343)
- [firker/diy-ziyong](https://github.com/firker/diy-ziyong)
- [xiaoqingfengATGH/feeds-xiaoqingfeng](https://github.com/xiaoqingfengATGH/feeds-xiaoqingfeng)

## Acknowledgments

- [Microsoft](https://www.microsoft.com)
- [Microsoft Azure](https://azure.microsoft.com)
- [GitHub](https://github.com)
- [GitHub Actions](https://github.com/features/actions)
- [tmate](https://github.com/tmate-io/tmate)
- [mxschmitt/action-tmate](https://github.com/mxschmitt/action-tmate)
- [csexton/debugger-action](https://github.com/csexton/debugger-action)
- [Cisco](https://www.cisco.com/)
- [OpenWrt](https://github.com/openwrt/openwrt)
- [Lean's OpenWrt](https://github.com/coolsnowwolf/lede)
- [Lienol's OpenWrt](https://github.com/Lienol/openwrt)
- [Cowtransfer](https://cowtransfer.com)
- [WeTransfer](https://wetransfer.com/)
- [Mikubill/transfer](https://github.com/Mikubill/transfer)

## License

[MIT](https://github.com/P3TERX/Actions-OpenWrt/blob/main/LICENSE) © P3TERX
