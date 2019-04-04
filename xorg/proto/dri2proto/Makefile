#
# Copyright (C) 2009-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=dri2proto
PKG_VERSION:=2.8
PKG_RELEASE:=2

PKG_SOURCE_URL:=http://xorg.freedesktop.org/releases/individual/proto/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_BUILD_DIR:=$(BUILD_DIR)/Xorg/$(PKG_NAME)-$(PKG_VERSION)/
PKG_HASH=f9b55476def44fc7c459b2537d17dbc731e36ed5d416af7ca0b1e2e676f8aa04

include $(INCLUDE_DIR)/package.mk

define Package/dri2proto
  SECTION:=xorg-proto
  CATEGORY:=Xorg
  SUBMENU:=proto
  TITLE:=dri2proto
  URL:=http://xorg.freedesktop.org/
endef

define Build/InstallDev
	DESTDIR="$(1)" $(MAKE) -C $(PKG_BUILD_DIR)/ $(MAKE_FLAGS) install
endef

define Build/Compile
	true
endef

$(eval $(call BuildPackage,dri2proto))
