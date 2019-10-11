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

PKG_BUILD_DEPENDS:=python/host xcbproto/host

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/host-build.mk
$(call include_mk, python-package.mk)

STAMP_CONFIGURED:=$(STAMP_CONFIGURED)_$(call confvar,PACKAGE_python PACKAGE_python)
PYTHON_VERSION:=2.7

define Package/xcbproto
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  BUILDONLY:=1
  TITLE:=xcbproto
  URL:=http://xcb.freedesktop.org/
endef

define InstallPy
	$(INSTALL_DIR) $(1)/usr/lib/python$(PYTHON_VERSION)/site-packages/xcbgen
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/python$(PYTHON_VERSION)/site-packages/xcbgen/*.py \
		$(1)/usr/lib/python$(PYTHON_VERSION)/site-packages/xcbgen/
endef

define Build/InstallDev
	$(call InstallPy,$(1),$(2))
	$(INSTALL_DIR) \
		$(1)/usr/lib/pkgconfig \
		$(1)/usr/share/xcb

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/xcb/* \
		$(1)/usr/share/xcb/

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/
endef

define Package/xcbproto/install
	true
endef

define Host/Install
	$(INSTALL_DIR) $(1)/usr/lib/python$(PYTHON_VERSION)/site-packages/xcbgen
	$(INSTALL_DATA) \
		$(HOST_BUILD_DIR)/xcbgen/*.py \
		$(1)/usr/lib/python$(PYTHON_VERSION)/site-packages/xcbgen/
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,xcbproto))
