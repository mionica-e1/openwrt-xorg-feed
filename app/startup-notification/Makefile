#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=startup-notification
PKG_RELEASE:=1
PKG_VERSION_MAJOR:=1.0
PKG_VERSION:=0.12
PKG_SOURCE_URL:=http://freedesktop.org/software/$(PKG_NAME)/releases
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_MD5SUM:=2cd77326d4dcaed9a5a23a1232fb38e9
PKG_FIXUP:=libtool

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

PKG_INSTALL:=1

define Package/startup-notification
  SECTION:=xorg-app
  CATEGORY:=Xorg
  SUBMENU:=app
  DEPENDS:=+libX11 +xcb-util
  TITLE:=startup notification
  URL:=https://freedesktop.org/
endef

define Build/Configure
	$(call Build/Configure/Default, \
		--with-x \
		lf_cv_sane_realloc=yes \
	)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/$(PKG_NAME)-$(PKG_VERSION_MAJOR)/libsn
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/include/$(PKG_NAME)-$(PKG_VERSION_MAJOR)/libsn/*.h \
		$(1)/usr/include/$(PKG_NAME)-$(PKG_VERSION_MAJOR)/libsn/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.{so*,a,la} \
		$(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/
endef

define Package/startup-notification/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so* \
		$(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/
endef

$(eval $(call BuildPackage,startup-notification))
