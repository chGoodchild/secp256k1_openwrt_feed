include $(TOPDIR)/rules.mk

PKG_NAME:=gltollgate
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/chGoodchild/GLTollGate.git
PKG_SOURCE_VERSION:=42-generate-nsec-on-the-router
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/gltollgate
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=GLTollGate Utilities
	DEPENDS:=+libopenssl +libsecp256k1 +libwallycore
endef

define Package/gltollgate/description
	GLTollGate Utilities including generate_npub tool.
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) $(TOPDIR)/../GLTollGate/nostr/c/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	$(TARGET_CC) $(TARGET_CFLAGS) $(TARGET_LDFLAGS) \
	-I$(STAGING_DIR)/usr/include \
	-I$(TOPDIR)/../nostr_client_relay/src/nostril \ 
	-o $(PKG_BUILD_DIR)/generate_npub $(PKG_BUILD_DIR)/generate_npub.c \
	-lwallycore -lssl -lsecp256k1
endef

define Package/gltollgate/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/generate_npub $(1)/usr/bin/
endef

$(eval $(call BuildPackage,gltollgate))

