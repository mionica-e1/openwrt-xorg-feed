#
# Copyright (C) 2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=jwm
PKG_VERSION:=2.4.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://joewing.net/projects/$(PKG_NAME)/releases
PKG_MD5SUM:=54bc8b273562aa492b043e4233e134a7

PKG_INSTALL:=1
PKG_FIXUP:=libtool

include $(INCLUDE_DIR)/package.mk

CONFIGURE_ARGS += \
	--includedir=${STAGING_DIR}/usr/include/ \
	--enable-xpm \
	--enable-jpeg \
	--enable-png \
	--enable-icons \
	--enable-xmu \
	--enable-pango

define Package/jwm
  SECTION:=xorg-wm
  CATEGORY:=Xorg
  SUBMENU:=window manager
  TITLE:=JWM
  DEPENDS:=@DISPLAY_SUPPORT +libX11 +libXext +libXft +libXmu +libXpm \
	+fontconfig +libfreetype +libpng +libjpeg +pango
  URL:=http://joewing.net/projects/jwm/
endef

define Package/jwm/install
	$(INSTALL_DIR) $(1)/etc/
	$(CP) $(PKG_INSTALL_DIR)/etc/* $(1)/etc/

	$(INSTALL_DIR) $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/usr/share/
	$(CP) $(PKG_INSTALL_DIR)/usr/share/* $(1)/usr/share/

endef

$(eval $(call BuildPackage,jwm))
