#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=libmatchbox
PKG_RELEASE:=3
PKG_VERSION:=1.12
PKG_SOURCE_URL:=https://git.yoctoproject.org/cgit/cgit.cgi/${PKG_NAME}/snapshot
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_MD5SUM:=c3e952b903621423e46c1c4a513c53d6
PKG_FIXUP:=libtool

EXTRA_LDFLAGS+=-Wl,-rpath-link=$(STAGING_DIR)/usr/lib/

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

PKG_INSTALL:=1

define Package/libmatchbox
  SECTION:=xorg-matchbox
  CATEGORY:=Xorg
  SUBMENU:=Matchbox Window manager
  DEPENDS:=+libX11 +libXft +libpng +libjpeg +libXext +pango
  TITLE:=libmatchbox
  URL:=http://matchbox-project.org
endef

define Build/Configure
	$(call Build/Configure/Default, \
		--enable-pango \
		--enable-jpeg \
		--enable-png \
		--enable-Xft \
		--enable-unit-tests=no \
	)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/libmb
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/include/libmb/*.h \
		$(1)/usr/include/libmb/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libmb.{so*,a,la} \
		$(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/
endef

define Package/libmatchbox/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libmb.so* \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,libmatchbox))
