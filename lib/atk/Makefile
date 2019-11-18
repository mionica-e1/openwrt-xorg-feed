#
# Copyright (C) 2006-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=atk
PKG_VERSION_MAJOR:=2.22
PKG_VERSION:=2.22.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@GNOME/$(PKG_NAME)/$(PKG_VERSION_MAJOR)/
PKG_HASH:=d349f5ca4974c9c76a4963e5b254720523b0c78672cbc0e1a3475dbd9b3d44b6

PKG_FIXUP:=libtool

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/atk
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  TITLE:=Accesibility library for gtk+ apps
  DEPENDS:=+glib2
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/{lib,include}
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib* $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/ $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
endef

define Package/atk/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib*so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,atk))
