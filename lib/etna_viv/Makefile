#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=etna_viv
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://github.com/etnaviv/etna_viv.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2019-12-04
PKG_SOURCE_VERSION:=057599584d95d747ef42ca2f97b10082a66e9e06
PKG_BUILD_DIR=$(BUILD_DIR)/Xorg/$(PKG_NAME)-$(PKG_VERSION)/

PKG_FIXUP:=libtool

include $(INCLUDE_DIR)/package.mk

define Package/etna_viv
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=@DISPLAY_SUPPORT
  TITLE:=etna_viv
  URL:=https://github.com/etnaviv/etna_viv.git
endef


define Build/Compile
endef

define Package/etna_viv/install
	true
endef

define Build/InstallDev
endef

$(eval $(call BuildPackage,etna_viv))
