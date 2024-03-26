### TODO: 
1) Download OpenWrt source code to the local disk:<br>
> wget -t5 --timeout=20 --no-check-certificate -O openwrt-23.05.2.zip https://github.com/openwrt/openwrt/archive/refs/tags/v23.05.2.zip
unzip -q openwrt-23.05.2.zip
> rm -f openwrt-23.05.2.zip
3) Navigate to the downloaded source directory:<br>
> cd openwrt-23.05.2
5) Get patch from git:<br>
> git clone https://github.com/Ser9ei/xiaomi_ax3000t-openwrt23_patch
4) Execute patch:<br>
> patch -p1 -N < xiaomi_ax3000t-openwrt23_patch/xiaomi_ax3000t-dts.patch
5) Check erros
6) Copy config file:<br>
> cp xiaomi_ax3000t-openwrt23_patch/openwrt.config .config
7) Build firmware from the patched sources<br>
see, how to: https://openwrt.org/docs/guide-developer/toolchain/use-buildsystem)
> make menuconfig
> make -j $(($(nproc)+1)) V=-1
