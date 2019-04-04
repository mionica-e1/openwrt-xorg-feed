#
# Copyright (C) 2006-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org
include $(TOPDIR)/rules.mk

PKG_NAME:=glproto
PKG_VERSION:=1.4.17
PKG_RELEASE:=2

PKG_SOURCE_URL:=http://xorg.freedesktop.org/releases/individual/proto/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_BUILD_DIR:=$(BUILD_DIR)/Xorg/$(PKG_NAME)-$(PKG_VERSION)/
PKG_HASH:=adaa94bded310a2bfcbb9deb4d751d965fcfe6fb3a2f6d242e2df2d6589dbe40

include $(INCLUDE_DIR)/package.mk

define Package/glproto
  SECTION:=xorg-proto
  CATEGORY:=Xorg
  SUBMENU:=proto
  DEPENDS:=
  TITLE:=glproto
  URL:=http://xorg.freedesktop.org/
endef

define Build/InstallDev
	DESTDIR="$(1)" $(MAKE) -C $(PKG_BUILD_DIR)/ $(MAKE_FLAGS) install
endef

define Build/Compile
	true
endef

$(eval $(call BuildPackage,glproto))
