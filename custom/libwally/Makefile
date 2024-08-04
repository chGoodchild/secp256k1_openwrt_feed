include $(TOPDIR)/rules.mk

PKG_NAME:=libwally
PKG_VERSION:=0.8.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/ElementsProject/libwally-core.git
PKG_SOURCE_VERSION:=master
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/libwally
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=A library for Bitcoin wallet development
  URL:=https://github.com/ElementsProject/libwally-core
  DEPENDS:=+libgmp
endef

define Package/libwally/description
  libwally-core is a cross-platform, cross-language collection of useful primitives for cryptocurrency wallets.
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	$(call GitCheckoutSubmodules)
endef

define Build/Configure
	$(call Build/Configure/Default)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
	CC="$(TARGET_CC)" \
	CFLAGS="$(TARGET_CFLAGS) -std=c99" \
	LDFLAGS="$(TARGET_LDFLAGS)" \
	all
endef

define Package/libwally/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/src/.libs/*.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libwally))
