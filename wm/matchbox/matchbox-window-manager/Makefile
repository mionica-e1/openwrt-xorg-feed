#
# Copyright (C) 2007-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=matchbox-window-manager
PKG_RELEASE:=1
PKG_VERSION:=1.2.2
PKG_SOURCE_URL:=https://github.com/suwus/matchbox-window-manager.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2019-11-19
PKG_SOURCE_VERSION:=91511f26a0584230a474d39490805618cbf672da

PKG_FIXUP:=libtool

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

TARGET_LDFLAGS+= \
	-Wl,-rpath-link=$(STAGING_DIR)/usr/lib \

define Package/matchbox-window-manager
  TITLE:=matchbox window manager
  SECTION:=xorg-matchbox
  CATEGORY:=Xorg
  SUBMENU:=Matchbox Window manager
  DEPENDS:=@!avr32 @DISPLAY_SUPPORT +libX11 +zlib +libfreetype +fontconfig +libmatchbox \
	+startup-notification +libSM +libXfixes +libXcursor +libpng
  URL:=http://matchbox-project.org/
endef

define Build/Configure
	cd $(PKG_BUILD_DIR); \
		aclocal & autoheader & automake --force-missing --add-missing & autoconf
		
	$(call Build/Configure/Default, \
		--enable-expat \
		--disable-gconf \
		--disable-composite \
		--disable-standalone \
		--disable-standalone-xft \
		--enable-startup-notification \
		--enable-session \
	)
endef


define Package/matchbox-window-manager/install
	$(INSTALL_DIR) $(1)/etc/matchbox
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/etc/matchbox/kbdconfig \
		$(1)/etc/matchbox/

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/* \
		$(1)/usr/bin/

	$(INSTALL_DIR) $(1)/usr/share/{matchbox,themes}
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/matchbox/* \
		$(1)/usr/share/matchbox/
	$(CP) -r \
		$(PKG_INSTALL_DIR)/usr/share/themes/* \
		$(1)/usr/share/themes/

	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_DATA) \
		./files/uci-defaults/x11 \
		$(1)/etc/uci-defaults/
endef

define Package/matchbox-window-manager/postinst
	#!/bin/sh
	[ -n "$${IPKG_INSTROOT}" ] && exit
	. /etc/functions.sh
	uci_apply_defaults
endef

$(eval $(call BuildPackage,matchbox-window-manager))
