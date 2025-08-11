include $(TOPDIR)/rules.mk

PKG_NAME:=caam-test
PKG_VERSION:=1.0
PKG_RELEASE:=1
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/caam-test
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=NXP caam-test user-space tool
	DEPENDS:=+libopenssl
endef

define Package/caam-test/description
	User-space tool for testing NXP CAAM crypto performance.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
	CC="$(TARGET_CC)"  -I$(STAGING_DIR)/usr/include \
	CFLAGS="$(TARGET_CFLAGS) -Wall -Werror" \
	LFLAGS="-lcrypto"
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Package/caam-test/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/caam-crypt $(1)/usr/bin/
endef

$(eval $(call BuildPackage,caam-test))
