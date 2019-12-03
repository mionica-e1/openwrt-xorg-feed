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

define Package/libdrm-amdgpu
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libdrm @DISPLAY_SUPPORT @TARGET_x86
  TITLE:=drm amdgpu api
  URL:=https://dri.freedesktop.org
endef

define Package/libdrm-radeon
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libdrm @DISPLAY_SUPPORT @TARGET_x86
  TITLE:=drm radeon api
  URL:=https://dri.freedesktop.org
endef

define Package/libdrm-nouveau
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libdrm @DISPLAY_SUPPORT
  TITLE:=drm nouveau api
  URL:=https://dri.freedesktop.org
endef

define Package/libdrm-intel
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libdrm @DISPLAY_SUPPORT @TARGET_x86
  TITLE:=drm intel api
  URL:=https://dri.freedesktop.org
endef

define Package/libdrm-vmwgfx
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libdrm @DISPLAY_SUPPORT @TARGET_x86
  TITLE:=drm vmwgfx api
  URL:=https://dri.freedesktop.org
endef

define Package/libdrm-freedreno
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libdrm @DISPLAY_SUPPORT @(arm||aarch64)
  TITLE:=drm freedreno api
  URL:=https://dri.freedesktop.org
endef

define Package/libdrm-vc4
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libdrm @DISPLAY_SUPPORT @(arm||aarch64)
  TITLE:=drm vc4 api
  URL:=https://dri.freedesktop.org
endef

define Package/libdrm-omap_experimental_api
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libdrm @DISPLAY_SUPPORT @(arm||aarch64)
  TITLE:=drm omap experimental api
  URL:=https://dri.freedesktop.org
endef

define Package/libdrm-exynos_experimental_api
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libdrm @DISPLAY_SUPPORT @(arm||aarch64)
  TITLE:=drm exynos experimental api
  URL:=https://dri.freedesktop.org
endef

define Package/libdrm-tegra_experimental_api
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libdrm @DISPLAY_SUPPORT @(arm||aarch64)
  TITLE:=drm tegra experimental api
  URL:=https://dri.freedesktop.org
endef

define Package/libdrm-etnaviv_experimental_api
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libdrm @DISPLAY_SUPPORT @(arm||aarch64)
  TITLE:=drm etnaviv experimental api
  URL:=https://dri.freedesktop.org
endef

DRM_APIS:=amdgpu nouveau radeon intel vmwgfx freedreno vc4 \
		tegra_experimental_api etnaviv_experimental_api \
		omap_experimental_api exynos_experimental_api

CONFIGURE_ARGS += --enable-malloc0returnsnull --without-xcb


STAMP_CONFIGURED:=$(STAMP_CONFIGURED)_$(call confvar,CONFIG_PACKAGE_libdrm \
    $(foreach dri,$(DRM_APIS),CONFIG_PACKAGE_libdrm-$(dri)) \
	)

define Build/Configure
	$(call Build/Configure/Default, \
		--disable-freedeno-kgsl \
		$(foreach dri,$(DRM_APIS),$(if $(CONFIG_PACKAGE_libdrm-$(dri)),--enable-$(dri),--disable-$(dri))) \
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
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libdrm.so* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libkms.so* $(1)/usr/lib/
endef

define Build/InstallDev
	$(CP) $(PKG_INSTALL_DIR)/* $(1)/
endef

define Package/libdrm-amdgpu/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libdrm_amdgpu.so* \
		$(1)/usr/lib/
endef

define Package/libdrm-nouveau/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libdrm_nouveau.so* \
		$(1)/usr/lib/
endef

define Package/libdrm-radeon/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libdrm_radeon.so* \
		$(1)/usr/lib/
endef

define Package/libdrm-intel/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libdrm_intel.so* \
		$(1)/usr/lib/
endef

define Package/libdrm-vmwgfx/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libdrm_vmwgfx.so* \
		$(1)/usr/lib/
endef

define Package/libdrm-freedreno/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libdrm_freedreno.so* \
		$(1)/usr/lib/
endef

define Package/libdrm-vc4/install
endef

define Package/libdrm-omap_experimental_api/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libdrm_omap.so* \
		$(1)/usr/lib/
endef

define Package/libdrm-exynos_experimental_api/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libdrm_exynos.so* \
		$(1)/usr/lib/
endef

define Package/libdrm-tegra_experimental_api/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libdrm_tegra.so* \
		$(1)/usr/lib/
endef

define Package/libdrm-etnaviv_experimental_api/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libdrm_etnaviv.so* \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,libdrm))
$(foreach dri,$(DRM_APIS),$(eval $(call BuildPackage,libdrm-$(dri))))