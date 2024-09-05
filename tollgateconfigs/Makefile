include $(TOPDIR)/rules.mk

PKG_NAME:=tollgateconfigs
PKG_VERSION:=1.0
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=base
  CATEGORY:=Base system
  TITLE:=TollGate custom configurations
  DEPENDS:=
endef

define Package/$(PKG_NAME)/description
  Custom configurations and scripts for TollGate system.
endef

define Build/Compile
	# No compilation needed
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/99-first-login $(1)/etc/init.d/

	$(INSTALL_DIR) $(1)/lib/preinit
	$(INSTALL_BIN) ./files/80_mount_root $(1)/lib/preinit/
	$(INSTALL_BIN) ./files/update_wireless_config.sh $(1)/lib/preinit/

	$(INSTALL_DIR) $(1)/etc/rc.d
	ln -s ../init.d/99-first-login $(1)/etc/rc.d/S99first-login
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./files/* $(PKG_BUILD_DIR)/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
