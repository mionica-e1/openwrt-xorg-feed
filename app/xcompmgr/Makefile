#
# Copyright (C) 2020 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xcompmgr
PKG_RELEASE:=1
PKG_VERSION:=1.1.8
PKG_SOURCE_URL:=http://xorg.freedesktop.org/releases/individual/app/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_BUILD_DIR:=$(BUILD_DIR)/Xorg/$(PKG_NAME)-$(PKG_VERSION)/

PKG_MD5SUM:=ef8c7d4140c11efb8de4141b3968208c
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/xcompmgr
  SECTION:=xorg-app
  CATEGORY:=Xorg
  SUBMENU:=app
  DEPENDS:=+libX11 +libXcomposite +libXdamage +libXext +libXfixes +libXrender
  TITLE:=xrandr
  URL:=http://xorg.freedesktop.org/
endef

define Package/xcompmgr/Default/description
 xcompmgr is a sample compositing manager that enables basic eye-candy effects.
endef

define Package/xcompmgr/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/* \
		$(1)/usr/bin/
endef

$(eval $(call BuildPackage,xcompmgr))
