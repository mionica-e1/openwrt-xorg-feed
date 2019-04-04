#
# Copyright (C) 2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#


include $(TOPDIR)/rules.mk

PKG_NAME:=libpthread-stubs
PKG_VERSION:=0.4
PKG_RELEASE:=1
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_HASH:=50d5686b79019ccea08bcbd7b02fe5a40634abcfd4146b6e75c6420cc170e9d9
PKG_SOURCE_URL:=http://xcb.freedesktop.org/dist/
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=COPYING
PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_MAINTAINER:=Han Pengfei <pengphei@foxmail.com>

include $(INCLUDE_DIR)/package.mk


define Package/libpthread-stubs
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:= weak aliases for pthread functions not provided in libc
  URL:=http://xcb.freedesktop.org/
endef

define Package/libpthread-stubs/description
  The libpthread-stubs package provides weak aliases for pthread 
  functions not provided in libc or otherwise available by default. 
  This is useful for libraries that rely on pthread stubs to use 
  pthreads optionally. On Linux, all necessary pthread functions 
  are available, so this package is simply a placeholder.
endef

define Package/compile
  true
endef

define Package/libpthread-stubs/install
  true
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig/

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/
endef

$(eval $(call BuildPackage,libpthread-stubs))
