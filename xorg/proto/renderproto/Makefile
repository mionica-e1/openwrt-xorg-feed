#
# Copyright (C) 2006-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=renderproto
PKG_VERSION:=0.11.1
PKG_RELEASE:=2

PKG_SOURCE_URL:=http://xorg.freedesktop.org/releases/individual/proto/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_BUILD_DIR:=$(BUILD_DIR)/Xorg/$(PKG_NAME)-$(PKG_VERSION)/
PKG_HASH:=06735a5b92b20759204e4751ecd6064a2ad8a6246bb65b3078b862a00def2537

include $(INCLUDE_DIR)/package.mk

define Package/renderproto
  SECTION:=xorg-proto
  CATEGORY:=Xorg
  SUBMENU:=proto
  DEPENDS:=
  TITLE:=renderproto
  URL:=http://xorg.freedesktop.org/
endef

define Build/InstallDev
	DESTDIR="$(1)" $(MAKE) -C $(PKG_BUILD_DIR)/ $(MAKE_FLAGS) install
endef

define Build/Compile
	true
endef

$(eval $(call BuildPackage,renderproto))
