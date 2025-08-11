#
# Copyright (C) 2024 Your Name <your.email@example.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=wolfssh
PKG_VERSION:=1.4.20
PKG_REAL_VERSION:=$(PKG_VERSION)-stable
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_REAL_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/wolfSSL/wolfssh/archive/v$(PKG_REAL_VERSION)
PKG_HASH:=c7007eb60f69b372afaf9a3e84ce723da2e3331f84ee9430f2a01472c8465ad8

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_REAL_VERSION)

PKG_MAINTAINER:=Your Name <your.email@example.com>
PKG_LICENSE:=GPL-2.0-or-later

include $(INCLUDE_DIR)/package.mk

define Package/wolfssh
  SECTION:=net
  CATEGORY:=Network
  TITLE:=WolfSSH lightweight SSHv2 library
  URL:=https://www.wolfssl.com/products/wolfssh/
  DEPENDS:=+libwolfssl
endef

define Package/wolfssh/description
  WolfSSH is a lightweight, C-language based, SSHv2 library targeted for
  embedded, RTOS, and resource-constrained environments. It is designed
  for speed, size, and portability.
endef

CONFIGURE_ARGS += \
	--host=$(ARCH)-linux \
	--disable-shared \
	--enable-static \
	--enable-examples \
	--with-wolfssl=$(STAGING_DIR)/usr \
	--enable-smallstack \
	--enable-debug \
	--enable-all

define Build/Configure
	(cd $(PKG_BUILD_DIR); ./autogen.sh );
	$(call Build/Configure/Default)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		all
endef

define Package/wolfssh/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/src/.libs/*.a $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/include/wolfssh
	$(CP) $(PKG_BUILD_DIR)/wolfssh/*.h $(1)/usr/include/wolfssh/
endef

$(eval $(call BuildPackage,wolfssh))
