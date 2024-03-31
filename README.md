# OpenWrt firmware build
Simple compilation without external packages, similar to the official build please find by link below:<br>
https://drive.google.com/drive/folders/1lsYUxoyvi-zqXln8qlYRa4Y5rIMDfy-P<br>

# How to build the firmware yourself
1. Download OpenWrt source code to the local disk:<br>
> wget -t5 --timeout=20 --no-check-certificate -O openwrt-23.05.2.zip https://github.com/openwrt/openwrt/archive/refs/tags/v23.05.2.zip<br>
> unzip -q openwrt-23.05.2.zip<br>
> rm -f openwrt-23.05.2.zip
2. Navigate to the downloaded source directory:<br>
> cd openwrt-23.05.2
3. Get patch from git:<br>
> git clone https://github.com/Ser9ei/xiaomi_ax3000t-openwrt23_patch
4. Execute patch:<br>
> patch -p1 -N < xiaomi_ax3000t-openwrt23_patch/xiaomi_ax3000t-dts.patch
5. Check erros
6. Copy config file:<br>
> cp xiaomi_ax3000t-openwrt23_patch/openwrt.config .config
7. Build firmware from the patched sources<br>
see more details by the link: https://openwrt.org/docs/guide-developer/toolchain/use-buildsystem<br>
- Update the feed:<br>
> ./scripts/feeds update -a<br>
> ./scripts/feeds install -a<br>
- Configure the firmware image:<br>
> make menuconfig<br>
- Build the firmware image:<br>
> make -j$(($(nproc)+1)) V=-1<br>
