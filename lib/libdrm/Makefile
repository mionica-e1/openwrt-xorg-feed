#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=libdrm
PKG_VERSION:=2.4.97
PKG_RELEASE:=5

PKG_SOURCE_URL:=http://dri.freedesktop.org/libdrm
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_BUILD_DIR=$(BUILD_DIR)/Xorg/$(_CATEGORY)/$(PKG_NAME)-$(PKG_VERSION)/
PKG_HASH:=77d0ccda3e10d6593398edb70b1566bfe1a23a39bd3da98ace2147692eadd123

PKG_FIXUP:=libtool

include $(INCLUDE_DIR)/package.mk

define Package/libdrm
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=+xorg-macros +libatomic
  TITLE:=libdrm
  URL:=http://dri.freedesktop.org/
endef

define Package/libdrm-api/Default
define Package/libdrm-$(1)
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libdrm @DISPLAY_SUPPORT $(2)
  TITLE:=drm $(1) api
  URL:=https://dri.freedesktop.org
endef
endef

DRM_X86:=amdgpu nouveau radeon intel vmwgfx
DRM_ARM:=freedreno freedreno-kgsl vc4
DRM_ARM_EX:=omap exynos tegra etnaviv

CONFIGURE_ARGS += --enable-malloc0returnsnull --without-xcb

$(foreach dri,$(DRM_X86),$(eval $(call Package/libdrm-api/Default,$(dri),@TARGET_x86)))
$(foreach dri,$(DRM_ARM),$(eval $(call Package/libdrm-api/Default,$(dri),@arm)))
$(foreach dri,$(DRM_ARM_EX),$(eval $(call Package/libdrm-api/Default,$(dri),@arm)))

STAMP_CONFIGURED:=$(STAMP_CONFIGURED)_$(call confvar,CONFIG_PACKAGE_libdrm \
    $(foreach dri,$(DRM_X86),CONFIG_PACKAGE_libdrm-$(dri)) \
	$(foreach dri,$(DRM_ARM),CONFIG_PACKAGE_libdrm-$(dri)) \
	$(foreach dri,$(DRM_ARM_EX),CONFIG_PACKAGE_libdrm-$(dri)) \
	)

define Build/Configure
	$(call Build/Configure/Default, \
		$(foreach dri,$(DRM_X86),$(if $(CONFIG_PACKAGE_libdrm-$(dri)),--enable-$(dri),--disable-$(dri))) \
		$(foreach dri,$(DRM_ARM),$(if $(CONFIG_PACKAGE_libdrm-$(dri)),--enable-$(dri),--disable-$(dri))) \
		$(foreach dri,$(DRM_ARM_EX),$(if $(CONFIG_PACKAGE_libdrm-$(dri)),--enable-$(dri)-experimental-api)) \
		)
endef

define Build/Compile
	$(call $(PKG_NAME)/Compile)
	make -C $(PKG_BUILD_DIR)
	DESTDIR=$(PKG_INSTALL_DIR) $(MAKE) -C $(PKG_BUILD_DIR) $(MAKE_FLAGS) install
	find $(PKG_INSTALL_DIR) -name *.la | xargs rm -rf
endef

define Package/libdrm/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libdrm* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libkms* $(1)/usr/lib/
endef

define Build/InstallDev
	$(CP) $(PKG_INSTALL_DIR)/* $(1)/
endef

define Package/libdrm-api/install/Default
define Package/libdrm-$(1)/install
	$(INSTALL_DIR) $$(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libdrm_$(1).so* \
		$$(1)/usr/lib/
endef
endef

$(foreach dri,$(DRM_X86),$(eval $(call Package/libdrm_api/install/Default,$(dri))))
$(foreach dri,$(DRM_ARM),$(eval $(call Package/libdrm_api/install/Default,$(dri))))
$(foreach dri,$(DRM_ARM_EX),$(eval $(call Package/libdrm_api/install/Default,$(dri))))

$(eval $(call BuildPackage,libdrm))
$(foreach dri,$(DRM_X86),$(eval $(call BuildPackage,libdrm-$(dri))))
$(foreach dri,$(DRM_ARM),$(eval $(call BuildPackage,libdrm-$(dri))))
$(foreach dri,$(DRM_ARM_EX),$(eval $(call BuildPackage,libdrm-$(dri))))