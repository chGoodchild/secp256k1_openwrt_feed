include $(TOPDIR)/rules.mk

PKG_NAME:=signevent
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/chGoodchild/GLTollGate.git
PKG_SOURCE_VERSION:=main
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/gltollgate-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/signevent
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=SignEvent Utility
	DEPENDS:=+libsecp256k1 +gltollgate
endef

define Package/signevent/description
	SignEvent utility for OpenWrt
endef


define Build/Prepare
	rm -rf $(PKG_BUILD_DIR)
	mkdir -p $(PKG_BUILD_DIR)
	git clone $(PKG_SOURCE_URL) $(PKG_BUILD_DIR) --branch $(PKG_SOURCE_VERSION) --single-branch
	(cd $(PKG_BUILD_DIR); git submodule update --init --recursive)
	[ -d "$(PKG_BUILD_DIR)/nostr/c" ] && $(CP) $(PKG_BUILD_DIR)/nostr/c/* $(PKG_BUILD_DIR)/ || (echo "The expected subdirectory does not exist." && exit 1)
	# Execute the script to generate config.h if it exists
	[ -f "$(PKG_BUILD_DIR)/generate_config_h.sh" ] && (cd $(PKG_BUILD_DIR); ./generate_config_h.sh)
endef

define Build/Compile
	$(TARGET_CC) $(TARGET_CFLAGS) \
		-I$(STAGING_DIR)/usr/include \
		-o $(PKG_BUILD_DIR)/sign_event \
		$(PKG_BUILD_DIR)/sign_event.c \
		$(TARGET_LDFLAGS) \
		-L$(STAGING_DIR)/usr/lib \
		-lsecp256k1 \
		-static
endef

define Package/signevent/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/sign_event $(1)/usr/bin/
endef

$(eval $(call BuildPackage,signevent))

