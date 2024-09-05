include $(TOPDIR)/rules.mk

PKG_NAME:=tollgateconfigs
PKG_VERSION:=1.0
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=base
  CATEGORY:=Base system
  TITLE:=TollGate custom configurations
endef

define Package/$(PKG_NAME)/description
  Custom configurations and scripts for TollGate system.
endef

define Build/Compile
	# No compilation needed
endef

define Package/$(PKG_NAME)/install
  $(INSTALL_DIR) $(1)/etc
  $(CP) ./files/* $(1)/etc/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
