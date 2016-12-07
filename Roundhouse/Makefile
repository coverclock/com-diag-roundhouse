################################################################################
# ROUNDHOUSE
################################################################################

# Copyright 2016 Digital Aggregates Corporation, Colorado, USA.
# "Digital Aggregates Corporation" is a registered trademark.
# Licensed under the terms of the GNU GPL v2.
# https://github.com/coverclock/com-diag-roundhouse
# mailto:coverclock@diag.com

################################################################################

# https://github.com/raspberrypi/tools
# https://github.com/openwrt/openwrt
# https://downloads.openwrt.org/chaos_calmer/15.05.1/brcm2708/bcm2709/
# https://wiki.openwrt.org/start
# https://wiki.openwrt.org/toh/raspberry_pi_foundation/raspberry_pi
# https://wiki.openwrt.org/doc/recipes/ltedongle
# https://wiki.openwrt.org/doc/uci
# https://www.verizonwireless.com/dam/support/pdf/user_guide/u620-linux-integration-guide-7-17-15.pdf
# https://forums.hak5.org/index.php?/topic/37131-questions-about-3g-4g-modems/
# http://permalink.gmane.org/gmane.linux.usb.general/133344
# https://downloads.openwrt.org/chaos_calmer/15.05.1/brcm2708/bcm2709/packages/
# http://devopscube.com/gnutls-handshake-failed-aws-codecommit/
# https://answers.launchpad.net/ubuntu/+source/pycurl/+question/221185
# https://downloads.openwrt.org/chaos_calmer/15.05.1/brcm2708/bcm2709/OpenWrt-ImageBuilder-15.05.1-brcm2708-bcm2709.Linux-x86_64.tar.bz2
# https://downloads.openwrt.org/chaos_calmer/15.05.1/brcm2708/bcm2709/OpenWrt-SDK-15.05.1-brcm2708-bcm2709_gcc-4.8-linaro_uClibc-0.9.33.2_eabi.Linux-x86_64.tar.bz2
# https://www.rivy.org/2012/09/enable-ipv6-on-openwrt/
# https://wiki.openwrt.org/doc/uci/network6
# https://wiki.openwrt.org/doc/howto/generic.backup
# http://mirrors.deepspace6.net/Linux+IPv6-HOWTO/
# http://www.tldp.org/HOWTO/pdf/Linux+IPv6-HOWTO.pdf

################################################################################

PROJECT:=roundhouse

ROOT:=$(shell pwd)
BUILD:=$(HOME)/Projects/com-diag-$(PROJECT)

IPV4:=192.168.2.1
IPV6:=fd71:9abb:2f8a::1

CODENAME:=chaos_calmer
OPENWRT:=15.05.1
ARCH:=arm
CROSS_COMPILE:=arm-openwrt-linux-uclibcgnueabi-
CORE:=cortex-a7+vfp
KERNEL:=3.18.23
GCC:=4.8-linaro
UCLIBC:=0.9.33.2_eabi
SOC:=brcm2708
CPU:=bcm2709
HOST:=x86_64

PACKAGES:=
PACKAGES+=kmod-mii
PACKAGES+=kmod-usb-net
PACKAGES+=kmod-usb-net-asix-ax88179
PACKAGES+=kmod-usb-net-cdc-ether
PACKAGES+=kmod-usb-net-qmi-wwan
PACKAGES+=kmod-usb-serial
PACKAGES+=kmod-usb-serial-wwan
PACKAGES+=kmod-usb-wdm
PACKAGES+=kmod-ipv6
PACKAGES+=ip6tables
PACKAGES+=ip
PACKAGES+=6in4
PACKAGES+=libpthread
PACKAGES+=librt
PACKAGES+=libusb-1.0
PACKAGES+=uqmi
PACKAGES+=usb-modeswitch
PACKAGES+=usbutils
PACKAGES+=wwan
PACKAGES+=zlib
PACKAGES+=luci
PACKAGES+=luci-base
PACKAGES+=luci-mod-admin-full
PACKAGES+=luci-app-firewall
PACKAGES+=luci-theme-bootstrap
PACKAGES+=luci-proto-ipv6
PACKAGES+=luci-proto-ppp
PACKAGES+=luci-lib-ip
PACKAGES+=luci-lib-nixio
PACKAGES+=chat
PACKAGES+=comgt

PLATFORM:=$(ARCH)_$(CORE)_uClibc-$(UCLIBC)
TOOLCHAIN:=$(ARCH)_$(CORE)_gcc-$(GCC)_uClibc-$(UCLIBC)
TARGET:=$(SOC)_$(CPU)
LINUX:=$(BUILD)/openwrt/build_dir/target-$(PLATFORM)/linux-$(TARGET)/linux-$(KERNEL)

