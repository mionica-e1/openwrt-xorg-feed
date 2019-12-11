#
# Copyright (C) 2007-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_BASE_NAME:=font-base
PKG_NAME:=font-misc-misc
PKG_RELEASE:=1
PKG_VERSION:=1.1.2
PKG_SOURCE_URL:=http://xorg.freedesktop.org/releases/individual/font
PKG_HASH:=b8e77940e4e1769dc47ef1805918d8c9be37c708735832a07204258bacc11794

include $(INCLUDE_DIR)/package.mk

define Package/font-misc-misc/Default
  SECTION:=xorg-font
  CATEGORY:=Xorg
  SUBMENU:=font
endef

define Package/font-base
  $(call Package/font-misc-misc/Default)
  DEPENDS:=+xserver +font-util @DISPLAY_SUPPORT
  TITLE:=font-base
  URL:=http://xorg.freedesktop.org/
endef

define Package/font-misc-misc
  $(call Package/font-misc-misc/Default)
  DEPENDS:=font-base
  TITLE:=font-misc-misc
  URL:=http://xorg.freedesktop.org/
endef


CONFIGURE_ARGS_XTRA+= \
			--disable-iso8859-2 \
			--disable-iso8859-3 \
			--disable-iso8859-4 \
			--disable-iso8859-5 \
			--disable-iso8859-7 \
			--disable-iso8859-8 \
			--disable-iso8859-9 \
			--disable-iso8859-10 \
			--disable-iso8859-11 \
			--disable-iso8859-13 \
			--disable-iso8859-14 \
			--disable-iso8859-16 \
			--disable-koi8-r \
			--disable-jisx0201

CONFIGURE_ARGS += \
			--prefix=$(PKG_INSTALL_DIR) \
			--with-fontdir="/usr/share/fonts/misc"

define Build/Compile
	UTIL_DIR="$(STAGING_DIR)/usr/share/fonts/X11/util/" make -e -C $(PKG_BUILD_DIR)
	DESTDIR=ipkg-install $(MAKE) -C $(PKG_BUILD_DIR) install
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR)/$(CONFIGURE_PATH); \
	if [ -x $(CONFIGURE_CMD) ]; then \
		$(CP) $(SCRIPT_DIR)/config.{guess,sub} $(PKG_BUILD_DIR)/ && \
			$(CONFIGURE_VARS) \
			$(CONFIGURE_CMD) \
			$(CONFIGURE_ARGS_XTRA) \
			$(CONFIGURE_ARGS) ;\
	fi \
	)
endef

define Build/InstallDev
	DESTDIR=$(1) $(MAKE) -C $(PKG_BUILD_DIR)/  $(MAKE_FLAGS) install
endef

define Package/font-base/install
	$(INSTALL_DIR) $(1)/usr/share/fonts/misc/
	$(CP) $(PKG_INSTALL_DIR)/usr/share/fonts/misc/6x13* $(1)/usr/share/fonts/misc/
	$(CP) files/fonts.dir.font-base $(1)/usr/share/fonts/misc/
endef

define Package/font-misc-misc/install
	$(INSTALL_DIR) $(1)/usr/share/fonts/misc/
	$(CP) $(PKG_INSTALL_DIR)/usr/share/fonts/misc/* $(1)/usr/share/fonts/misc/
	rm $(1)/usr/share/fonts/misc/6x13*
	$(CP) files/fonts.dir.font-misc-misc $(1)/usr/share/fonts/misc/
endef

define Package/font-base/postinst
#!/bin/sh

FILE_NEW=`find $${IPKG_INSTROOT} -name fonts.dir.font-base`
FILE_OLD=`dirname $${FILE_NEW}`/fonts.dir

echo found $${FILE}

if [ ! -z $${FILE_NEW} ]; then
	if [ -f $${FILE_OLD} ]; then
		sed -i "1d" $${FILE_OLD}
		cat $${FILE_NEW} >> $${FILE_OLD}
		rm -rf $${FILE_NEW}
		mv $${FILE_OLD} $${FILE_OLD}.tmp
	else
		mv $${FILE_NEW} $${FILE_OLD}.tmp
	fi
	(echo `wc -l $${FILE_OLD}.tmp | awk '{print($$1)}'`; cat $${FILE_OLD}.tmp) > $${FILE_OLD}
	rm $${FILE_OLD}.tmp
fi
endef

define Package/font-misc-misc/postinst
#!/bin/sh

FILE_NEW=`find $${IPKG_INSTROOT} -name fonts.dir.font-misc-misc`
FILE_OLD=`dirname $${FILE_NEW}`/fonts.dir

echo found $${FILE}

if [ ! -z $${FILE_NEW} ]; then
	if [ -f $${FILE_OLD} ]; then
		sed -i "1d" $${FILE_OLD}
		cat $${FILE_NEW} >> $${FILE_OLD}
		rm -rf $${FILE_NEW}
		mv $${FILE_OLD} $${FILE_OLD}.tmp
	else
		mv $${FILE_NEW} $${FILE_OLD}.tmp
	fi
	(echo `wc -l $${FILE_OLD}.tmp | awk '{print($$1)}'`; cat $${FILE_OLD}.tmp) > $${FILE_OLD}
	rm $${FILE_OLD}.tmp
fi
endef

# FIXME: replace with native versions
$(eval $(call RequireCommand,mkfontscale, \
	Please install mkfontscale (usually in xfonts-utils) \
))
$(eval $(call RequireCommand,mkfontdir, \
	Please install mkfontdir (usually in xfonts-utils) \
))

$(eval $(call BuildPackage,font-misc-misc))
$(eval $(call BuildPackage,font-base))


