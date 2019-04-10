#
# Copyright (C) 2009-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libXcomposite
PKG_RELEASE:=2
PKG_VERSION:=0.4.4

PKG_SOURCE_URL:=http://xorg.freedesktop.org/releases/individual/lib/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_BUILD_DIR:=$(BUILD_DIR)/Xorg/$(PKG_NAME)-$(PKG_VERSION)/
PKG_HASH:=ede250cd207d8bee4a338265c3007d7a68d5aca791b6ac41af18e9a2aeb34178

PKG_FIXUP:=libtool
PKG_INSTALL:=1
PKG_BUILD_DEPENDS:=compositeproto fixesproto

include $(INCLUDE_DIR)/package.mk

define Package/libXcomposite
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=+libX11 +libXfixes +libXext
  TITLE:=libXcomposite
  URL:=http://xorg.freedesktop.org/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/{lib/pkgconfig,include/X11/extensions}
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.{so*,a,la} \
		$(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/include/X11/extensions/* \
		$(1)/usr/include/X11/extensions/
endef

define Package/libXcomposite/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so* \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,libXcomposite))
