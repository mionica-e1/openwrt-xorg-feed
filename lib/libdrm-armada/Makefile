#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=libdrm-armada
PKG_VERSION:=2.0.0
PKG_RELEASE:=1

PKG_SOURCE_URL:=http://git.arm.linux.org.uk/cgit/libdrm-armada.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2019-12-04
PKG_SOURCE_VERSION:=607c697d7c403356601cd0d5fa6407b61a45e8ed
PKG_BUILD_DIR=$(BUILD_DIR)/Xorg/$(_CATEGORY)/$(PKG_NAME)-$(PKG_VERSION)/

PKG_FIXUP:=libtool

include $(INCLUDE_DIR)/package.mk

define Package/libdrm-armada
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=+libdrm +librt @DISPLAY_SUPPORT
  TITLE:=libdrm-armada
  URL:=http://git.arm.linux.org.uk/cgit/libdrm-armada.git
endef

define Build/Compile
	$(call $(PKG_NAME)/Compile)
	make -C $(PKG_BUILD_DIR)
	DESTDIR=$(PKG_INSTALL_DIR) $(MAKE) -C $(PKG_BUILD_DIR) $(MAKE_FLAGS) install
	find $(PKG_INSTALL_DIR) -name *.la | xargs rm -rf
endef

define Package/libdrm-armada/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libdrm_armada.so* $(1)/usr/lib/
endef

define Build/InstallDev
	$(CP) $(PKG_INSTALL_DIR)/* $(1)/
endef

$(eval $(call BuildPackage,libdrm-armada))
