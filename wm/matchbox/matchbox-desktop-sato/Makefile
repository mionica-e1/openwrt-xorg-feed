#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=matchbox-desktop-sato
PKG_RELEASE:=1
PKG_VERSION:=1.0
PKG_SOURCE_URL:=https://github.com/suwus/matchbox-desktop-sato.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2019-11-19
PKG_SOURCE_VERSION:=4a02b6408565f083802592f152e05dee9b40e05b
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_FIXUP:=libtool

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

PKG_INSTALL:=1

define Package/matchbox-desktop-sato
  SECTION:=xorg-matchbox
  CATEGORY:=Xorg
  SUBMENU:=Matchbox Window manager
  TITLE:=matchbox-desktop-sato
  URL:=http://matchbox-project.org
endef

define Package/matchbox-desktop-sato/description
 Matchbox Desktop 2 Sato Configuration
endef

define Package/matchbox-desktop-sato/install
	$(INSTALL_DIR) $(1)/usr/share/matchbox/vfolders
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/matchbox/vfolders/* \
		$(1)/usr/share/matchbox/vfolders/
endef

$(eval $(call BuildPackage,matchbox-desktop-sato))
