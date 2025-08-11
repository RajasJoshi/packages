include $(TOPDIR)/rules.mk

PKG_NAME:=caam-keygen
PKG_VERSION:=1.0
PKG_RELEASE:=1
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/caam-keygen
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=NXP CAAM key generation tool
	DEPENDS:=+libopenssl
endef

define Package/caam-keygen/description
	User-space tool for generating keys using NXP CAAM.
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	$(TARGET_CC) $(TARGET_CFLAGS) -O2 -Wall \
	-I$(STAGING_DIR)/usr/include \
	-o $(PKG_BUILD_DIR)/caam-keygen \
	$(PKG_BUILD_DIR)/caam-keygen.c \
	-lcrypto
endef


define Package/caam-keygen/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/caam-keygen $(1)/usr/bin/
endef

$(eval $(call BuildPackage,caam-keygen))
 