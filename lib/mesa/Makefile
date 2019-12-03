#
# Copyright (C) 2008-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mesa
PKG_RELEASE:=3
PKG_VERSION:=18.3.6

PKG_SOURCE_URL:=https://mesa.freedesktop.org/archive/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_HASH:=aaf17638dcf5a90b93b6389e152fdc9ef147768b09598f24d2c5cf482fcfc705
PKG_FIXUP:=libtool
PKG_BUILD_DEPENDS:=glproto xrandr

include $(INCLUDE_DIR)/package.mk

PKG_INSTALL:=1

define Package/libgl-mesa
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=+libX11 +libXext +libXfixes +libXdamage +libXxf86vm +libdrm +libexpat \
	+libxcb +libxshmfence +zlib +libxcb-dri2 +libxcb-dri3 +libxcb-glx +libxcb-present \
	+libxcb-sync +libxcb-sync +libxcb-xfixes
  TITLE:=Mesa OpenGL library
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-egl
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT
  TITLE:=Mesa EGL library
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-gles-v1
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT
  TITLE:=Mesa GLESv1 CM library
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-gles-v2
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT
  TITLE:=Mesa GLESv2 library
  URL:=https://mesa.freedesktop.org
endef

define Package/libosmesa
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT
  TITLE:=OS Mesa library
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-dri/Default
define Package/libgl-mesa-dri-$(1)
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT $(if $(findstring swrast,$(1)),,@TARGET_x86)
  TITLE:=mesa dri $(1)
  URL:=https://mesa.freedesktop.org
endef
endef

define Package/libgl-mesa-gallium/Default
define Package/libgl-mesa-gallium-$(1)
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT $(2)
  TITLE:=mesa gallium $(1) driver
  URL:=https://mesa.freedesktop.org
endef
endef

define Package/libgl-mesa-gallium-r300
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT +libstdcpp +libdrm @TARGET_x86
  TITLE:=mesa gallium r300 driver
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-gallium-r600
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT +libstdcpp +libdrm @TARGET_x86
  TITLE:=mesa gallium r600 driver
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-gallium-radeonsi
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT +libstdcpp +libdrm @TARGET_x86
  TITLE:=mesa gallium radeonsi driver
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-gallium-svga
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT +libstdcpp +libdrm @TARGET_x86
  TITLE:=mesa gallium svga driver
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-gallium-swr
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT +libstdcpp +libdrm @TARGET_x86
  TITLE:=mesa gallium swr driver
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-gallium-swrast
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT +libstdcpp +libdrm
  TITLE:=mesa gallium swrast driver
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-gallium-softpipe
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT +libstdcpp +libdrm @TARGET_x86
  TITLE:=mesa gallium softpipe driver
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-gallium-i915
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT +libstdcpp +libdrm @TARGET_x86
  TITLE:=mesa gallium i915 driver
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-gallium-etnaviv
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT +libstdcpp +libdrm +libdrm-etnaviv_experimental_api @(arm||aarch64)
  TITLE:=mesa gallium etnaviv driver
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-gallium-imx
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT +libstdcpp +libdrm @(arm||aarch64)
  TITLE:=mesa gallium imx driver
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-gallium-freedreno
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT +libstdcpp +libdrm @(arm||aarch64)
  TITLE:=mesa gallium freedreno driver
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-gallium-nouveau
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT +libstdcpp +libdrm
  TITLE:=mesa gallium nouveau driver
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-gallium-tegra
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT +libstdcpp +libdrm +libgl-mesa-gallium-nouveau @(arm||aarch64)
  TITLE:=mesa gallium tegra driver
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-gallium-v3d
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT +libstdcpp +libdrm @(arm||aarch64)
  TITLE:=mesa gallium v3d driver
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-gallium-vc4
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT +libstdcpp +libdrm @(arm||aarch64)
  TITLE:=mesa gallium vc4 driver
  URL:=https://mesa.freedesktop.org
endef

define Package/libgl-mesa-gallium-pipe/Default
define Package/libgl-mesa-gallium-pipe-$(1)
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=libgl-mesa @DISPLAY_SUPPORT $(2)
  TITLE:=mesa gallium $(1) pipe driver
  URL:=https://mesa.freedesktop.org
endef
endef

DRI_DRV:=i810 i915 i965 mach64 mga r128 r200 r300 radeon s3v \
            savage sis tdfx trident unichrome ffb swrast

GALLIUM_DRV:=i915 nouveau r300 r600 radeonsi svga swr swrast \
            softpipe etnaviv imx freedreno tegra v3d vc4

$(foreach dri,$(DRI_DRV),$(eval $(call Package/libgl-mesa-dri/Default,$(dri))))

STAMP_CONFIGURED:=$(STAMP_CONFIGURED)_$(call confvar,CONFIG_PACKAGE_libgl-mesa \
    CONFIG_PACKAGE_libgl-mesa-egl \
	CONFIG_PACKAGE_libgl-mesa-gles-v1 \
	CONFIG_PACKAGE_libgl-mesa-gles-v2 \
	CONFIG_PACKAGE_libosmesa \
    $(foreach dri,$(DRI_DRV),CONFIG_PACKAGE_libgl-mesa-dri-$(dri)) \
	$(foreach dri,$(GALLIUM_DRV),CONFIG_PACKAGE_libgl-mesa-gallium-$(dri)))

