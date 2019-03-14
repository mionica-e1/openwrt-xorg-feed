#
# Copyright (C) 2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=util-macros
PKG_VERSION:=1.19.2
PKG_RELEASE:=1

PKG_SOURCE:=${PKG_NAME}-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://www.x.org/releases/individual/util/
PKG_MD5SUM:=5059b328fac086b733ffac6607164c41
PKG_FIXUP:=libtool

include $(INCLUDE_DIR)/package.mk

define Package/xorg-macros
  SECTION:=xorg-utils
  CATEGORY:=Xorg
  SUBMENU:=utils
  TITLE:=xorg aclocal macros
  DEPENDS:=
  URL:=http://xorg.freedesktop.org/
endef

define Package/xorg-macros/description
This package contains the aclocal macros needed for building xorg modules
from upstream source.
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/share/pkgconfig/
	$(CP) $(PKG_BUILD_DIR)/xorg-macros.pc $(1)/usr/share/pkgconfig/

	$(INSTALL_DIR) $(1)/usr/share/aclocal
	$(CP) $(PKG_BUILD_DIR)/xorg-macros.m4 $(1)/usr/share/aclocal/
	$(CP) $(PKG_BUILD_DIR)/xorgversion.m4 $(1)/usr/share/aclocal/
endef

define Package/xorg-macros/install
	true
endef

$(eval $(call BuildPackage,xorg-macros))