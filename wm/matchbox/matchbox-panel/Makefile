#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=matchbox-panel
PKG_RELEASE:=1
PKG_VERSION:=0.9
PKG_MIN_VERSION:=3
PKG_SOURCE_URL:=http://downloads.yoctoproject.org/releases/matchbox/$(PKG_NAME)/$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).$(PKG_MIN_VERSION).tar.bz2
PKG_MD5SUM:=56d1807636f3919e22e51896ab7ccd2e
PKG_FIXUP:=libtool

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION).$(PKG_MIN_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

PKG_INSTALL:=1

define Package/matchbox-panel
  SECTION:=xorg-matchbox
  CATEGORY:=Xorg
  SUBMENU:=Matchbox Window manager
  DEPENDS:=+libmatchbox
  TITLE:=matchbox-panel
  URL:=http://matchbox-project.org
endef

CONFIGURE_ARGS+= \
	--enable-expat \
	--disable-startup-notification \
	--enable-dnotify \
	--disable-acpi-linux

define Package/matchbox-panel/install
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

$(eval $(call BuildPackage,matchbox-panel))
