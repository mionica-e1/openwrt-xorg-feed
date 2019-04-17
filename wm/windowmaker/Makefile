#
# Copyright (C) 2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=WindowMaker
PKG_VERSION:=0.95.8
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.windowmaker.org/pub/source/release
PKG_MD5SUM:=29035bf6d07066713d1ace458098727d

PKG_INSTALL:=1
PKG_FIXUP:=libtool

include $(INCLUDE_DIR)/package.mk

CONFIGURE_ARGS += \
	--includedir=${STAGING_DIR}/usr/include/ \
	--enable-xpm \
	--enable-jpeg \
	--enable-gif \
	--enable-png \
	--enable-tiff \
	--disable-documentation \
	--disable-magick \
	--disable-pango \
	--disable-webp \
	--disable-xdnd \
	--disable-randr \
	--disable-shm \
	--disable-shape

define Package/windowmaker
  SECTION:=xorg-wm
  CATEGORY:=Xorg
  SUBMENU:=window manager
  TITLE:=WindowMaker
  DEPENDS:=@DISPLAY_SUPPORT +libX11 +libXext +libXft +libXmu +libXpm \
	+fontconfig +libfreetype +libpng +libjpeg +libtiff +giflib
  URL:=http://www.windowmaker.org
endef

define Package/windowmaker/install
	$(INSTALL_DIR) $(1)/etc/WindowMaker/
	$(CP) $(PKG_INSTALL_DIR)/etc/WindowMaker/* $(1)/etc/WindowMaker/

	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
endef

$(eval $(call BuildPackage,windowmaker))
