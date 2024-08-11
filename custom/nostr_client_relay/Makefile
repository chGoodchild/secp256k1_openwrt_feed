include $(TOPDIR)/rules.mk

PKG_NAME:=nostr_client_relay
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/chGoodchild/nostr_client_relay.git
PKG_SOURCE_VERSION:=main
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_MIRROR_HASH:=5df4821b11382b559fce399774d5aef25c141df42ac409199689ac6e455f7c09

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/nostr_client_relay
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Client relay for Nostr protocol
	DEPENDS:=+libopenssl +libsecp256k1 +libwally
endef

define Package/nostr_client_relay/description
	This package provides a client relay implementation for the Nostr decentralized communication protocol.
endef

TARGET_CFLAGS += -I$(STAGING_DIR)/target-mips_24kc_musl/usr/include
TARGET_LDFLAGS += -L$(STAGING_DIR)/target-mips_24kc_musl/usr/lib

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	# Copy all files from the nostr_client_relay repository root
	$(CP) $(TOPDIR)/../nostr_client_relay/* $(PKG_BUILD_DIR)/
endef

CMAKE_OPTIONS += \
	-DENABLE_SSL_SUPPORT=ON \
	-DCMAKE_C_FLAGS="$(TARGET_CFLAGS)" \
	-DCMAKE_LIBRARY_PATH=$(STAGING_DIR)/target-mips_24kc_musl/usr/lib \
	-DCMAKE_INCLUDE_PATH=$(STAGING_DIR)/target-mips_24kc_musl/usr/include

CMAKE_OPTIONS += \
	-DENABLE_SSL_SUPPORT=ON \
	-DCMAKE_C_FLAGS="$(TARGET_CFLAGS)"

define Package/nostr_client_relay/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/nostr_client_relay $(1)/usr/bin/
endef

$(eval $(call BuildPackage,nostr_client_relay))

