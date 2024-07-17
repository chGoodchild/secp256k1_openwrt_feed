include $(TOPDIR)/rules.mk

PKG_NAME:=jansson
PKG_VERSION:=2.14
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/akheron/jansson/releases/download/v$(PKG_VERSION)/$(PKG_SOURCE)
PKG_HASH:=5798d010e41cf8d76b66236cfb2f2543c8d082181d16bc3085ab49538d4b9929

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/jansson
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Jansson JSON library
  URL:=https://github.com/akheron/jansson
endef

define Package/jansson/description
  Jansson is a C library for encoding, decoding, and manipulating JSON data.
endef

define Build/Configure
  $(call Build/Configure/Default, --disable-shared --enable-static)
endef

define Build/Compile
  $(MAKE) -C $(PKG_BUILD_DIR)
endef

define Package/jansson/install
  $(INSTALL_DIR) $(1)/usr/lib
  $(CP) $(PKG_BUILD_DIR)/src/.libs/libjansson.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,jansson))

