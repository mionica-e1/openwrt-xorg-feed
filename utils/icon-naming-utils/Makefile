#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=icon-naming-utils
PKG_RELEASE:=1
PKG_VERSION:=0.8.90
PKG_SOURCE_URL:= http://tango.freedesktop.org/releases
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_MD5SUM:=ccf92e77b98ce579022ec1259336ccce
PKG_FIXUP:=libtool

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/host-build.mk

PKG_INSTALL:=1

define Package/icon-naming-utils
  SECTION:=xorg-utils
  CATEGORY:=Xorg
  SUBMENU:=utils
  TITLE:=icon-naming-utils
  URL:=http://tango.freedesktop.org
endef

define Package/icon-naming-utils/description
 a Perl script used for maintaining backwards 
 compatibility with current desktop icon themes
endef

define Package/icon-naming-utils/install
  $(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/icon-name-mapping \
		$(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/share/pkgconfig/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/pkgconfig/* $(1)/usr/share/pkgconfig/

	$(INSTALL_DIR) $(1)/usr/share/dtds/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/dtds/* $(1)/usr/share/dtds/

	$(INSTALL_DIR) $(1)/usr/share/icon-naming-utils/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/icon-naming-utils/* $(1)/usr/share/icon-naming-utils/
endef

define Host/Install
  $(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DATA) \
		$(HOST_BUILD_DIR)/icon-name-mapping \
		$(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/share/pkgconfig/
	$(INSTALL_DATA) $(HOST_BUILD_DIR)/icon-naming-utils.pc $(1)/usr/share/pkgconfig/

	$(INSTALL_DIR) $(1)/usr/share/dtds/
	$(INSTALL_DATA) $(HOST_BUILD_DIR)/legacy-icon-mapping.dtd $(1)/usr/share/dtds/

	$(INSTALL_DIR) $(1)/usr/share/icon-naming-utils/
	$(INSTALL_DATA) $(HOST_BUILD_DIR)/legacy-icon-mapping.xml $(1)/usr/share/icon-naming-utils/
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,icon-naming-utils))
