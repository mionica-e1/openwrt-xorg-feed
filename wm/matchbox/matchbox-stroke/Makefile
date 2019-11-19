#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=matchbox-stroke
PKG_RELEASE:=1
PKG_VERSION:=1.0
PKG_SOURCE_URL:=https://github.com/suwus/matchbox-stroke.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2019-11-19
PKG_SOURCE_VERSION:=2b772583b61d2f6e8358e7c80e10293fc27cfcb7
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_FIXUP:=libtool

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

PKG_INSTALL:=1

define Package/matchbox-stroke
  SECTION:=xorg-matchbox
  CATEGORY:=Xorg
  SUBMENU:=Matchbox Window manager
  DEPENDS:=+libmatchbox +libfakekey +libXtst
  TITLE:=matchbox-stroke
  URL:=http://matchbox-project.org
endef

define Package/matchbox-stroke/description
 Matchbox touchscreen input method
endef

CONFIGURE_ARGS+= \
	--enable-expat \
	--enable-dnotify \
	--disable-acpi-linux

define Package/matchbox-stroke/install
	$(INSTALL_DIR) $(1)/usr/{bin,share}
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/bin/* \
		$(1)/usr/bin/

	$(INSTALL_DIR) $(1)/usr/share/{applications,matchbox-stroke,pixmaps}

	$(INSTALL_DIR) $(1)/usr/share/applications/inputmethods
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/applications/inputmethods/* \
		$(1)/usr/share/applications/inputmethods/

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/matchbox-stroke/* \
		$(1)/usr/share/matchbox-stroke/

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/pixmaps/* \
		$(1)/usr/share/pixmaps/
endef

$(eval $(call BuildPackage,matchbox-stroke))
