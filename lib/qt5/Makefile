#
# Copyright (C) 2013 Riccardo Ferrazzo <f.riccardo87@gmail.com>
# Copyright (C) 2017 Paweł Knioła <pawel.kn@gmail.com>
# Copyright (C) 2019 Han Pengfei <pengphei@foxmail.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qt5
PKG_VERSION:=5.6
PKG_RELEASE:=3
PKG_MD5SUM:=010342d515b62ee1c0e709254f4ef9ab

PKG_SOURCE:=qt-everywhere-opensource-src-$(PKG_VERSION).$(PKG_RELEASE).tar.xz
PKG_SOURCE_URL:=http://download.qt-project.org/archive/qt/$(PKG_VERSION)/$(PKG_VERSION).$(PKG_RELEASE)/single
PKG_BUILD_DIR=$(BUILD_DIR)/qt-everywhere-opensource-src-$(PKG_VERSION).$(PKG_RELEASE)
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0
PKG_BUILD_DEPENDS:=+libstdcpp

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
-include $(if $(DUMP),,./files/qmake.mk)

# not using sstrip here as this fucks up the .so's somehow
STRIP:=/bin/true
RSTRIP:= \
  NM="$(TOOLCHAIN_DIR)/bin/$(TARGET_CROSS)nm" \
  STRIP="$(STRIP)" \
  STRIP_KMOD="$(STRIP)" \
  $(SCRIPT_DIR)/rstrip.sh

define Package/qt5/Default
  SECTION:=xorg-framework
  CATEGORY:=Xorg
  SUBMENU:=framework
  URL:=http://www.qt.io/
endef

define Package/qt5
  $(call Package/qt5/Default)
  TITLE:=qt5
  DEPENDS:= \
  	+librt \
  	+libstdcpp \
  	+libatomic \
  	+libpthread \
	$(ICONV_DEPENDS) \
	@DISPLAY_SUPPORT \
	@!LINUX_2_4
endef

QT5_GUI_DEPS:=\
	+qt5-plugin-generic \
	+qt5-plugin-platforms \
	+qt5-plugin-imageformats \

define Package/qt5/config
	menu "Qt5 Base Config"
		depends on PACKAGE_qt5
	
		config QT5_ZLIB
			bool "Enable qt5 zlib (system)"
			select PACKAGE_zlib
			default n

	endmenu

	menu "Qt5 Gui Config"
		depends on PACKAGE_qt5

		config QT5_LINUXFB
			bool "Enable qt5 linuxfb backend"
			default n

		config QT5_DIRECTFB
			depends on FEATURE_drawing-backend_DirectFB
			bool "Enable qt5 directfb backend"
			default n

		config QT5_X11
			depends on FEATURE_drawing-backend_libX11
			bool "Enable qt5 X11 backend"
            select PACKAGE_xorg
            select PACKAGE_libX11
            select PACKAGE_libXext
			default n

		config QT5_EGLFS
			bool "Enable qt5 eglfs backend"
			default n

		config QT5_XCB
			bool "Enable qt5 xcb backend"
			default n

		config QT5_WAYLAND
			bool "Enable qt5 wayland backend"
			select PACKAGE_wayland
			default n

		config QT5_KMS
			bool "Enable qt5 kms backend"
			select PACKAGE_libdrm
			default n

		config QT5_LIBPNG
			bool "Enable qt5 png (system)"
			select PACKAGE_libpng
			default n

		config QT5_LIBJPEG
			bool "Enable qt5 jpeg (system)"
			select PACKAGE_libjpeg
			default n

		config QT5_LIBTIFF
			bool "Enable qt5 tiff (system)"
			select PACKAGE_libtiff
			default n

		config QT5_ICONV
			bool "Enable qt5 iconv support"
			select PACKAGE_libiconv-full
			default n

		config QT5_GIF
			bool "Enable qt5 gif support"
			select PACKAGE_giflib
			default n

		config QT5_FREETYPE
			bool "Enable qt5 freetype (system)"
			select PACKAGE_libfreetype
			default n

		config QT5_FONTCONFIG
			bool "Enable qt5 fontconfig support"
			select PACKAGE_fontconfig
			default n

		config QT5_LIBINPUT
			bool "Enable qt5 libinput support"
			select PACKAGE_libinput
			default n

		config QT5_TSLIB
			bool "Enable qt5 tslib support"
			select PACKAGE_tslib
			default n

		config QT5_MTDEV
			bool "Enable qt5 multi touch input"
			select PACKAGE_mtdev
			default n

		config QT5_EVDEV
			bool "Enable qt5 evdev support"
			select PACKAGE_libevdev
			default n

        config QT5_XKBCOMMON_EVDEV
			bool "Enable qt5 xkbcommon evdev support"
			select PACKAGE_libxkbcommon
			default n

		config QT5_ALSA
			bool "Enable qt5 alsa support"
			select PACKAGE_alsa-lib
			default n

		config QT5_OPENGL
			bool "Enable qt5 opengl support"
			default n
			
	endmenu

	menu "Qt5 SQL Plugin"
		depends on PACKAGE_qt5

		config QT5_SQLITE
			bool "Enable qt5 sqlite (system)"
			select PACKAGE_libsqlite3
			default n

		config QT5_MYSQL
			bool "Enable qt5 mysql support"
			select PACKAGE_libmysqlclient
			default n

		config QT5_PGSQL
			bool "Enable qt5 pgsql support"
			select PACKAGE_pgsql-cli
			default n

		config QT5_ODBC
			bool "Enable qt5 odbc support"
			select PACKAGE_unixodbc
			default n

	endmenu
