#
# Copyright (C) 2006-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=font-util
PKG_VERSION:=1.3.1
PKG_RELEASE:=4

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://xorg.freedesktop.org/releases/individual/font
PKG_HASH:=aa7ebdb0715106dd255082f2310dbaa2cd7e225957c2a77d719720c7cc92b921

include $(INCLUDE_DIR)/package.mk

define Package/font-util
  SECTION:=xorg-font
  CATEGORY:=Xorg
  SUBMENU:=app
  TITLE:=misc tool to generate x fonts
  DEPENDS:=+xserver
  URL:=http://xorg.freedesktop.org/
endef

define Build/Configure
	cd  $(PKG_BUILD_DIR)/; ./configure  
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)
	$(MAKE) -C $(PKG_BUILD_DIR) install DESTDIR="$(PKG_INSTALL_DIR)"
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig $(1)/usr/share $(2)/bin
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/local/lib/pkgconfig/fontutil.pc $(1)/usr/lib/pkgconfig/
	$(CP) -r $(PKG_INSTALL_DIR)/usr/local/share/* $(1)/usr/share/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/local/bin/* $(2)/bin/
endef

$(eval $(call BuildPackage,font-util))
