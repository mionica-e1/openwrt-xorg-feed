#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=sato-icon-theme
PKG_RELEASE:=1
PKG_VERSION:=1.0
PKG_SOURCE_URL:=https://github.com/suwus/sato-icon-theme.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2019-11-19
PKG_SOURCE_VERSION:=b9f02989310a3c920589f1aa646bcbf16b2572a0
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_FIXUP:=libtool

PKG_BUILD_DEPENDS:=icon-naming-utils/host

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

PKG_INSTALL:=1

define Package/sato-icon-theme
  SECTION:=xorg-matchbox
  CATEGORY:=Xorg
  SUBMENU:=Matchbox Window manager
  TITLE:=sato-icon-theme
  DEPENDS:=+icon-naming-utils
  URL:=http://matchbox-project.org
endef

define Package/sato-icon-theme/description
 Matchbox Sato Icon Theme
endef

define Package/sato-icon-theme/install
	$(INSTALL_DIR) $(1)/usr/share/matchbox/vfolders
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/matchbox/vfolders/* \
		$(1)/usr/share/matchbox/vfolders/
endef

$(eval $(call BuildPackage,sato-icon-theme))