################################################################################
# ROUNDHOUSE
################################################################################

# Copyright 2016-2017 Digital Aggregates Corporation, Colorado, USA.
# "Digital Aggregates Corporation" is a registered trademark.
# Licensed under the terms of the GNU GPL v2.
# https://github.com/coverclock/com-diag-roundhouse
# mailto:coverclock@diag.com

################################################################################

# make image-get
# make overlay-clean image-clean image
# sudo make image-load SINK=</dev/sdSOMETHING>

################################################################################

# R. Graziani, IPV6 FUNDAMENTALS, Cisco Press, 2013
#
# P. Bieringer, LINUX IPv6 HOWTO, 2015-10-16
#
# R. Gilligan, S. Thomson, J. Bound, J. McCann, W. Stevens, "Basic Socket
# Interface Extentions for IPv6", RFC 3493, February 2003
#
# W. Stevens, M. Thomas, E. Nordmark, T. Jinmei, "Advanced Sockets
# Applications Program Interface (API) for IPv6", RFC 3542, May 2003
#
# E. Davies, S. Krishnan, P. Sovola, "IPv6 Transition/Coexistence Security
# Considerations", RFC 4942, September 2007
#
# T. Berners-Lee, R. Fielding, L. Masinter, "Uniform Resource Identifier
# (URI) Syntax", RFC 3986, January 2005
#
# O.Li, T. Jimmel, K. Shima, IPV6 CORE PROTOCOLS IMPLEMENTATION, Morgan
# Kaufmann, 2007

################################################################################

# https://en.wikipedia.org/wiki/IPv6_deployment
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
# http://he.net
# https://tunnelbroker.net
# http://unique-local-ipv6.com
# https://www.sixxs.net/tools/grh/ula/

################################################################################

# Example cfg/$(CONFIG).mk:
#
#   RH_PASSWORD=\$$0\$$abCd1E23\$$fGHI45JkLm6No\/pq4stuV6
#   LA_IP4ADDR=192.168.2.1
#   LA_NETMASK=255.255.255.0
#   LA_IP6PREFIX=fd71:aaaa:bbbb::\/48
#   LA_IP6ADDR=LA_IP6ADDR
#   WA_IP4ADDR=192.168.1.241
#   WA_NETMASK=255.255.255.0
#   WA_GATEWAY=192.168.1.1
#   HE_PEERADDR=123.456.789.012
#   HE_IP6ADDR=1234:456:89:012::\/64
#   HE_IP6PREFIX=2345:678:90:123::\/64
#   HE_TUNNELID=123456
#   HE_USERNAME=abcdef
#   HE_PASSWORD=0a1b2c3d4e5f6g7h
#
# These parameters are derived from Hurrican Electric's sample OpwnWrt
# configuration for your IPv6 tunnel, and other information specific to
# your setup.

################################################################################

# Example overlay/etc/config/firewall rule to forward port:

#   config rule
#           option enabled '1'
#           option target 'ACCEPT'
#           option dest 'lan'
#           option name 'com-diag-diminuto'
#           option family 'ipv6'
#           option dest_port '5555'
#           option src 'wan6'
 
################################################################################

PROJECT:=roundhouse

ROOT:=$(shell pwd)
BUILD:=$(ROOT)/out

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
CONFIG:=375621

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
PACKAGES+=tcpdump

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

CONFIG_FIL=cfg/$(CONFIG).mk

.PHONY:	overlay overlay-clean overlay-check

include $(CONFIG_FIL)

$(BUILD)/overlay/etc/shadow:	overlay/etc/shadow $(CONFIG_FIL)
	mkdir -p $(BUILD)
	test -f $@ || ( tar -cvf - overlay | tar -C $(BUILD) -xvf - )
	sed \
		-e "/^root:/s/::/:$(RH_PASSWORD):/" \
		< $< > $@

$(BUILD)/overlay/etc/config/network:	overlay/etc/config/network $(CONFIG_FIL)
	mkdir -p $(BUILD)
	test -f $@ || ( tar -cvf - overlay | tar -C $(BUILD) -xvf - )
	sed \
		-e "s/LA_IP4ADDR/$(LA_IP4ADDR)/" \
		-e "s/LA_NETMASK/$(LA_NETMASK)/" \
		-e "s/LA_IP6PREFIX/$(LA_IP6PREFIX)/" \
		-e "s/WA_IP4ADDR/$(WA_IP4ADDR)/" \
		-e "s/WA_NETMASK/$(WA_NETMASK)/" \
		-e "s/WA_GATEWAY/$(WA_GATEWAY)/" \
		-e "s/HE_PEERADDR/$(HE_PEERADDR)/" \
		-e "s/HE_IP6ADDR/$(HE_IP6ADDR)/" \
		-e "s/HE_IP6PREFIX/$(HE_IP6PREFIX)/" \
		-e "s/HE_TUNNELID/$(HE_TUNNELID)/" \
		-e "s/HE_USERNAME/$(HE_USERNAME)/" \
		-e "s/HE_PASSWORD/$(HE_PASSWORD)/" \
		< $< > $@

overlay:	$(BUILD)/overlay/etc/shadow $(BUILD)/overlay/etc/config/network

overlay-clean:
	rm -rf $(BUILD)/overlay

overlay-check:
	test -f $(BUILD)/overlay/etc/shadow && cat $(BUILD)/overlay/etc/shadow
	test -f $(BUILD)/overlay/etc/config/network && cat $(BUILD)/overlay/etc/config/network

################################################################################

IMAGE_DIR=OpenWrt-ImageBuilder-$(OPENWRT)-$(SOC)-$(CPU).Linux-$(HOST)
IMAGE_FIL=$(IMAGE_DIR).tar.bz2
IMAGE_URL=https://downloads.openwrt.org/$(CODENAME)/$(OPENWRT)/$(SOC)/$(CPU)/$(IMAGE_FIL)
IMAGE_SOURCE=$(BUILD)/$(IMAGE_DIR)/bin/$(SOC)/openwrt-$(OPENWRT)-$(SOC)-$(CPU)-sdcard-vfat-ext4.img

.PHONY:	image-get image-clean image image-load image-size

image-get:
	mkdir -p $(BUILD)
	( cd $(BUILD); wget -O $(IMAGE_FIL) $(IMAGE_URL); tar -xvjf $(IMAGE_FIL) )

image:	$(BUILD)/overlay/etc/config/network $(BUILD)/overlay/etc/shadow $(BUILD)/$(IMAGE_DIR)
	( cd $(BUILD)/$(IMAGE_DIR); make image PACKAGES="$(PACKAGES)" FILES=${BUILD}/overlay )

image-clean:	$(BUILD)/$(IMAGE_DIR)
	( cd $(BUILD)/$(IMAGE_DIR); make clean )

image-load:	$(IMAGE_SOURCE) $(SINK)
	dd if=$(IMAGE_SOURCE) of=$(SINK) bs=2M conv=fsync

image-size:
	test -f $(IMAGE_SOURCE) && ls -ld $(IMAGE_SOURCE)

################################################################################

.PHONY:	renew

renew:
	ssh-keygen -R $(IPV4)
	ssh-keygen -R $(IPV6)

.PHONY:	browser

BROWSER=firefox

browser4:
	exec $(BROWSER) http://$(IPV4)

browser6:
	exec $(BROWSER) http://[$(IPV6)]

################################################################################
