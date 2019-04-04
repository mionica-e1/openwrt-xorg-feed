#
# Copyright (C) 2007-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xtrans
PKG_RELEASE:=2
PKG_VERSION:=1.3.5

PKG_SOURCE_URL:=http://xorg.freedesktop.org/releases/individual/lib
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_BUILD_DIR:=$(BUILD_DIR)/Xorg/$(PKG_NAME)-$(PKG_VERSION)/
PKG_HASH:=adbd3b36932ce4c062cd10f57d78a156ba98d618bdb6f50664da327502bc8301

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/xtrans
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  TITLE:=xtrans
  URL:=http://xorg.freedesktop.org/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/{lib/pkgconfig,include/X11/Xtrans}
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/include/X11/Xtrans/* \
		$(1)/usr/include/X11/Xtrans/

	$(INSTALL_DIR) $(1)/usr/share/aclocal
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/aclocal/* \
		$(1)/usr/share/aclocal/
endef

$(eval $(call BuildPackage,xtrans))
