#
# Copyright (C) 2008-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xkeyboard-config
PKG_VERSION:=2.20
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://www.x.org/releases/individual/data/xkeyboard-config
PKG_HASH:=d1bfc72553c4e3ef1cd6f13eec0488cf940498b612ab8a0b362e7090c94bc134
PKG_BUILD_DEPENDS:=intltool/host

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/xkeyboard-config
  SECTION:=xorg-data
  CATEGORY:=Xorg
  SUBMENU:=data
  TITLE:=xkeyboard-config
  DEPENDS:=+xkbcomp
  URL:=http://freedesktop.org/wiki/Software/XKeyboardConfig
endef

define Package/xkeyboard-config/install
	$(INSTALL_DIR) $(1)/usr/share/X11
	$(CP) $(PKG_INSTALL_DIR)/usr/share/X11/xkb $(1)/usr/share/X11/
endef

$(eval $(call BuildPackage,xkeyboard-config))
