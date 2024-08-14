include $(TOPDIR)/rules.mk

PKG_NAME:=gltollgate
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/chGoodchild/GLTollGate.git
PKG_SOURCE_VERSION:=42-generate-nsec-on-the-router
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
	# Check if the .git directory exists, indicating a repo clone is there
	if [ ! -d "$(PKG_BUILD_DIR)/.git" ]; then
		git clone $(PKG_SOURCE_URL) $(PKG_BUILD_DIR) --branch $(PKG_SOURCE_VERSION) --single-branch;
	else
		(cd $(PKG_BUILD_DIR); git fetch origin; git reset --hard $(PKG_SOURCE_VERSION))
	fi
	# Ensuring submodules are updated in case they exist
	(cd $(PKG_BUILD_DIR); git submodule update --init --recursive)
	# Verify the correct subdirectory and copy from it
	if [ -d "$(PKG_BUILD_DIR)/nostr/c" ]; then
		$(CP) $(PKG_BUILD_DIR)/nostr/c/* $(PKG_BUILD_DIR)/
	else
	echo "The expected subdirectory does not exist."
	exit 1
	fi
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./$(PKG_NAME)-$(PKG_VERSION)/* $(PKG_BUILD_DIR)/
	$(info Contents of PKG_BUILD_DIR:)
	$(shell ls -la $(PKG_BUILD_DIR))
endef

define Package/gltollgate/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/generate_npub $(1)/usr/bin/
endef

$(eval $(call BuildPackage,gltollgate))

