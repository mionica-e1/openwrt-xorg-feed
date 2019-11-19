#
# Copyright (C) 2008-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gtk2
PKG_VERSION_MAJOR:=2.24
PKG_VERSION:=2.24.32
PKG_RELEASE:=2

PKG_SOURCE:=gtk+-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@GNOME/gtk+/$(PKG_VERSION_MAJOR)
PKG_BUILD_DIR=$(BUILD_DIR)/gtk+-$(PKG_VERSION)
PKG_HASH:=b6c8a93ddda5eabe3bfee1eb39636c9a03d2a56c7b62828b359bf197943c582e

PKG_FIXUP:=libtool
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

TARGET_LDFLAGS+=\
	-Wl,-rpath-link=$(STAGING_DIR)/usr/lib

STAMP_CONFIGURED:=$(STAMP_CONFIGURED)_$(call confvar,CONFIG_PACKAGE_gtk2 CONFIG_PACKAGE_gtk2-cups)

# We can _either_ compile gtk2 with directfb-support _or_ against libX11 (libX11 is preferred when both libs are selected)

define Package/gtk2
  SECTION:=xorg-framework
  CATEGORY:=Xorg
  SUBMENU:=framework
  TITLE:=GTK+-2.0
  DEPENDS:=@DISPLAY_SUPPORT +cairo +pango +libpng +libjpeg +atk +libtiff +glib2 +gdk-pixbuf \
  +CONFIG_DISPLAY_DIRECTFB_SUPPORT:directfb \
  +DISPLAY_X11_SUPPORT:libX11 \
  +DISPLAY_X11_SUPPORT:libXext \
  +DISPLAY_X11_SUPPORT:libXrender \
  +DISPLAY_X11_SUPPORT:libXfixes \
  +DISPLAY_X11_SUPPORT:libXrandr \
  +DISPLAY_X11_SUPPORT:libXcursor \
  +DISPLAY_X11_SUPPORT:libXdamage \
  +DISPLAY_X11_SUPPORT:libXcomposite \
  +DISPLAY_X11_SUPPORT:libXi
  URL:=http://www.gtk.org/
endef

define Package/gtk2-cups
  SECTION:=xorg-framework
  CATEGORY:=Xorg
  SUBMENU:=framework
  TITLE:=CUPS print backend for GTK+-2.0
  DEPENDS:=gtk2 +cups
endef

define Build/Configure
	$(call Build/Configure/Default, \
		--enable-shm \
		--disable-glibtest \
		--disable-gdiplus \
		--disable-xinerama \
		--without-libjasper \
		--without-xinput \
		$(if $(CONFIG_DISPLAY_DIRECTFB_SUPPORT),--with-gdktarget=directfb,) \
		$(if $(CONFIG_DISPLAY_X11_SUPPORT),--with-x --with-gdktarget=x11,--without-x) \
		$(if $(CONFIG_PACKAGE_gtk2-cups),--enable-cups=auto,--disable-cups), \
		gio_can_sniff=no \
	)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/{lib/pkgconfig,include}
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/gtk-2.0/include/* $(1)/usr/include/

	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.{so*,la} \
		$(1)/usr/lib/

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/
endef

define Package/gtk2/install
	$(INSTALL_DIR) $(1)/etc/gtk-2.0
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/etc/gtk-2.0/* \
		$(1)/etc/gtk-2.0/

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so* \
		$(1)/usr/lib/

	$(foreach d,engines immodules, \
		$(INSTALL_DIR) $(1)/usr/lib/gtk-2.0/2.10.0/$(d); \
		$(INSTALL_DATA) \
			$(PKG_INSTALL_DIR)/usr/lib/gtk-2.0/2.10.0/$(d)/*.so \
			$(1)/usr/lib/gtk-2.0/2.10.0/$(d)/;\
	)
	$(INSTALL_DIR) $(1)/usr/lib/gtk-2.0/2.10.0/printbackends/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/gtk-2.0/2.10.0/printbackends/libprintbackend-{file,lpr}.so \
		$(1)/usr/lib/gtk-2.0/2.10.0/printbackends/

	$(INSTALL_DIR) $(1)/usr/bin/
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/{gtk-builder-convert,gtk-query-immodules-2.0,gtk-update-icon-cache} \
		$(1)/usr/bin/

	$(INSTALL_DIR) $(1)/usr/share/themes/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/share/themes/* \
		$(1)/usr/share/themes/
endef

define Package/gtk2-cups/install
	$(INSTALL_DIR) $(1)/usr/lib/gtk-2.0/2.10.0/printbackends/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/gtk-2.0/2.10.0/printbackends/libprintbackend-cups.so \
		$(1)/usr/lib/gtk-2.0/2.10.0/printbackends/
endef

$(eval $(call BuildPackage,gtk2))
$(eval $(call BuildPackage,gtk2-cups))
