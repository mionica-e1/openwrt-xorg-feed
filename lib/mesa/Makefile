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
PKG_BUILD_DEPENDS:=glproto

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

DRIDRIVERS:=i810 i915 i965 mach64 mga r128 r200 r300 radeon s3v \
            savage sis tdfx trident unichrome ffb swrast

GALLIUM_X86:=i915 nouveau r300 r600 radeon radeonsi svga swr \
            softpipe llvmpipe

GALLIUM_ARM:=etnaviv imx freedreno trega v3d v4c

$(foreach dri,$(DRIDRIVERS),$(eval $(call Package/libgl-mesa-dri/Default,$(dri))))
$(foreach dri,$(GALLIUM_X86),$(eval $(call Package/libgl-mesa-gallium/Default,$(dri),@TARGET_x86)))
$(foreach dri,$(GALLIUM_ARM),$(eval $(call Package/libgl-mesa-gallium/Default,$(dri),@arm)))

STAMP_CONFIGURED:=$(STAMP_CONFIGURED)_$(call confvar,CONFIG_PACKAGE_libgl-mesa \
    CONFIG_PACKAGE_libgl-mesa-egl \
	CONFIG_PACKAGE_libgl-mesa-gles-v1 \
	CONFIG_PACKAGE_libgl-mesa-gles-v2 \
    $(foreach dri,$(DRIDRIVERS),CONFIG_PACKAGE_libgl-mesa-dri-$(dri)) \
	$(foreach dri,$(GALLIUM_X86),CONFIG_PACKAGE_libgl-mesa-gallium-$(dri)) \
	$(foreach dri,$(GALLIUM_ARM),CONFIG_PACKAGE_libgl-mesa-gallium-$(dri)))

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
		$(if $(CONFIG_PACKAGE_libgl-mesa-gles-v1),--enable-gles1,--disable-gles1) \
		$(if $(CONFIG_PACKAGE_libgl-mesa-gles-v2),--enable-gles2,--disable-gles2) \
		--with-driver=dri \
		--with-platforms="x11 drm" \
		--with-dri-drivers=" \
		$(foreach dri,$(DRIDRIVERS),$(if $(CONFIG_PACKAGE_libgl-mesa-dri-$(dri)),$(dri)))" \
		--with-gallium-drivers="\
		$(foreach dri,$(GALLIUM_X86),$(if $(CONFIG_PACKAGE_libgl-mesa-gallium-$(dri)),$(dri))) \
		$(foreach dri,$(GALLIUM_ARM),$(if $(CONFIG_PACKAGE_libgl-mesa-gallium-$(dri)),$(dri)))" \
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

define Package/libgl-mesa-dri/install/Default
define Package/libgl-mesa-dri-$(1)/install
	$(INSTALL_DIR) $$(1)/usr/lib/dri/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/dri/$(2)_dri.so* \
		$$(1)/usr/lib/dri
endef
endef

define Package/libgl-mesa-gallium/install/Default
define Package/libgl-mesa-gallium-$(1)/install
	$(INSTALL_DIR) $$(1)/usr/lib/gallium-pipe/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/gallium-pipe/pipe_$(1).so* \
		$$(1)/usr/lib/gallium-pipe
endef
endef

$(foreach dri,$(DRIDRIVERS),$(eval $(call Package/libgl-mesa-dri/install/Default,$(dri),$(dri))))
$(foreach dri,$(GALLIUM_X86),$(eval $(call Package/libgl-mesa-gallium/install/Default,$(dri))))

$(eval $(call Package/libgl-mesa-dri/install/Default,$(dri)))

$(eval $(call BuildPackage,libgl-mesa))
$(eval $(call BuildPackage,libgl-mesa-egl))
$(eval $(call BuildPackage,libgl-mesa-gles-v1))
$(eval $(call BuildPackage,libgl-mesa-gles-v2))
$(foreach dri,$(DRIDRIVERS),$(eval $(call BuildPackage,libgl-mesa-dri-$(dri))))
$(foreach dri,$(GALLIUM_X86),$(eval $(call BuildPackage,libgl-mesa-gallium-$(dri))))
$(foreach dri,$(GALLIUM_ARM),$(eval $(call BuildPackage,libgl-mesa-gallium-$(dri))))

