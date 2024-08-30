include $(TOPDIR)/rules.mk

PKG_NAME:=relaylink
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/chGoodchild/GLTollGate.git
PKG_SOURCE_VERSION:=42-generate-nsec-on-the-router
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/gltollgate-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/relaylink
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=RelayLink Utility
	DEPENDS:=+libwebsockets +libopenssl +libcap +gltollgate
endef

define Package/relaylink/description
	RelayLink utility for OpenWrt
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
	$(TARGET_CC) $(TARGET_CFLAGS) -I$(STAGING_DIR)/usr/include \
		-o $(PKG_BUILD_DIR)/RelayLink $(PKG_BUILD_DIR)/RelayLink.c \
		$(TARGET_LDFLAGS) \
		-L$(STAGING_DIR)/usr/lib \
		-lwebsockets -lssl -lcrypto -lcap -latomic \
		-static
endef

define Package/relaylink/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/RelayLink $(1)/usr/bin/
endef

$(eval $(call BuildPackage,relaylink))
