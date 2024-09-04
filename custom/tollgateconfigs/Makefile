include $(TOPDIR)/rules.mk

PKG_NAME:=tollgateconfigs
PKG_VERSION:=1.0
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/tollgateconfigs
  SECTION:=base
  CATEGORY:=Base system
  TITLE:=TollGate custom configurations
  DEPENDS:=
endef

define Package/tollgateconfigs/description
  Custom configurations and scripts for TollGate system.
endef

define Build/Compile
	# No compilation needed
endef

define Package/tollgateconfigs/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/99-first-login $(1)/etc/init.d/

	$(INSTALL_DIR) $(1)/lib/preinit
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/80_mount_root $(1)/lib/preinit/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/update_wireless_config.sh $(1)/lib/preinit/
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./files/* $(PKG_BUILD_DIR)/
endef

$(eval $(call BuildPackage,tollgateconfigs))
