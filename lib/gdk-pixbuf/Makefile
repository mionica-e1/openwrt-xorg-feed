#
# Copyright (C) 2006-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=gdk-pixbuf
PKG_VERSION_MAJOR:=2.36
PKG_VERSION:=2.36.4
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@GNOME/$(PKG_NAME)/$(PKG_VERSION_MAJOR)/
PKG_HASH:=0b19901c3eb0596141d2d48ddb9dac79ad1524bdf59366af58ab38fcb9ee7463

PKG_FIXUP:=libtool

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/gdk-pixbuf
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  TITLE:=Gdk-Pixbuf
  DEPENDS:=+libpng +libjpeg +atk +libtiff +glib2
endef

define Build/Configure
	$(call Build/Configure/Default, \
		--disable-glibtest \
		$(if $(CONFIG_CONFIG_DISPLAY_X11_SUPPORT),--with-x11,--without-x11) \
		gio_can_sniff=no \
	)
	cd $(PKG_BUILD_DIR); \
		$(SED) 's/ tests//' Makefile.in
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/{lib,include}
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib* $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/ $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
endef

define Package/gdk-pixbuf/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib*so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,gdk-pixbuf))
