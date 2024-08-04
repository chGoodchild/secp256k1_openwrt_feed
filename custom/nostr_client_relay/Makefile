include $(TOPDIR)/rules.mk

PKG_NAME:=nostr_client_relay
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/chGoodchild/nostr_client_relay.git
PKG_SOURCE_VERSION:=master
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/nostr_client_relay
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Client relay for Nostr protocol
  DEPENDS:=+libopenssl
endef

define Package/nostr_client_relay/description
  This package provides a client relay implementation for the Nostr decentralized communication protocol.
endef

CMAKE_OPTIONS += \
	-DENABLE_SSL_SUPPORT=ON

define Package/nostr_client_relay/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/nostr_client_relay $(1)/usr/bin/
endef

$(eval $(call BuildPackage,nostr_client_relay))
