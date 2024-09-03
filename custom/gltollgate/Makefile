include $(TOPDIR)/rules.mk

PKG_NAME:=gltollgate
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/chGoodchild/GLTollGate.git
PKG_SOURCE_VERSION:=endian_problems
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
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
	rm -rf $(PKG_BUILD_DIR)
	mkdir -p $(PKG_BUILD_DIR)
	git clone $(PKG_SOURCE_URL) $(PKG_BUILD_DIR) --branch $(PKG_SOURCE_VERSION) --single-branch
	(cd $(PKG_BUILD_DIR); git submodule update --init --recursive)
	[ -d "$(PKG_BUILD_DIR)/nostr/c" ] && $(CP) $(PKG_BUILD_DIR)/nostr/c/* $(PKG_BUILD_DIR)/ || (echo "The expected subdirectory does not exist." && exit 1)
	# Execute the script to generate config.h
	(cd $(PKG_BUILD_DIR); ./generate_config_h.sh)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC=$(TARGET_CC) \
		CFLAGS="$(TARGET_CFLAGS) -I$(STAGING_DIR)/usr/include -I$(STAGING_DIR)/target-mips_24kc_musl/usr/include" \
		LDFLAGS="$(TARGET_LDFLAGS) \
		-L$(STAGING_DIR)/usr/lib \
		-L$(STAGING_DIR)/target-mips_24kc_musl/usr/lib \
		-L$(STAGING_DIR)/target-mips_24kc_musl/root-ath79/usr/lib \
		-L$(BUILD_DIR)/libwallycore-0.8.1/src/.libs \
		-L$(BUILD_DIR)/libsecp256k1-0.1/.libs \
		$(BUILD_DIR)/libsecp256k1-0.1/.libs/libsecp256k1.a \
		-static" \
		$(TARGET_CONFIGURE_OPTS)
endef

define Package/gltollgate/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/generate_npub $(1)/usr/bin/
endef

$(eval $(call BuildPackage,gltollgate))

