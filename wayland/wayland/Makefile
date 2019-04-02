#
# Copyright (C) 2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=wayland
PKG_VERSION:=1.16.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://wayland.freedesktop.org/releases/
PKG_MD5SUM:=0c215e53de71d6fb26f7102cdc6432d3

PKG_INSTALL:=1
PKG_FIXUP:=libtool

PKG_BUILD_DEPENDS:=wayland/host libxml2/host

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/host-build.mk

define Package/wayland
  SECTION:=wayland
  CATEGORY:=Wayland
  TITLE:=wayland core library
  DEPENDS:=@!avr32 +libffi +libexpat +libxml2
  URL:=https://wayland.freedesktop.org/
endef

CONFIGURE_ARGS+= \
	--enable-shared \
	--enable-static \
	--with-host-scanner \
	--disable-documentation 

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.{so*,a,la} $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* $(1)/usr/lib/pkgconfig/
	$(INSTALL_DIR) $(1)/usr/include/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/share/aclocal
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/aclocal/* $(1)/usr/share/aclocal/
	$(INSTALL_DIR) $(1)/usr/share/wayland
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/wayland/* $(1)/usr/share/wayland/
endef

define Package/wayland/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
endef

HOST_CONFIGURE_ARGS+= \
	--enable-shared \
	--enable-static \
	--disable-documentation \
	--without-libxml2-prefix

define Host/Install
       $(call Host/Install/Default)
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,wayland))
