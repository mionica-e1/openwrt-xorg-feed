#
# Copyright (C) 2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=wayland-protocols
PKG_VERSION:=1.17
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://wayland.freedesktop.org/releases/
PKG_MD5SUM:=55ddd5fdb02b73b9de9559aaec267315

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

WAYLAND_PROTOCOLS_STABLE= \
	presentation-time \
	viewporter \
	xdg-shell

WAYLAND_PROTOCOLS_UNSTABLE= \
	fullscreen-shell \
	idle-inhibit \
	input-method \
	input-timestamps \
	keyboard-shortcuts-inhibit \
	linux-dmabuf \
	linux-explicit-synchronization \
	pointer-constraints \
	pointer-gestures \
	primary-selection \
	relative-pointer \
	tablet \
	text-input \
	xdg-decoration \
	xdg-foreign \
	xdg-output \
	xdg-shell \
	xwayland-keyboard-grab


CONFIGURE_ARGS+= \
	--disable-documentation

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/share/pkgconfig/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/pkgconfig/* $(1)/usr/share/pkgconfig/

	$(foreach d,${WAYLAND_PROTOCOLS_STABLE}, \
		$(INSTALL_DIR) $(1)/usr/share/wayland-protocols/stable/$(d)/; \
		$(INSTALL_DATA) \
			$(PKG_INSTALL_DIR)/usr/share/wayland-protocols/stable/$(d)/* \
			$(1)/usr/share/wayland-protocols/stable/$(d)/; \
	)
  
	$(foreach d,${WAYLAND_PROTOCOLS_UNSTABLE}, \
		$(INSTALL_DIR) $(1)/usr/share/wayland-protocols/unstable/$(d)/; \
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

	$(foreach d,${WAYLAND_PROTOCOLS_STABLE}, \
		$(INSTALL_DIR) $(1)/usr/share/wayland-protocols/stable/$(d)/; \
		$(INSTALL_DATA) \
			$(HOST_BUILD_DIR)/stable/$(d)/* \
			$(1)/usr/share/wayland-protocols/stable/$(d)/; \
	)
  
	$(foreach d,${WAYLAND_PROTOCOLS_UNSTABLE}, \
		$(INSTALL_DIR) $(1)/usr/share/wayland-protocols/unstable/$(d)/; \
		$(INSTALL_DATA) \
			$(HOST_BUILD_DIR)/unstable/$(d)/* \
			$(1)/usr/share/wayland-protocols/unstable/$(d)/; \
	)
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,wayland-protocols))