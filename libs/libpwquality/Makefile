include $(TOPDIR)/rules.mk

PKG_NAME:=libpwquality
PKG_VERSION:=1.4.5
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/libpwquality/libpwquality.git
PKG_SOURCE_VERSION:=libpwquality-$(PKG_VERSION)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(libpwquality).tar.gz
PKG_MIRROR_HASH:=skip

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING

PKG_FIXUP:=autoreconf
PKG_INSTALL:=0

include $(INCLUDE_DIR)/package.mk

define Package/libpwquality
	SECTION:=libs
	CATEGORY:=Libraries
	TITLE:=PAM module for password quality checking
	URL:=https://github.com/libpwquality/libpwquality
	DEPENDS:=+libpam +cracklib
endef

define Package/libpwquality/description
	libpwquality is a PAM module that can be used to enforce password quality policies.
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	(cd $(PKG_BUILD_DIR); ./autogen.sh)
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); \
		./configure \
		--host=$(CONFIGURE_TARGET) \
		--prefix=/usr \
		--disable-static \
		--enable-shared \
	)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)
endef

define Package/libpwquality/install
	$(INSTALL_DIR) $(1)/usr/lib/security
	$(CP) $(PKG_BUILD_DIR)/src/.libs/libpwquality.so $(1)/usr/lib/security/

	$(INSTALL_DIR) $(1)/usr/share/libpwquality
	$(CP) $(PKG_BUILD_DIR)/pwquality.conf $(1)/usr/share/libpwquality/
endef

$(eval $(call BuildPackage,libpwquality))
