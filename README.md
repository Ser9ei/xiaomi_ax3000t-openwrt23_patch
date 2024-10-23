# OpenWrt firmware build
Simple compilation without external packages, similar to the official build please find by link below:<br>
https://drive.google.com/drive/folders/1lsYUxoyvi-zqXln8qlYRa4Y5rIMDfy-P<br>

# What's New?
- W25N01KV spi-nand supported in the firmware.
https://github.com/openwrt/openwrt/pull/16669
- W25N01KV spi-nand supported in the OpenWrt U-Boot (ubootmod).
'ubootmod'firmware type can be installed to the router with Winbond spi-nand.
Patch has been merged from the SNAPSHOT.
https://forum.openwrt.org/t/openwrt-support-for-xiaomi-ax3000t/180490/1934
- Anti-Bootloop (nvram fix).
Fix work with u-boot variables for the stock u-boot.
The new version of the stock u-boot has an updated algorithm for multi-slot switching. In some cases, the router may enter a boot loop after installing OpenWrt.
https://forum.openwrt.org/t/openwrt-support-for-xiaomi-ax3000t/180490/1735
- "kernel: Fix section mismatch in ubi" patch has been merged from the SNAPSHOT.
https://github.com/openwrt/openwrt/commit/089c25f466dd496d165a02ab026fe55dbb802a8e
- Fix memory corruption during fq dma init. Patch has been merged from the SNAPSHOT.
https://github.com/openwrt/openwrt/blob/master/target/linux/generic/pending-6.6/735-net-ethernet-mtk_eth_soc-fix-memory-corruption-durin.patch
- Continue to support dts configuration for '112M NMBM' type firmware (as ImmortalWrt).
You can find MTK U-Boot for this firmware in the Google Drive link below.

# Warning
AN8855 support not included in current patch!

# How to build the firmware yourself
1. Download OpenWrt source code to the local disk:<br>
> wget -t5 --timeout=20 --no-check-certificate -O openwrt-23.05.5.zip https://github.com/openwrt/openwrt/archive/refs/tags/v23.05.5.zip<br>
> unzip -q openwrt-23.05.5.zip<br>
> rm -f openwrt-23.05.5.zip
2. Navigate to the downloaded source directory:<br>
> cd openwrt-23.05.5
3. Get patch from git:<br>
> git clone https://github.com/Ser9ei/xiaomi_ax3000t-openwrt23_patch
4. Execute patch:<br>
> patch -p1 -N < xiaomi_ax3000t-openwrt23_patch/xiaomi_ax3000t-dts.patch
5. fix permissions to the bootcount file (see issue from the SNAPSHOT https://github.com/openwrt/openwrt/commit/cb86e313d3ad6faf894b626bdd311fb106223ddf)
> chmod 755 target/linux/mediatek/filogic/base-files/etc/init.d/bootcount
6. Check erros
7. Copy config file:<br>
> cp xiaomi_ax3000t-openwrt23_patch/openwrt.config .config
8. Build firmware from the patched sources<br>
see more details by the link: https://openwrt.org/docs/guide-developer/toolchain/use-buildsystem<br>
- Update the feed:<br>
> ./scripts/feeds update -a<br>
> ./scripts/feeds install -a<br>
- Configure the firmware image:<br>
> make menuconfig<br>
- Build the firmware image:<br>
> make -j$(($(nproc)+1)) V=-1<br>
