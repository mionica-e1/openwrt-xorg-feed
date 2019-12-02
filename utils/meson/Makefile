include $(TOPDIR)/rules.mk

PKG_NAME:=meson
PKG_VERSION:=0.52.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/mesonbuild/meson/releases/download/$(PKG_VERSION)/
PKG_HASH:=d60f75f0dedcc4fd249dbc7519d6f3ce6df490033d276ef1cf27453ef4938d32

PKG_MAINTAINER:=Andre Heider <a.heider@gmail.com>
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=COPYING

HOST_BUILD_DEPENDS:=ninja/host python3-light/host

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-host.mk

define Host/Configure
endef

define Host/Compile
  $(call Build/Compile/HostPy3Mod,,install --prefix="" --root="$(STAGING_DIR_HOSTPKG)")
endef

define Host/Install
endef

define Host/Clean
	$(call Host/Clean/Default)
	rm -f $(STAGING_DIR_HOSTPKG)/bin/meson
endef

define Package/meson
  SECTION:=devel
  CATEGORY:=Development
  TITLE:=meson
  URL:=https://mesonbuild.com/
  DEPENDS:=+ninja +python3-pkg-resources
  VARIANT:=python3
endef

define Package/meson/description
  Meson is an open source build system meant to be both extremely fast, and, even more importantly, as user friendly as possible.
endef


define Build/Compile
	$(call Build/Compile/Py3Mod,,install --prefix=/usr --root=$(PKG_INSTALL_DIR))
endef

define Package/meson/install
endef

$(eval $(call HostBuild))
$(eval $(call Py3Package,meson))
$(eval $(call BuildPackage,meson))
$(eval $(call BuildPackage,meson-src))