include $(TOPDIR)/rules.mk

PKG_NAME:=libcamera
PKG_RELEASE:=$(COMMITCOUNT)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://git.libcamera.org/libcamera/libcamera.git
PKG_SOURCE_VERSION:=v0.1.0
PKG_MIRROR_HASH:=de6511b2e494d54fb4432eeb3d4d1644133b5c14305aeb1f97e8e1d67d043611

PKG_VERSION:=$(PKG_SOURCE_VERSION)
PKG_LICENSE:=LGPL-2.1-or-later
PKG_LICENSE_FILES:=COPYING.rst

#include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/meson.mk
RSTRIP:=:
STRIP:=:

HOST_BUILD_DEPENDS:=python3/host
#include $(INCLUDE_DIR)/host-build.mk 
#include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

PYTHON3_PKG_BUILD:=0
HOST_PYTHON3_PACKAGE_BUILD_DEPENDS:=./pyyaml.txt ply ./jinja2.txt

define Package/libcamera
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=A complex camera support library
  URL:=https://libcamera.org
  # libevent2 is used by the cam app
  # Some of these dependencies are actually unnecessary. The problem is the meson
  # build auto-detects since they exist in our build env for other reasons.
  #DEPENDS:=+libopenssl +libstdcpp +libyaml +libudev +libgnutls +libdw +libevent2 +libevent2-pthreads
  DEPENDS:=+libopenssl +libstdcpp +libyaml +libudev +libdw +libevent2 +libevent2-pthreads
endef

#MESON_ARGS += 

#define Build/Configure
	#$(call Py3Build/InstallBuildDepends)
#	$(call Build/Configure/Meson)
#endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/libcamera
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libcamera $(1)/usr/include/libcamera
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib
endef

define Package/libcamera/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/cam $(1)/usr/bin
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libcamera*.so* $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/lib/libcamera
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libcamera/*.so* $(1)/usr/lib/libcamera
endef

$(eval $(call BuildPackage,libcamera))
