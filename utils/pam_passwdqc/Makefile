include $(TOPDIR)/rules.mk

PKG_NAME:=pam_passwdqc
PKG_VERSION:=1.0.5
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://www.openwall.com/passwdqc/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_HASH:=32528ddf7d8219c788b6e7702361611ff16c6340b6dc0f418ff164aadc4a4a88
PKG_SOURCE_URL=https://www.openwall.com/pam/modules/pam_passwdqc/

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/pam_passwdqc
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=passwdqc strength checking and enforcement
	URL:=https://www.openwall.com/passwdqc/
	DEPENDS:=+libpam
endef

define Package/pam_passwdqc/description
	pam_passwdqc is a password strength checking and policy enforcement toolset.
endef

define Build/Compile
	$(TARGET_CC) $(TARGET_CFLAGS) -I$(STAGING_DIR)/usr/include -fPIC -c \
		-o $(PKG_BUILD_DIR)/pam_passwdqc.o $(PKG_BUILD_DIR)/pam_passwdqc.c
	$(TARGET_CC) $(TARGET_CFLAGS) -I$(STAGING_DIR)/usr/include -fPIC -c \
		-o $(PKG_BUILD_DIR)/passwdqc_check.o $(PKG_BUILD_DIR)/passwdqc_check.c
	$(TARGET_CC) $(TARGET_CFLAGS) -I$(STAGING_DIR)/usr/include -fPIC -c \
		-o $(PKG_BUILD_DIR)/passwdqc_random.o $(PKG_BUILD_DIR)/passwdqc_random.c
	$(TARGET_CC) $(TARGET_CFLAGS) -I$(STAGING_DIR)/usr/include -fPIC -c \
		-o $(PKG_BUILD_DIR)/wordset_4k.o $(PKG_BUILD_DIR)/wordset_4k.c

	$(TARGET_CC) $(TARGET_LDFLAGS) -shared \
		-o $(PKG_BUILD_DIR)/pam_passwdqc.so \
		$(PKG_BUILD_DIR)/pam_passwdqc.o \
		$(PKG_BUILD_DIR)/passwdqc_check.o \
		$(PKG_BUILD_DIR)/passwdqc_random.o \
		$(PKG_BUILD_DIR)/wordset_4k.o \
		-L$(STAGING_DIR)/usr/lib -lpam
endef


define Package/pam_passwdqc/install
	$(INSTALL_DIR) $(1)/usr/lib/security
	$(CP) $(PKG_BUILD_DIR)/pam_passwdqc.so $(1)/usr/lib/security/
endef

$(eval $(call BuildPackage,pam_passwdqc))