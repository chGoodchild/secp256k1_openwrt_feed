include $(TOPDIR)/rules.mk

PKG_NAME:=secp256k1
PKG_VERSION:=0.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/bitcoin-core/secp256k1.git
PKG_SOURCE_VERSION:=HEAD

PKG_MIRROR_HASH:=skip

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/secp256k1
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Optimized C library for EC operations on curve secp256k1
  URL:=https://github.com/bitcoin-core/secp256k1
endef

define Package/secp256k1/description
  Optimized C library for EC operations on curve secp256k1
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	mkdir -p $(PKG_BUILD_DIR)
	echo "int main() { return 0; }" > $(PKG_BUILD_DIR)/dummy.c
endef

define Build/Compile
	$(TARGET_CC) $(TARGET_CFLAGS) $(PKG_BUILD_DIR)/dummy.c -o $(PKG_BUILD_DIR)/dummy
endef

define Package/secp256k1/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/dummy $(1)/usr/bin/dummy
endef

$(eval $(call BuildPackage,secp256k1))

