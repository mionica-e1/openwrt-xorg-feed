#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=matchbox-desktop
PKG_RELEASE:=1
PKG_VERSION:=0.9
PKG_MIN_VERSION:=1
PKG_SOURCE_URL:=http://downloads.yoctoproject.org/releases/matchbox/$(PKG_NAME)/$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).$(PKG_MIN_VERSION).tar.bz2
PKG_MD5SUM:=3335a30b1a1aacfb39f23b505254765c
PKG_FIXUP:=libtool

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION).$(PKG_MIN_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

PKG_INSTALL:=1

define Package/matchbox-desktop
  SECTION:=xorg-matchbox
  CATEGORY:=Xorg
  SUBMENU:=Matchbox Window manager
  DEPENDS:=+libmatchbox +zlib
  TITLE:=matchbox-desktop
  URL:=http://matchbox-project.org
endef

CONFIGURE_ARGS+= \
	--enable-expat \
	--disable-startup-notification

define Package/matchbox-desktop/install
	$(INSTALL_DIR) $(1)/etc/matchbox
	$(CP) -r \
		$(PKG_INSTALL_DIR)/etc/matchbox/* \
		$(1)/etc/matchbox/

	$(INSTALL_DIR) $(1)/usr/{bin,lib,share}
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/matchbox-desktop \
		$(1)/usr/bin/

	$(INSTALL_DIR) $(1)/usr/lib/matchbox/desktop
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/matchbox/desktop/*.so \
		$(1)/usr/lib/matchbox/desktop/

	$(INSTALL_DIR) $(1)/usr/share/{applications,pixmaps}
	$(CP) -r \
		$(PKG_INSTALL_DIR)/usr/share/applications/* \
		$(1)/usr/share/applications/
	$(CP) -r \
		$(PKG_INSTALL_DIR)/usr/share/pixmaps/* \
		$(1)/usr/share/pixmaps/
endef

$(eval $(call BuildPackage,matchbox-desktop))