STAGING_DIR:=$(BUILD)/openwrt/staging_dir/toolchain-$(TOOLCHAIN)

HOSTPATH:=$(BUILD)/openwrt/staging_dir/host/bin
TOOLPATH:=$(STAGING_DIR)/bin
PATH:=$(HOSTPATH):$(TOOLPATH):$(PATH)

export ARCH
export CROSS_COMPILE
export PATH
export STAGING_DIR

SINK:=/dev/null

################################################################################

.PHONY:	default

default:	image

################################################################################

SDK_DIR=OpenWrt-SDK-$(OPENWRT)-$(SOC)-$(CPU)_gcc-$(GCC)_uClibc-$(UCLIBC).Linux-$(HOST)
SDK_FIL=$(SDK_DIR).tar.bz2
SDK_URL=https://downloads.openwrt.org/$(CODENAME)/$(OPENWRT)/$(SOC)/$(CPU)/$(SDK_FIL)

.PHONY:		sdk-get

sdk-get:
	mkdir -p $(BUILD)
	( cd $(BUILD); wget -O $(SDK_FIL) $(SDK_URL); tar -xvjf $(SDK_FIL) )

################################################################################

IMAGE_DIR=OpenWrt-ImageBuilder-$(OPENWRT)-$(SOC)-$(CPU).Linux-$(HOST)
IMAGE_FIL=$(IMAGE_DIR).tar.bz2
IMAGE_URL=https://downloads.openwrt.org/$(CODENAME)/$(OPENWRT)/$(SOC)/$(CPU)/$(IMAGE_FIL)

.PHONY: image-get

image-get:
	mkdir -p $(BUILD)
	( cd $(BUILD); wget -O $(IMAGE_FIL) $(IMAGE_URL); tar -xvjf $(IMAGE_FIL) )

################################################################################

.PHONY:	overlay-generate overlay-clean

include $(HOME)/.$(PROJECT)

$(BUILD)/overlay/etc/shadow:	overlay/etc/shadow $(HOME)/.$(PROJECT)
	test -f $@ || ( tar -cvf - overlay | tar -C $(BUILD) -xvf - )
	sed \
		-e "/^root:/s/::/:$(SU_PASSWORD):/" \
		< $< > $@

$(BUILD)/overlay/etc/config/network:	overlay/etc/config/network $(HOME)/.$(PROJECT)
	test -f $@ || ( tar -cvf - overlay | tar -C $(BUILD) -xvf - )
	sed \
		-e "s/PEERADDR/$(HE_PEERADDR)/" \
		-e "s/IP6ADDR/$(HE_IP6ADDR)/" \
		-e "s/IP6PREFIX/$(HE_IP6PREFIX)/" \
		-e "s/TUNNELID/$(HE_TUNNELID)/" \
		-e "s/USERNAME/$(HE_USERNAME)/" \
		-e "s/PASSWORD/$(HE_PASSWORD)/" \
		< $< > $@

overlay-generate:	$(BUILD)/overlay/etc/shadow $(BUILD)/overlay/etc/config/network

overlay-clean:
	rm -rf $(BUILD)/overlay

################################################################################

.PHONY:	image image-clean

image:	$(BUILD)/overlay/etc/config/network $(BUILD)/overlay/etc/shadow $(BUILD)/$(IMAGE_DIR)
	( cd $(BUILD)/$(IMAGE_DIR); make image PACKAGES="$(PACKAGES)" FILES=${BUILD}/overlay )

image-clean:	$(BUILD)/$(IMAGE_DIR)
	( cd $(BUILD)/$(IMAGE_DIR); make clean )

################################################################################

IMAGE_SOURCE=$(BUILD)/$(IMAGE_DIR)/bin/$(SOC)/openwrt-$(OPENWRT)-$(SOC)-$(CPU)-sdcard-vfat-ext4.img

.PHONY:	image-load

image-load:	$(IMAGE_SOURCE) $(SINK)
	dd if=$(IMAGE_SOURCE) of=$(SINK) bs=2M conv=fsync

################################################################################

.PHONY:	renew

renew:
	ssh-keygen -R $(IPV4)
	ssh-keygen -R $(IPV6)

################################################################################

.PHONY:	browser

BROWSER=firefox

browser4:
	exec $(BROWSER) http://$(IPV4)

browser6:
	exec $(BROWSER) http://[$(IPV6)]

################################################################################
