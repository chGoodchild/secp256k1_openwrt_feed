include $(TOPDIR)/rules.mk

PKG_NAME:=libwebsockets
PKG_VERSION:=4.3.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/warmcat/libwebsockets/archive/refs/tags/v$(PKG_VERSION).tar.gz
PKG_HASH:=6fd33527b410a37ebc91bb64ca51bdabab12b076bc99d153d7c5dd405e4bdf90

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/libwebsockets
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Libwebsockets library
  URL:=https://libwebsockets.org
endef

define Package/libwebsockets/description
  Libwebsockets is a flexible, lightweight pure C library for implementing WebSocket clients and servers.
endef

define Build/Configure
  $(call Build/Configure/Default, -DCMAKE_INSTALL_PREFIX=/usr -DLWS_WITH_STATIC=OFF -DLWS_WITH_SHARED=ON)
endef

define Build/Compile
  $(MAKE) -C $(PKG_BUILD_DIR)
endef

define Package/libwebsockets/install
  $(INSTALL_DIR) $(1)/usr/lib
  $(CP) $(PKG_BUILD_DIR)/lib/*.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libwebsockets))