define Build/Configure
	$(call Build/Configure/Default, \
		--disable-debug \
		--disable-glw \
		--disable-selinux \
		--disable-llvm \
		--disable-llvm-shared-libs \
		--enable-opengl \
		--enable-glx \
		$(if $(CONFIG_PACKAGE_libgl-mesa-egl),--enable-egl,--disable-egl) \
		$(if $(CONFIG_PACKAGE_libosmesa),--enable-gallium-osmesa,--disable-gallium-osmesa) \
		$(if $(CONFIG_PACKAGE_libgl-mesa-gles-v1),--enable-gles1,--disable-gles1) \
		$(if $(CONFIG_PACKAGE_libgl-mesa-gles-v2),--enable-gles2,--disable-gles2) \
		--with-driver=dri \
		--with-platforms="x11 drm" \
		--with-dri-drivers=" \
		$(foreach dri,$(DRI_DRV),$(if $(CONFIG_PACKAGE_libgl-mesa-dri-$(dri)),$(dri)))" \
		--with-gallium-drivers="\
		$(foreach dri,$(GALLIUM_DRV),$(if $(CONFIG_PACKAGE_libgl-mesa-gallium-$(dri)),$(dri)))" \
	)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/{include,lib/pkgconfig}
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/include/* \
		$(1)/usr/include/

	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so* \
		$(1)/usr/lib

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig
endef

define Package/libgl-mesa/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libGL.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libglapi.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libgbm.so* \
		$(1)/usr/lib/
endef

define Package/libosmesa/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libOSMesa.so* \
		$(1)/usr/lib/
endef

define Package/libgl-mesa-egl/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libEGL.so* \
		$(1)/usr/lib/
endef

define Package/libgl-mesa-gles-v1/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libGLESv1_CM.so* \
		$(1)/usr/lib/
endef

define Package/libgl-mesa-gles-v2/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libGLESv2.so* \
		$(1)/usr/lib/
endef

define Package/libgl-mesa-gallium-r300/install
	$(INSTALL_DIR) $(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/r300_dri.so* \
		$(1)/usr/lib/dri/
endef

define Package/libgl-mesa-gallium-r600/install
	$(INSTALL_DIR) $(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/r600_dri.so* \
		$(1)/usr/lib/dri/
endef

define Package/libgl-mesa-gallium-radeonsi/install
	$(INSTALL_DIR) $(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/radeonsi_dri.so* \
		$(1)/usr/lib/dri/
endef

define Package/libgl-mesa-gallium-softpipe/install
	$(INSTALL_DIR) $(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/swrast_dri.so* \
		$(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/kms_swrast_dri.so* \
		$(1)/usr/lib/dri/
endef

define Package/libgl-mesa-gallium-svga/install
	$(INSTALL_DIR) $(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/vmwgfx_dri.so* \
		$(1)/usr/lib/dri/
endef

define Package/libgl-mesa-gallium-swr/install
	$(INSTALL_DIR) $(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/swrast_dri.so* \
		$(1)/usr/lib/dri/
endef

define Package/libgl-mesa-gallium-swrast/install
	$(INSTALL_DIR) $(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/kms_swrast_dri.so* \
		$(1)/usr/lib/dri/
endef

define Package/libgl-mesa-gallium-softpipe/install
	$(INSTALL_DIR) $(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/swrast_dri.so* \
		$(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/kms_swrast_dri.so* \
		$(1)/usr/lib/dri/
endef


define Package/libgl-mesa-gallium-i915/install
	$(INSTALL_DIR) $(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/i915_dri.so* \
		$(1)/usr/lib/dri/
endef

define Package/libgl-mesa-gallium-etnaviv/install
	$(INSTALL_DIR) $(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/etnaviv_dri.so* \
		$(1)/usr/lib/dri/
endef

define Package/libgl-mesa-gallium-imx/install
	$(INSTALL_DIR) $(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/imx-drm_dri.so* \
		$(1)/usr/lib/dri/
endef

define Package/libgl-mesa-gallium-freedreno/install
	$(INSTALL_DIR) $(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/msm_dri.so* \
		$(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/kgsl_dri.so* \
		$(1)/usr/lib/dri/
endef

define Package/libgl-mesa-gallium-nouveau/install
	$(INSTALL_DIR) $(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/nouveau_dri.so* \
		$(1)/usr/lib/dri/
endef

define Package/libgl-mesa-gallium-tegra/install
	$(INSTALL_DIR) $(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/tegra_dri.so* \
		$(1)/usr/lib/dri/
endef

define Package/libgl-mesa-gallium-v3d/install
	$(INSTALL_DIR) $(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/v3d_dri.so* \
		$(1)/usr/lib/dri/
endef

define Package/libgl-mesa-gallium-vc4/install
	$(INSTALL_DIR) $(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/vc4_dri.so* \
		$(1)/usr/lib/dri/
endef

define Package/libgl-mesa-dri/install/Default
define Package/libgl-mesa-dri-$(1)/install
	$(INSTALL_DIR) $(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/$(2)_dri.so* \
		$(1)/usr/lib/dri
endef
endef

define Package/libgl-mesa-gallium-pipe/install/Default
define Package/libgl-mesa-gallium-pipe-$(1)/install
	$(INSTALL_DIR) $$(1)/usr/lib/gallium-pipe/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/gallium-pipe/pipe_$(1).so* \
		$$(1)/usr/lib/gallium-pipe
endef
endef

$(foreach dri,$(DRI_DRV),$(eval $(call Package/libgl-mesa-dri/install/Default,$(dri),$(dri))))
$(eval $(call Package/libgl-mesa-dri/install/Default,$(dri)))

$(eval $(call BuildPackage,libgl-mesa))
$(eval $(call BuildPackage,libgl-mesa-egl))
$(eval $(call BuildPackage,libgl-mesa-gles-v1))
$(eval $(call BuildPackage,libgl-mesa-gles-v2))
$(foreach dri,$(DRI_DRV),$(eval $(call BuildPackage,libgl-mesa-dri-$(dri))))
$(foreach dri,$(GALLIUM_DRV),$(eval $(call BuildPackage,libgl-mesa-gallium-$(dri))))
