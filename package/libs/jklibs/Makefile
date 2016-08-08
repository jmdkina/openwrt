#
# Copyright (C) 2015 OpenWrt-dist
#
# This is free software, licensed under the GNU General Public License v3.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=jklibs
PKG_VERSION:=0.0.1
PKG_RELEASE:=2969857454a65441560d460ade948cbe1b5e4a93

PKG_SOURCE_PROTO:=git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=$(PKG_RELEASE)
PKG_SOURCE_URL:=https://git.oschina.net/jmdvirus/jklibs.git
#PKG_MD5SUM:=4f68731a8ca5db21b3eb994e8c2f1a7a

PKG_LICENSE:=GPLv3
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=jmdvirus <jmdvirus@roamter.com>

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)/$(BUILD_VARIANT)/$(PKG_NAME)-$(PKG_VERSION)

#PKG_INSTALL:=0
#PKG_FIXUP:=autoreconf
PKG_USE_MIPS16:=0
PKG_BUILD_PARALLEL:=1
HOST_BUILD_PARALLEL:=1

#PKG_CONFIG_DEPENDS:=CONFIG_KFROUTER_KFRASCTL CONFIG_KFROUTER_KFFIRMWAREREAD KFROUTER_KFCLIENT KFROUTER_KFROUTERSTART KFROUTER_KFMD5SUM KFROUTER_KFCLIENTPING

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/cmake.mk

TARGET_CFLAGS += -I$(STAGING_DIR)/usr/include

define Package/jklibs/Default
	SECTION:=libs
	CATEGORY:=jk
	TITLE:=jklibs
	URL:=https://git.oschina.net/jmdvirus/jklibs.git
    DEPENDS:=+libpthread +libubox +libjson-c
	MENU:=1
endef

#define Package/jklibs/config
	#source "$(SOURCE)/Config.in"
#endef

Package/jklibs = $(call Package/jklibs/Default)

define Package/jklibs/description
JKLibs
endef

#define Package/kfrouter/conffiles
#endef

#define Package/kfrouter/conffiles
#endef

#Package/shadowsocks-libev-polarssl/conffiles = $(Package/shadowsocks-libev/conffiles)
#Package/shadowsocks-libev-spec-polarssl/conffiles = $(Package/shadowsocks-libev-spec/conffiles)

#define Package/shadowsocks-libev-spec/postinst
##!/bin/sh
#if [ -z "$${IPKG_INSTROOT}" ]; then
#	uci -q batch <<-EOF >/dev/null
#		delete firewall.shadowsocks
#		set firewall.shadowsocks=include
#		set firewall.shadowsocks.type=script
#		set firewall.shadowsocks.path=/usr/share/shadowsocks/firewall.include
#		set firewall.shadowsocks.reload=1
#		commit firewall
#EOF
#fi
#exit 0
#endef

#Package/shadowsocks-libev-spec-polarssl/postinst = $(Package/shadowsocks-libev-spec/postinst)

#ifeq ($(BUILD_VARIANT),polarssl)
	#CONFIGURE_ARGS += --with-crypto-library=polarssl
#endif

#define Build/Prepare
#	cp -rf ./src/* $(PKG_BUILD_DIR)
#endef

#define Host/Prepare
#	mkdir -p $(HOST_BUILD_DIR)
#endef

define Host/Compile
	cd $(HOST_BUILD_DIR); $(MAKE) pc; make CC="$(HOSTCC)"
endef

define Host/jklibs/install
	$(INSTALL_BIN) $(HOST_BUILD_DIR)/kffirmware/demo_firmware $(STAGING_DIR_HOST)/bin/mkfirmware
	$(INSTALL_BIN) $(HOST_BUILD_DIR)/kffirmware/demo_firmware_read $(STAGING_DIR_HOST)/bin/kffirmwareread
endef

define Host/Install
	$(call Host/kfrouter/install)
endef

#define Build/Compile
#	+$(MAKE) mips
#	$(MAKE) 
#endef

#ifeq ($(CONFIG_KFROUTER_KFRASCTL), y)
#	$(INSTALL_BIN) $(PKG_BUILD_DIR)/kfrasctl/kfrasctl $(1)/usr/bin
#endif

define Package/jklibs/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/demo/jsonc_demo $(STAGING_DIR)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/demo/list_demo $(STAGING_DIR)/usr/bin/
endef

#Package/kfrouter/install = $(Package/kfrouter-prog/install)

$(eval $(call BuildPackage,jklibs))
#$(eval $(call HostBuild))

