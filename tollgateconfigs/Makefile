include $(TOPDIR)/rules.mk

PKG_NAME:=tollgateconfigs
PKG_VERSION:=1.0
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=base
	CATEGORY:=Base system
	TITLE:=Custom files and scripts
endef

define Package/$(PKG_NAME)/description
	Custom files and scripts for the system.
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/install
	$(CP) ./files/* $(1)/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