endef


# $(1): package name & command in /usr/bin/
# $(2): package dependencies
# $(3): package final lib name
# $(4): package source path
define BuildSubPackage

  define Package/$(1)
  $(call Package/qt5/Default)
    DEPENDS:=qt5  $(2)
    TITLE+=$(1)
  endef

  define Package/$(1)/description
   Qt5 $(1) lib
  endef

  define Package/$(1)/install
	$(INSTALL_DIR) $$(1)/usr/lib/
	$(CP) $(foreach f,$(3),$(PKG_BUILD_DIR)/$(4)/lib/lib$(f).so*) $$(1)/usr/lib/
  endef

  $$(eval $$(call BuildPackage,$(1)))
endef

# $(1): package name
# $(2): package plugin dependencies
# $(3): package plugin path
define BuildPluginPackage

  define Package/$(1)
  $(call Package/qt5/Default)
    DEPENDS:=qt5 $(2)
    TITLE:=Qt5 $(3) Plugin
  endef

  define Package/$(1)/description
   Qt5 $(3) Plugin
  endef

  define Package/$(1)/install
	$(INSTALL_DIR) $$(1)/usr/lib/Qt5/plugins/$(3)
	$(CP) $(PKG_BUILD_DIR)/qtbase/plugins/$(3)/*.so $$(1)/usr/lib/Qt5/plugins/$(3)/
  endef

  $$(eval $$(call BuildPackage,$(1)))
endef

define Build/Configure
	$(INSTALL_DIR) $(PKG_BUILD_DIR)/qtbase/mkspecs/linux-openwrt-g++
	$(CP) ./files/qplatformdefs.h $(PKG_BUILD_DIR)/qtbase/mkspecs/linux-openwrt-g++/qplatformdefs.h
	$(CP) ./files/qmake.conf $(PKG_BUILD_DIR)/qtbase/mkspecs/linux-openwrt-g++/qmake.conf
	$(SED) 's@$$$$(TARGET_CROSS)@$(TARGET_CROSS)@g' $(PKG_BUILD_DIR)/qtbase/mkspecs/linux-openwrt-g++/qmake.conf
	( cd $(PKG_BUILD_DIR) ; \
		TARGET_CC="$(TARGET_CROSS)gcc" \
		TARGET_CXX="$(TARGET_CROSS)g++" \
		TARGET_AR="$(TARGET_CROSS)ar cqs" \
		TARGET_OBJCOPY="$(TARGET_CROSS)objcopy" \
		TARGET_RANLIB="$(TARGET_CROSS)ranlib" \
		TARGET_CFLAGS="$(TARGET_CFLAGS) $(EXTRA_CFLAGS)" \
		TARGET_CXXFLAGS="$(TARGET_CFLAGS) $(EXTRA_CFLAGS)" \
		TARGET_LDFLAGS="$(TARGET_LDFLAGS) $(EXTRA_LDFLAGS) -lpthread -lrt" \
		TARGET_INCDIRS="$(TARGET_INCDIRS)" \
		TARGET_LIBDIRS="$(TARGET_LIBDIRS) $(STAGING_DIR)/usr/lib/" \
		CFLAGS= \
		CXXFLAGS= \
		LDFLAGS= \
		./configure \
			-prefix /usr \
			-extprefix $(TOOLCHAIN_DIR) \
			-sysroot $(TOOLCHAIN_DIR) \
			-plugindir /usr/lib/Qt/plugins \
			-xplatform linux-openwrt-g++ \
			-opensource \
			-confirm-license \
			-no-pch \
			-no-rpath \
			-no-qml-debug \
			-no-strip \
			-no-cups \
			-no-dbus \
			-no-libudev \
            $(if $(CONFIG_QT5_LINUXFB),-linuxfb,-no-linuxfb) \
            $(if $(CONFIG_QT5_DIRECTFB),-directfb,-no-directfb) \
            $(if $(CONFIG_QT5_EGLFS),-eglfs,-no-eglfs) \
            $(if $(CONFIG_QT5_XCB),-qt-xcb,-no-xcb) \
            $(if $(CONFIG_QT5_WAYLAND),-wayland,-no-wayland) \
            $(if $(CONFIG_QT5_KMS),-kms,-no-kms) \
            $(if $(CONFIG_QT5_FREETYPE),-freetype,-qt-freetype) \
            $(if $(CONFIG_QT5_FONTCONFIG),-fontconfig,-no-fontconfig) \
            $(if $(CONFIG_QT5_LIBGIF),-gif,-no-gif) \
            $(if $(CONFIG_QT5_LIBPNG),-libpng,-qt-libpng) \
            $(if $(CONFIG_QT5_LIBJPEG),-libjpeg,-qt-libjpeg) \
            $(if $(CONFIG_QT5_ICONV),-iconv,-no-iconv) \
            $(if $(CONFIG_QT5_TSLIB),-tslib,-no-tslib) \
            $(if $(CONFIG_QT5_LIBINPUT),-libinput,) \
            $(if $(CONFIG_QT5_MTDEV),-mtdev,-no-mtdev) \
            $(if $(CONFIG_QT5_EVDEV),-evdev,-no-evdev) \
            $(if $(CONFIG_QT5_XKBCOMMON_EVDEV),-xkbcommon-evdev,-no-xkbcommon-evdev) \
            $(if $(CONFIG_QT5_ZLIB),-zlib,-qt-zlib) \
            $(if $(CONFIG_QT5_OPENGL),-opengl,-no-opengl) \
            $(if $(CONFIG_QT5_SQLITE),-qt-sql-sqlite,-no-sql-sqlite) \
            $(if $(CONFIG_QT5_MYSQL),-qt-sql-mysql,-no-sql-mysql) \
            $(if $(CONFIG_QT5_PGSQL),-qt-sql-psql,-no-sql-psql) \
            $(if $(CONFIG_QT5_ODBC),-qt-sql-odbc,-no-sql-odbc) \
            $(if $(CONFIG_QT5_ALSA),-alsa,-no-alsa) \
			-make libs \
			-skip qtdeclarative \
			-skip qtmultimedia \
			-skip activeqt \
			-skip qtdoc \
			-skip qtconnectivity \
			-skip qtscript \
			-v \
	)
endef

define Build/Compile
	TARGET_CC="$(TARGET_CROSS)gcc" \
	TARGET_CXX="$(TARGET_CROSS)g++" \
	TARGET_AR="$(TARGET_CROSS)ar cqs" \
	TARGET_OBJCOPY="$(TARGET_CROSS)objcopy" \
	TARGET_RANLIB="$(TARGET_CROSS)ranlib" \
	TARGET_CFLAGS="$(TARGET_CFLAGS) $(EXTRA_CFLAGS)" \
	TARGET_CXXFLAGS="$(TARGET_CFLAGS) $(EXTRA_CFLAGS)" \
	TARGET_LDFLAGS="$(TARGET_LDFLAGS) $(EXTRA_LDFLAGS) -ldl -lpthread -lrt" \
	TARGET_INCDIRS="$(TARGET_INCDIRS)" \
	TARGET_LIBDIRS="$(TARGET_LIBDIRS) $(STAGING_DIR)/usr/lib/" \
	STAGING_DIR="$(STAGING_DIR)" \
	STAGING_DIR_HOST="$(STAGING_DIR)/../host" \
	PKG_CONFIG_SYSROOT="$(STAGING_DIR)" \
	$(MAKE) -C $(PKG_BUILD_DIR)
endef

define Build/InstallDev
	$(INSTALL_DIR) \
		$(STAGING_DIR_HOST)/usr/lib/qt5/bin

	# host tools (qmake, moc, rcc, uic)
	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/bin/{qmake,moc,rcc,uic} \
		$(STAGING_DIR_HOST)/usr/lib/qt5/bin/	

	$(INSTALL_DIR) \
		$(1)/usr/share/ \
		$(1)/usr/share/pkgconfig \
		$(1)/usr/include \
		$(1)/usr/include/qt5 \
		$(1)/usr/lib \
		$(1)/usr/lib/cmake \
		$(1)/usr/lib/qt5 \
		$(1)/usr/lib/qt5/plugins \
		$(1)/usr/lib/qt5/qml \
		$(1)/usr/lib/qt5/mkspecs

	$(CP) -r \
		$(PKG_BUILD_DIR)/qtbase/cmake/* \
		$(1)/usr/lib/cmake/

	$(CP) -r \
		$(PKG_BUILD_DIR)/qtbase/mkspecs/* \
		$(1)/usr/lib/qt5/mkspecs/

	$(INSTALL_DATA) \
		$(PKG_BUILD_DIR)/qtbase/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/

	$(CP) -r \
		$(PKG_INSTALL_DIR)/qtbase/include/* \
		$(1)/usr/include/qt5/

	$(CP) \
		$(PKG_INSTALL_DIR)/qtbase/lib/*.so* \
		$(1)/usr/lib/
endef

define Package/qt5/install
	true
endef

$(eval $(call BuildPackage,qt5))
$(eval $(call BuildSubPackage,qt5-core,,Qt5Core,qtbase))
$(eval $(call BuildSubPackage,qt5-concurrent,+qt5-core,Qt5Concurrent,qtbase))
$(eval $(call BuildSubPackage,qt5-network,+qt5-core,Qt5Network,qtbase))
$(eval $(call BuildPluginPackage,qt5-plugin-generic,+qt5-core +qt5-gui +qt5-network,generic))
$(eval $(call BuildPluginPackage,qt5-plugin-platforms,+qt5-core,platforms))
$(eval $(call BuildPluginPackage,qt5-plugin-imageformats,+qt5-core,imageformats))
$(eval $(call BuildSubPackage,qt5-gui,+qt5-widgets $(QT5_GUI_DEPS),Qt5Gui,qtbase))
$(eval $(call BuildSubPackage,qt5-widgets,+qt5-core,Qt5Widgets,qtbase))
$(eval $(call BuildPluginPackage,qt5-plugin-sqldrivers,+qt5-core,sqldrivers))
$(eval $(call BuildSubPackage,qt5-sql,+qt5-core +qt5-plugin-sqldrivers,Qt5Sql,qtbase))
$(eval $(call BuildSubPackage,qt5-xml,+qt5-core,Qt5Xml,qtbase))
$(eval $(call BuildSubPackage,qt5-test,+qt5-core,Qt5Test,qtbase))
$(eval $(call BuildSubPackage,qt5-printsupport,+qt5-core,Qt5PintSupport,qtbase))
$(eval $(call BuildSubPackage,qt5-svg,+qt5-core,Qt5Svg,qtsvg))
$(eval $(call BuildSubPackage,qt5-wayland-client,+qt5-core,Qt5WaylandClient,qtwayland))
$(eval $(call BuildSubPackage,qt5-xml-patterns,+qt5-xml +qt5-network,Qt5XmlPatterns,qtxmlpatterns))
$(eval $(call BuildSubPackage,qt5-location,+qt5-core,Qt5Positioning,qtlocation))
$(eval $(call BuildSubPackage,qt5-webchannel,+qt5-core +qt5-network,Qt5WebChannel,qtwebchannel))
$(eval $(call BuildSubPackage,qt5-websockets,+qt5-core +qt5-network,Qt5WebSockets,qtwebsockets))
$(eval $(call BuildSubPackage,qt5-serialbus,+qt5-core +qt5-network,Qt5SerialBus,qtserialbus))
$(eval $(call BuildSubPackage,qt5-serialport,+qt5-core,Qt5SerialPort,qtserialport))
$(eval $(call BuildSubPackage,qt5-sensors,+qt5-core,Qt5Sensors,qtsensors))
