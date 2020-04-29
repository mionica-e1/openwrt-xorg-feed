#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xf86-input-libinput
PKG_RELEASE:=1
PKG_VERSION:=0.24.0

PKG_SOURCE_URL:=http://xorg.freedesktop.org/releases/individual/driver
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_BUILD_DIR:=$(BUILD_DIR)/Xorg/$(PKG_NAME)-$(PKG_VERSION)/
PKG_MD5SUM:=bd3fa118e4abadb8804dc6a099bb4ab3

PKG_FIXUP:=libtool
PKG_INSTALL:=1

PKG_BUILD_DEPENDS:=randrproto inputproto xproto

include $(INCLUDE_DIR)/package.mk
$(call include_mk, xorg-driver.mk)

define Package/xf86-input-libinput
  SECTION:=xorg-driver
  CATEGORY:=Xorg
  SUBMENU:=driver
  DEPENDS:=+xserver-xorg +libinput
  TITLE:=xf86-input-libinput
  URL:=http://xorg.freedesktop.org/
endef

define Package/xf86-input-libinput/install
	$(INSTALL_DIR) $(1)/usr/lib/xorg/modules/input
	$(INSTALL_DIR) $(1)/usr/share/X11/xorg.conf.d
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/xorg/modules/input/libinput_drv.so \
		$(1)/usr/lib/xorg/modules/input/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/X11/xorg.conf.d/*.conf \
		$(1)/usr/share/X11/xorg.conf.d/
endef

$(eval $(call BuildPackage,xf86-input-libinput))
