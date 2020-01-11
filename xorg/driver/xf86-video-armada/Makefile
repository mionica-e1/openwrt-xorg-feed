#
# Copyright (C) 2007-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xf86-video-armada
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

PKG_SOURCE_URL:=http://git.arm.linux.org.uk/cgit/xf86-video-armada.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2019-12-04
PKG_SOURCE_VERSION:=34a7272573431a9a0fabb94012f902198a3ac9a7

PKG_BUILD_DIR:=$(BUILD_DIR)/Xorg/$(PKG_NAME)-$(PKG_VERSION)/

PKG_FIXUP:=libtool
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
$(call include_mk, xorg-driver.mk)

define Package/xf86-video-armada
  SECTION:=xorg-driver
  CATEGORY:=Xorg
  SUBMENU:=driver
  DEPENDS:=@DISPLAY_SUPPORT +xserver-xorg +libdrm +libdrm-armada +etna_viv
  TITLE:=xf86-video-armada
  URL:=http://git.arm.linux.org.uk/cgit/xf86-video-armada.git/
endef

ETNA_SRC:=$(BUILD_DIR)/Xorg/etna_viv-$(PKG_VERSION)

define Build/Configure
	$(call Build/Configure/Default, \
		--enable-maintainer-mode \
		--disable-vivante \
		--enable-etnaviv \
		--with-etnaviv-source=$(ETNA_SRC) \
		--host=$(GNU_TARGET_NAME) \
	)
endef

define Package/xf86-video-armada/install
	$(INSTALL_DIR) $(1)/usr/lib/xorg/modules/drivers
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/xorg/modules/drivers/*.so \
		$(1)/usr/lib/xorg/modules/drivers/
endef

$(eval $(call BuildPackage,xf86-video-armada))
