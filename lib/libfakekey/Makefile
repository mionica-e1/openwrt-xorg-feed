#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=libfakekey
PKG_RELEASE:=1
PKG_VERSION:=0.1
PKG_SOURCE_URL:=http://downloads.yoctoproject.org/releases/matchbox/$(PKG_NAME)/$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_MD5SUM:=83dbde4d77e8baf0176fe4291d8a2303

PKG_FIXUP:=libtool

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

PKG_INSTALL:=1

define Package/libfakekey
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=+libX11 +libXtst
  TITLE:=libfakekey
  URL:=http://matchbox-project.org
endef

define Build/Configure
	cd $(PKG_BUILD_DIR); \
		autoreconf & automake --add-missing
	$(call Build/Configure/Default, \
		--enable-expat \
	)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/fakekey
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/include/fakekey/* \
		$(1)/usr/include/fakekey/

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.{so*,a,la} \
		$(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/
endef

define Package/libfakekey/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so.* \
		$(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/
endef

$(eval $(call BuildPackage,libfakekey))
