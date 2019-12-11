#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=matchbox-common
PKG_RELEASE:=1
PKG_VERSION:=0.9
PKG_MIN_VERSION:=1
PKG_SOURCE_URL:=http://downloads.yoctoproject.org/releases/matchbox/$(PKG_NAME)/$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).$(PKG_MIN_VERSION).tar.bz2
PKG_MD5SUM:=8e8ba0ee170a9ac78fdc583b00ccf76b
PKG_FIXUP:=libtool

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION).$(PKG_MIN_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

PKG_INSTALL:=1

define Package/matchbox-common
  SECTION:=xorg-matchbox
  CATEGORY:=Xorg
  SUBMENU:=Matchbox Window manager
  DEPENDS:=+libmatchbox
  TITLE:=matchbox-common
  URL:=http://matchbox-project.org
endef

CONFIGURE_ARGS+= \
	--disable-pda-folders

define Build/InstallDev
endef

define Package/matchbox-common/install
	$(INSTALL_DIR) $(1)/usr/{bin,share}
	$(INSTALL_DIR) $(1)/usr/share/{icons,matchbox,pixmaps}
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/matchbox-session \
		$(1)/usr/bin/
	$(CP) -r \
		$(PKG_INSTALL_DIR)/usr/share/icons/* \
		$(1)/usr/share/icons
	$(CP) -r \
		$(PKG_INSTALL_DIR)/usr/share/matchbox/* \
		$(1)/usr/share/matchbox
	$(CP) -r \
		$(PKG_INSTALL_DIR)/usr/share/pixmaps/* \
		$(1)/usr/share/pixmaps
endef

$(eval $(call BuildPackage,matchbox-common))
