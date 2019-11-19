#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=matchbox-themes-extra
PKG_RELEASE:=1
PKG_VERSION:=1.0
PKG_SOURCE_URL:=https://github.com/suwus/matchbox-themes-extra.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2019-11-19
PKG_SOURCE_VERSION:=f848f9e4e577d5b9719f05b5152df1ce59399f5c
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_FIXUP:=libtool

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

PKG_INSTALL:=1

define Package/matchbox-themes-extra
  SECTION:=xorg-matchbox
  CATEGORY:=Xorg
  SUBMENU:=Matchbox Window manager
  TITLE:=matchbox-themes-extra
  URL:=http://matchbox-project.org
endef

define Package/matchbox-themes-extra/description
 Matchbox Window Manager Extra Themes
endef

define Package/matchbox-themes-extra/install
	true
endef

$(eval $(call BuildPackage,matchbox-themes-extra))
