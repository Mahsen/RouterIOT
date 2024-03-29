# RouterIOT
This project useing openWRT and link lichee

This is the buildsystem for the OpenWrt Linux distribution.

Please use "make menuconfig" to configure your appreciated
configuration for the toolchain and firmware.

You need to have installed gcc, binutils, bzip2, flex, python, perl, make,
find, grep, diff, unzip, gawk, getopt, subversion, libz-dev and libc headers.

Run "./scripts/feeds update -a" to get all the latest package definitions
defined in feeds.conf / feeds.conf.default respectively
and "./scripts/feeds install -a" to install symlinks of all of them into
package/feeds/.

Use "make menuconfig" to configure your image.

Simply running "make" will build your firmware.
It will download all sources, build the cross-compile toolchain, 
the kernel and all choosen applications.

You can use "scripts/flashing/flash.sh" for remotely updating your embedded
system via tftp.

The OpenWrt system is documented in docs/. You will need a LaTeX distribution
and the tex4ht package to build the documentation. Type "make -C docs/" to build it.

To build your own firmware you need to have access to a Linux, BSD or MacOSX system
(case-sensitive filesystem required). Cygwin will not be supported because of
the lack of case sensitiveness in the file system.
-----------------------------------------------------
Build OpenWrt Image for Lichee Pi Nano

Update the configuration for Lichee Pi Nano
cd ~/openwrt
cat > .config << EOL
CONFIG_TARGET_sunxi=y
CONFIG_TARGET_sunxi_arm9=y
CONFIG_TARGET_sunxi_arm9_DEVICE_suniv-f1c100s-licheepi-nano=y
CONFIG_DEVEL=y
CONFIG_BRCMFMAC_SDIO=y
CONFIG_BRCMFMAC_USB=y
CONFIG_DRIVER_11AC_SUPPORT=y
CONFIG_DRIVER_11N_SUPPORT=y
CONFIG_PACKAGE_MAC80211_DEBUGFS=y
CONFIG_PACKAGE_MAC80211_MESH=y
CONFIG_PACKAGE_brcmfmac-firmware-usb=y
CONFIG_PACKAGE_hostapd-common=y
CONFIG_PACKAGE_iw=y
CONFIG_PACKAGE_iwinfo=y
CONFIG_PACKAGE_kmod-ata-ahci-platform=y
CONFIG_PACKAGE_kmod-ata-core=y
CONFIG_PACKAGE_kmod-ata-sunxi=y
CONFIG_PACKAGE_kmod-brcmfmac=y
CONFIG_PACKAGE_kmod-brcmutil=y
CONFIG_PACKAGE_kmod-cfg80211=y
CONFIG_PACKAGE_kmod-libphy=y
CONFIG_PACKAGE_kmod-mac80211=y
CONFIG_PACKAGE_kmod-mmc=y
CONFIG_PACKAGE_kmod-nls-base=y
CONFIG_PACKAGE_kmod-of-mdio=y
CONFIG_PACKAGE_kmod-rtc-sunxi=y
CONFIG_PACKAGE_kmod-rtl8192c-common=y
CONFIG_PACKAGE_kmod-rtl8192cu=y
CONFIG_PACKAGE_kmod-rtl8xxxu=y
CONFIG_PACKAGE_kmod-rtlwifi=y
CONFIG_PACKAGE_kmod-rtlwifi-usb=y
CONFIG_PACKAGE_kmod-scsi-core=y
CONFIG_PACKAGE_kmod-sun4i-emac=y
CONFIG_PACKAGE_kmod-usb-core=y
CONFIG_PACKAGE_libiwinfo=y
CONFIG_PACKAGE_rtl8188eu-firmware=y
CONFIG_PACKAGE_rtl8192cu-firmware=y
CONFIG_PACKAGE_swconfig=y
CONFIG_PACKAGE_wireless-regdb=y
CONFIG_PACKAGE_wpad-mini=y
CONFIG_SOFT_FLOAT=y
CONFIG_TARGET_OPTIONS=y
EOL

Generate the image
./scripts/feeds update -a && ./scripts/feeds install -a
make defconfig
make world

When you finish the compile without any failure, you can find the image (openwrt-sunxi-arm9-suniv-f1c100s-licheepi-nano-ext4-sdcard.img.gz) under ./bin/targets/sunxi/arm9/,

