#
# Copyright (C) 2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=wayland-protocols
PKG_VERSION:=1.16
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://wayland.freedesktop.org/releases/
PKG_MD5SUM:=e0b523ff162e30bab46be1d65d527683

PKG_INSTALL:=1
PKG_FIXUP:=libtool

PKG_BUILD_DEPENDS:=wayland/host
HOST_BUILD_DEPENDS:=wayland/host

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/host-build.mk

define Package/wayland-protocols
  SECTION:=wayland-protocols
  CATEGORY:=Wayland
  TITLE:=wayland protocols
  DEPENDS:=@!avr32 @DISPLAY_SUPPORT
  URL:=https://wayland.freedesktop.org/
endef

CONFIGURE_ARGS+= \
	--disable-documentation

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/share/pkgconfig/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/pkgconfig/* $(1)/usr/share/pkgconfig/

	$(INSTALL_DIR) $(1)/usr/share/wayland-protocols/stable/{presentation-time,viewporter,xdg-shell}
	$(foreach d,presentation-time viewporter xdg-shell, \
		$(INSTALL_DATA) \
			$(PKG_INSTALL_DIR)/usr/share/wayland-protocols/stable/$(d)/* \
			$(1)/usr/share/wayland-protocols/stable/$(d)/; \
	)
  
	$(INSTALL_DIR) $(1)/usr/share/wayland-protocols/unstable/{fullscreen-shell,input-method,xdg-shell,tablet}
	$(foreach d,fullscreen-shell input-method xdg-shell tablet, \
		$(INSTALL_DATA) \
			$(PKG_INSTALL_DIR)/usr/share/wayland-protocols/unstable/$(d)/* \
			$(1)/usr/share/wayland-protocols/unstable/$(d)/; \
	)
endef

HOST_CONFIGURE_ARGS+= \
	--disable-documentation

define Host/Install
	$(INSTALL_DIR) $(1)/usr/share/pkgconfig/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/pkgconfig/* $(1)/usr/share/pkgconfig/

	$(INSTALL_DIR) $(1)/usr/share/wayland-protocols/stable/{presentation-time,viewporter,xdg-shell}
	$(foreach d,presentation-time viewporter xdg-shell, \
		$(INSTALL_DATA) \
			$(PKG_INSTALL_DIR)/usr/share/wayland-protocols/stable/$(d)/* \
			$(1)/usr/share/wayland-protocols/stable/$(d)/; \
	)
  
	$(INSTALL_DIR) $(1)/usr/share/wayland-protocols/unstable/{fullscreen-shell,input-method,xdg-shell,tablet}
	$(foreach d,fullscreen-shell input-method xdg-shell tablet, \
		$(INSTALL_DATA) \
			$(PKG_INSTALL_DIR)/usr/share/wayland-protocols/unstable/$(d)/* \
			$(1)/usr/share/wayland-protocols/unstable/$(d)/; \
	)
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,wayland-protocols))