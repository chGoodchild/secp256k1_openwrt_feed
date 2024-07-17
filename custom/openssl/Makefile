include $(TOPDIR)/rules.mk

PKG_NAME:=openssl
PKG_VERSION:=3.3.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/openssl/openssl/releases/download/openssl-$(PKG_VERSION)/$(PKG_SOURCE)
PKG_HASH:=777cd596284c883375a2a7a11bf5d2786fc5413255efab20c50d6ffe6d020b7e

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/openssl
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=OpenSSL
  URL:=https://www.openssl.org
endef

define Package/openssl/description
  OpenSSL is a robust, full-featured Open Source toolkit implementing the Secure Sockets Layer (SSL v2/v3) and Transport Layer Security (TLS v1) protocols as well as a full-strength general purpose cryptography library.
endef

define Build/Configure
  cd $(PKG_BUILD_DIR) && ./config --prefix=/usr --openssldir=/etc/ssl no-shared
endef

define Build/Compile
  $(MAKE) -C $(PKG_BUILD_DIR)
endef

define Package/openssl/install
  $(INSTALL_DIR) $(1)/usr/lib
  $(CP) $(PKG_BUILD_DIR)/libssl.so* $(1)/usr/lib/
  $(CP) $(PKG_BUILD_DIR)/libcrypto.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,openssl))

