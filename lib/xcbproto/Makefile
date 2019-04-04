#
# Copyright (C) 2008-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xcb-proto
PKG_VERSION:=1.13
PKG_RELEASE:=3

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://xcb.freedesktop.org/dist/
PKG_HASH:=7b98721e669be80284e9bbfeab02d2d0d54cd11172b72271e47a2fe875e2bde1
PKG_INSTALL:=1

#PKG_BUILD_DEPENDS:=python-mini/host

include $(INCLUDE_DIR)/package.mk
#$(call include_mk, python-package.mk)

#STAMP_CONFIGURED:=$(STAMP_CONFIGURED)_$(call confvar,PACKAGE_python PACKAGE_python-mini)

define Package/xcbproto
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  BUILDONLY:=1
  TITLE:=xcbproto
  URL:=http://xcb.freedesktop.org/
endef

#define InstallPy
#	$(INSTALL_DIR) $(1)/host/lib/$(PYTHON)/site-packages/xcbgen
#	$(INSTALL_DATA) \
#		$(PKG_INSTALL_DIR)/usr/lib/$(PYTHON)/site-packages/xcbgen/*.py \
#		$(1)/host/lib/$(PYTHON)/site-packages/xcbgen/
#endef

define Build/InstallDev
#	$(call InstallPy,$(1),$(2))
	$(INSTALL_DIR) \
		$(1)/usr/lib/pkgconfig \
		$(1)/host/share/xcb

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/xcb/* \
		$(1)/host/share/xcb/

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/

	$(SED) 's,datadir=/usr,datadir=$(STAGING_DIR)/host,g' $(1)/usr/lib/pkgconfig/xcb-proto.pc
endef

$(eval $(call BuildPackage,xcbproto))
