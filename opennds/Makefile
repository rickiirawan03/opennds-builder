include $(TOPDIR)/rules.mk

PKG_NAME:=opennds
PKG_VERSION:=10.3.0
PKG_RELEASE:=r1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/openNDS/openNDS.git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz

PKG_MAINTAINER:=openNDS Maintainers <opennds@lists.infradead.org>
PKG_LICENSE:=GPL-2.0

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/opennds
  SECTION:=net
  CATEGORY:=Network
  TITLE:=openNDS - Open Network Device Server (Captive Portal)
  DEPENDS:=+libubus +libuci +libnl-tiny +kmod-tun +libmicrohttpd-no-ssl +libjson-c +libip4tc +freeradius3
  MAINTAINER:=openNDS Developers <opennds@lists.infradead.org>
endef

define Package/opennds/description
  openNDS is a Captive Portal with RADIUS support and UCI config.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS)" \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all install
endef

define Package/opennds/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/opennds $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/opennds.init $(1)/etc/init.d/opennds
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/files/opennds.config $(1)/etc/config/opennds
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/etc/uci-defaults/99-opennds-default $(1)/etc/uci-defaults/
endef

$(eval $(call BuildPackage,opennds))
