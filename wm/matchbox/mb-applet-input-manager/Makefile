#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=mb-applet-input-manager
PKG_RELEASE:=1
PKG_VERSION:=0.6
PKG_SOURCE_URL:=http://downloads.yoctoproject.org/releases/matchbox/$(PKG_NAME)/$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_MD5SUM:=8a7ac22fdbbc7d3fdbfd0d7e98bb0de0
PKG_FIXUP:=libtool

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

PKG_INSTALL:=1

define Package/mb-applet-input-manager
  SECTION:=xorg-matchbox
  CATEGORY:=Xorg
  SUBMENU:=Matchbox Window manager
  DEPENDS:=+libmatchbox +startup-notification
  TITLE:=matchbox input manager applet
  URL:=http://matchbox-project.org
endef

CONFIGURE_ARGS+= \
	--enable-expat \
	--enable-startup-notification \
	--enable-dnotify

define Package/mb-applet-input-manager/install
	$(INSTALL_DIR) $(1)/usr/{bin,share}
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/* \
		$(1)/usr/bin/

	$(INSTALL_DIR) $(1)/usr/share/pixmaps
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/pixmaps/* \
		$(1)/usr/share/pixmaps/

	$(INSTALL_DIR) $(1)/usr/share/applications
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/applications/* \
		$(1)/usr/share/applications/
endef

$(eval $(call BuildPackage,mb-applet-input-manager))
