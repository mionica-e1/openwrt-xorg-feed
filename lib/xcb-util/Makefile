#
# Copyright (C) 2008-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xcb-util
PKG_VERSION:=0.3.9
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://xcb.freedesktop.org/dist/
PKG_HASH:=c611259c0ab20fd76f79f48f4684843c18ea9c967eba78a45e8b3636315c18c4
PKG_INSTALL:=1

PKG_BUILD_DEPENDS:=python/host xcbproto/host

include $(INCLUDE_DIR)/package.mk

define Package/xcb-util
  TITLE:=xcb util
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=+libxcb
  URL:=http://xcb.freedesktop.org/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/xcb
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/include/xcb/*.h \
		$(1)/usr/include/xcb/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.{so*,a,la} \
		$(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/
endef

define Package/xcb-util/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so* \
		$(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/
endef

$(eval $(call BuildPackage,xcb-util))
