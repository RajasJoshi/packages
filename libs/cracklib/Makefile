include $(TOPDIR)/rules.mk

PKG_NAME:=cracklib
PKG_VERSION:=2.10.3
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/cracklib/cracklib.git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_MIRROR_HASH:=dfb9da76ac73db54fdd99142baede677680aa52879dfa4a8313ca96f11730095

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_LICENSE:=LGPL-2.1
PKG_LICENSE_FILES:=COPYING.LIB

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/cracklib
	SECTION:=libs
	CATEGORY:=Libraries
	TITLE:=CrackLib - Password Checking Library
	URL:=https://github.com/cracklib/cracklib
	DEPENDS:=+libc +zlib
endef

define Package/cracklib/description
	CrackLib is a library used to enforce strong passwords by checking them against dictionary words and other heuristics.
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	(cd $(PKG_BUILD_DIR)/src; ./autogen.sh)
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR)/src; \
		./configure \
		--host=$(CONFIGURE_TARGET) \
		--prefix=/usr \
		--disable-static \
		--enable-shared \
	)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/src
endef


define Build/InstallDev
    # Install headers
    $(INSTALL_DIR) $(1)/usr/include
    $(CP) $(PKG_BUILD_DIR)/src/lib/crack.h $(1)/usr/include/

    # Install shared library symlink and .so
    $(INSTALL_DIR) $(1)/usr/lib
    $(CP) $(PKG_BUILD_DIR)/src/lib/.libs/libcrack.so* $(1)/usr/lib/

    # Create symlink for linking
    ln -sf libcrack.so.$(PKG_VERSION) $(1)/usr/lib/libcrack.so
endef

define Package/cracklib/install
	# Install shared library
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/src/lib/.libs/libcrack.so* $(1)/usr/lib/

	# Install utility binaries
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/util/cracklib-check $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/util/cracklib-format $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/util/create-cracklib-dict $(1)/usr/bin/

	# Optionally install headers
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_BUILD_DIR)/src/lib/*.h $(1)/usr/include/
endef

$(eval $(call BuildPackage,cracklib))
