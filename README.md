# xorg feeds

This is a surviving copy of the openwrt xorg feed which used to be on svn before.. 

## mesa build

The Mesa project began as an open-source implementation of the OpenGL specification - a system for rendering interactive 3D graphics.

Mesa depends libdrm for graphics rendering, and openwrt provides a default libdrm which misses some features. So we provide a replacement for it in xorg feeds. If we want to compile mesa correctly, we
have to follow the steps below:

1. Uninstall libdrm provided by openwrt base package
2. Install libdrm provided with xorg feeds
3. Select the packages you platform needs for libdrm and mesa.