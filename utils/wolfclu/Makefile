#
# Copyright (C) 2024 Your Name <your.email@example.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=wolfclu
PKG_VERSION:=0.1.8
PKG_REAL_VERSION:=$(PKG_VERSION)-stable
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_REAL_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/wolfSSL/wolfCLU/archive/v$(PKG_REAL_VERSION)
PKG_HASH:=15a6e2c271616fc0d69137d411a29ae8511546549ad0b7f6b64b110b82904a4b

PKG_BUILD_DIR:=$(BUILD_DIR)/wolfCLU-$(PKG_REAL_VERSION)

PKG_MAINTAINER:=Your Name <your.email@example.com>
PKG_LICENSE:=GPL-2.0-or-later

include $(INCLUDE_DIR)/package.mk

define Package/wolfclu
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=wolfCLU (WolfCrypt Command Line Utility)
  URL:=https://github.com/wolfSSL/wolfCLU
  DEPENDS:=+libwolfssl
endef

define Package/wolfclu/description
  wolfCLU provides command-line utilities for wolfCrypt, including
  crypttest for cryptographic algorithm testing and benchmark for
  performance measurement.
endef

CONFIGURE_ARGS += \
	--host=$(ARCH)-linux \
	--with-wolfssl=$(STAGING_DIR)/usr \
	--enable-debug

TARGET_LDFLAGS += -lwolfssl

define Build/Configure
	(cd $(PKG_BUILD_DIR); ./autogen.sh );
	$(call Build/Configure/Default)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		all
endef

define Package/wolfclu/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/wolfssl $(1)/usr/bin/
endef

$(eval $(call BuildPackage,wolfclu))
