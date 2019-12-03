#
# Copyright (C) 2007-2017 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=Mako
PKG_VERSION:=1.1.0
PKG_RELEASE:=1
PKG_LICENSE:=MIT

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://files.pythonhosted.org/packages/b0/3c/8dcd6883d009f7cae0f3157fb53e9afb05a0d3d33b3db1268ec2e6f4a56b/
PKG_HASH:=a36919599a9b7dc5d86a7a8988f23a9a3a3d083070023bab23d64f7f1d1e0a4b

HOST_BUILD_DEPENDS:=python/host

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python-package.mk
include $(INCLUDE_DIR)/host-build.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-host.mk
include $(TOPDIR)/feeds/packages/lang/python/python-host.mk

define Package/Mako
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  MAINTAINER:=Han Pengfei <pengphei@qq.com>
  TITLE:=Mako Templates for Python
  URL:=http://simplejson.readthedocs.org/
  DEPENDS:=+python
  VARIANT:=python
endef

define Package/Mako/description
  Mako Templates for Python
  .
  (Variant for Python)
endef

define Host/Configure
endef

define Host/Compile
  $(call Build/Compile/HostPy3Mod,,install --prefix="" --root="$(STAGING_DIR_HOSTPKG)")
endef

define Host/Install
endef

define Build/Compile
	$(call Build/Compile/Py3Mod,,install --prefix=/usr --root=$(PKG_INSTALL_DIR))
endef

$(eval $(call HostBuild))
$(eval $(call PyPackage,Mako))
$(eval $(call BuildPackage,Mako))
$(eval $(call BuildPackage,Mako-src))