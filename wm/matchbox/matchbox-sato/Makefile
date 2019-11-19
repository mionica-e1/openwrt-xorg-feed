#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=matchbox-sato
PKG_RELEASE:=1
PKG_VERSION:=1.0
PKG_SOURCE_URL:=https://github.com/suwus/matchbox-sato.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2019-11-19
PKG_SOURCE_VERSION:=df085ba9cdaeaf2956890b0e29d7ea1779bf6c78
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_FIXUP:=libtool

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

PKG_INSTALL:=1

define Package/matchbox-sato
  SECTION:=xorg-matchbox
  CATEGORY:=Xorg
  SUBMENU:=Matchbox Window manager
  DEPENDS:=+libmatchbox
  TITLE:=matchbox-sato
  URL:=http://matchbox-project.org
endef

define Package/matchbox-sato/description
 Matchbox Window Manager Sato Theme
endef

define Package/matchbox-sato/install
	$(INSTALL_DIR) $(1)/usr/share/themes/Sato/matchbox
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/themes/Sato/matchbox/* \
		$(1)/usr/share/themes/Sato/matchbox/
endef

$(eval $(call BuildPackage,matchbox-sato))
