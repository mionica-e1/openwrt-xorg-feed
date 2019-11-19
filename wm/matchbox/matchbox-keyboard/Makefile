#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=matchbox-keyboard
PKG_RELEASE:=1
PKG_VERSION:=0.1
PKG_SOURCE_URL:=http://downloads.yoctoproject.org/releases/matchbox/$(PKG_NAME)/$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_MD5SUM:=50940321d59fee23b38a4941100abf25
PKG_FIXUP:=libtool

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

PKG_INSTALL:=1

define Package/matchbox-keyboard
  SECTION:=xorg-matchbox
  CATEGORY:=Xorg
  SUBMENU:=Matchbox Window manager
  DEPENDS:=+libmatchbox +libXft +libfakekey
  TITLE:=matchbox-keyboard
  URL:=http://matchbox-project.org
endef

CONFIGURE_ARGS+= \
	--disable-cairo

define Package/matchbox-keyboard/install
	$(INSTALL_DIR) $(1)/usr/{bin,share}
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/bin/* \
		$(1)/usr/bin/

	$(INSTALL_DIR) $(1)/usr/share/{applications,locale,pixmaps}
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/applications/* \
		$(1)/usr/share/applications/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/pixmaps/* \
		$(1)/usr/share/pixmaps/
endef

$(eval $(call BuildPackage,matchbox-keyboard))
