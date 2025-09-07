include $(TOPDIR)/rules.mk

PKG_NAME:=libnss-ldapd
PKG_VERSION:=0.9.13
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/libnss-ldapd/nss-pam-ldapd-$(PKG_VERSION)
PKG_SOURCE:=nss-pam-ldapd-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://arthurdejong.org/nss-pam-ldapd/
PKG_HASH:=e01784e17cb533bb66bd0601e205e785263445c3c2df7a6f90232ab4131c716d
PKG_INSTALL:=1
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/libnss-ldapd
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=NSS module for using LDAP as a naming service
  DEPENDS:=+libpam +libopenldap @USE_GLIBC
  URL:=https://arthurdejong.org/nss-pam-ldapd/
endef

define Package/libnss-ldapd/description
 This package provides a Name Service Switch module that allows using an LDAP server
 to provide user account, group, host name, alias, netgroup, and basically any other
 information that would normally be retrieved from /etc flat files or NIS.
endef

define Package/libnss-ldapd/conffiles
/etc/nslcd.conf
endef

define Build/Configure
	$(call Build/Configure/Default, \
		--with-linux-headers=$(LINUX_DIR) \
		--disable-utils \
	)
endef

define Package/libnss-ldapd/install
	$(INSTALL_DIR) $(1)/usr $(1)/usr/lib $(1)/usr/sbin $(1)/usr/lib/security
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/lib/security/pam_ldap.so $(1)/usr/lib/security/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/libnss_ldap.so.2 $(1)/usr/lib/libnss_ldap.so.2
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/nslcd $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,libnss-ldapd))
