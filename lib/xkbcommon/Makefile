#
# Copyright (C) 2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libxkbcommon
PKG_VERSION:=0.8.4
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://xkbcommon.org/download/
PKG_MD5SUM:=3c4409058dfd203f641a563358e0187d

PKG_INSTALL:=1
PKG_FIXUP:=libtool autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/libxkbcommon
  SECTION:=libxkbcommon
  CATEGORY:=Xorg
  SUBMENU:=libraries
  TITLE:=xkbcommon library
  
  DEPENDS:=@!avr32 +xorg-macros\
  +FEATURE_with_x11:xserver

  URL:=https://xkbcommon.org/
endef

define Package/libxkbcommon/description
xkbcommon is a library for handling of keyboard descriptions, 
including loading them from disk, parsing them and handling 
their state. It's mainly meant for client toolkits, window 
systems, and other system applications;
endef

CONFIGURE_ARGS+= \
	--enable-shared \
	--enable-static \
	--disable-documentation \
	$(if $(CONFIG_FEATURE_with_x11), --enable-x11, --disable-x11) 

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.{so*,a,la} $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* $(1)/usr/lib/pkgconfig/
	$(INSTALL_DIR) $(1)/usr/include/xkbcommon
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/include/xkbcommon/* $(1)/usr/include/xkbcommon
endef

define Package/libxkbcommon/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libxkbcommon))
