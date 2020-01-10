#
# Copyright (C) 2008-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xorgconf-ext
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_SOURCE_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/xorgconf-ext
  SECTION:=xorg-data
  CATEGORY:=Xorg
  SUBMENU:=data
  TITLE:=xorgconf-ext
  URL:=http://freedesktop.org/wiki
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/xorgconf/install
	$(INSTALL_DIR) $(1)/etc/X11/xorg.conf.d
	$(INSTALL_DATA) ./src/* $(1)/etc/X11/xorg.conf.d/
endef

$(eval $(call BuildPackage,xorgconf-ext))
