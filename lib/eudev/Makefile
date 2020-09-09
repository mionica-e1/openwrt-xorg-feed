# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=eudev

PKG_RELEASE:=1
PKG_VERSION:=3.2.2
PKG_SOURCE_VERSION:=6b5db4f21e84fd4c6206927b41f1074d20c4ec45

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.xz
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/gentoo/eudev.git

PKG_LICENSE:=GPLv2
PKG_LICENSE_FILES:=COPYING
PKG_MAINTAINER:=Han Pengfei <pengphei@foxmail.com>
PKG_FIXUP:=libtool
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libeudev
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=eudev for Gentoo/OpenRC (and other non-systemd)
  URL:=https://github.com/gentoo/eudev
  DEPENDS:=libevdev +libblkid +libkmod
  PROVIDES:=libudev-fbsd libudev
  CONFLICTS:=libudev libudev-fbsd
endef

define Package/eudev
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=eudev daemon utils
  URL:=https://github.com/gentoo/eudev
  DEPENDS:=libeudev +libblkid +libkmod
  CONFLICTS:=udev
endef

define Package/eudev-rules
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=eudev rules
  URL:=https://github.com/gentoo/eudev
  DEPENDS:=libeudev
endef

define Package/eudev-hwdb
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=eudev hwdb
  URL:=https://github.com/gentoo/eudev
  DEPENDS:=libeudev
endef

STAMP_CONFIGURED:=$(STAMP_CONFIGURED)_$(call confvar,CONFIG_PACKAGE_eudev \
    CONFIG_PACKAGE_eudev-rules \
	CONFIG_PACKAGE_eudev-hwdb)

define Build/Configure
	$(call Build/Configure/Default, \
		--disable-debug \
		--disable-selinux \
		--with-rootrundir=/var/run \
		$(if $(CONFIG_PACKAGE_eudev-rulesl),--enable-rule-generator,--disable-rule-generator) \
		$(if $(CONFIG_PACKAGE_eudev-hwdb),--enable-hwdb,--disable-hwdb) \
	)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* $(1)/usr/lib/pkgconfig/
endef

define Package/libeudev/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
endef

define Package/eudev/install
	$(INSTALL_DIR) $(1)/etc/udev
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/etc/udev/udev.conf $(1)/etc/udev/

	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/usr/sbin
	$(CP) $(PKG_INSTALL_DIR)/usr/sbin/* $(1)/usr/sbin/

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./files/eudevd.config $(1)/etc/config/eudevd
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/eudevd.init $(1)/etc/init.d/eudevd
endef

define Package/eudev-rules/install
	$(INSTALL_DIR) $(1)/usr/lib/udev/rules.d
	$(INSTALL_DIR) $(1)/etc/udev/rules.d
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/udev/rules.d/* \
		$(1)/usr/lib/udev/rules.d/
endef

define Package/eudev-hwdb/install
	$(INSTALL_DIR) $(1)/etc/udev/hwdb.d
	$(CP) \
		$(PKG_INSTALL_DIR)/etc/udev/hwdb.d/* \
		$(1)/etc/udev/hwdb.d/
endef

$(eval $(call BuildPackage,libeudev))
$(eval $(call BuildPackage,eudev))
$(eval $(call BuildPackage,eudev-rules))
$(eval $(call BuildPackage,eudev-hwdb))
