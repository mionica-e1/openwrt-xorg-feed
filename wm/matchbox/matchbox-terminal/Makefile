#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk
PKG_NAME:=matchbox-terminal
PKG_RELEASE:=1
PKG_VERSION:=0.2
PKG_SOURCE_URL:=http://git.yoctoproject.org/cgit/cgit.cgi/$(PKG_NAME)/snapshot/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_MD5SUM:=1e4ff6b7660f46eaf6d13649fcf88b61
PKG_FIXUP:=libtool

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

PKG_INSTALL:=1

define Package/matchbox-terminal
  SECTION:=xorg-matchbox
  CATEGORY:=Xorg
  SUBMENU:=Matchbox Window manager
  DEPENDS:=+libmatchbox
  TITLE:=matchbox-terminal
  URL:=http://matchbox-project.org
endef

define Package/matchbox-terminal/description
 Matchbox Terminal
endef

CONFIGURE_ARGS+= \
	--enable-expat \
	--disable-startup-notification \
	--enable-dnotify \
	--disable-acpi-linux

define Package/matchbox-terminal/install
	$(INSTALL_DIR) $(1)/usr/{bin,share}
	$(INSTALL_BIN) \
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

$(eval $(call BuildPackage,matchbox-terminal))
