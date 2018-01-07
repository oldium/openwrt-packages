#
# sniproxy - Makefile for SNIProxy
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=sniproxy
PKG_VERSION:=0.6.0-git-20190124
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://github.com/dlundquist/sniproxy.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=822bb80df9b7b345cc9eba55df74a07b498819ba
PKG_LICENSE:=BSD-2-Clause
PKG_SOURCE:=$(PKG_NAME)-$(PKG_SOURCE_VERSION).tar.bz2
PKG_MIRROR_HASH:=d58a46d636621c3d9711618d50dfa4cf0fa2161aeae5885de393c86cefce4113
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_SOURCE_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_SOURCE_VERSION)

PKG_FIXUP:=autoreconf
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

# No NLS support for this package
DISABLE_NLS:=

define Package/sniproxy
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Web Servers/Proxies
	TITLE:=Proxies incoming HTTP and TLS connections
	URL:=https://github.com/dlundquist/sniproxy
	MAINTAINER:=Oldrich Jedlicka <oldium.pro@gmail.com>
	DEPENDS:=+libev +libpcre +SNIPROXY_WITH_UDNS:libudns
endef

define Package/sniproxy/description
	Proxies incoming HTTP and TLS connections based on the hostname \
	contained in the initial request of the TCP session.
endef

define Package/sniproxy/config
	source "$(SOURCE)/Config.in"
endef

define Package/sniproxy/install
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/sniproxy$(if $(CONFIG_SNIPROXY_WITH_UDNS),,-nodns) $(1)/etc/config/sniproxy
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/sniproxy.conf $(1)/etc/sniproxy.conf
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/sniproxy $(1)/usr/sbin
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/sniproxy.init $(1)/etc/init.d/sniproxy
endef

define Package/sniproxy/conffiles
/etc/sniproxy.conf
/etc/config/sniproxy
endef

CONFIGURE_ARGS += \
	$(if $(CONFIG_SNIPROXY_WITH_UDNS),,--disable-dns)

$(eval $(call BuildPackage,sniproxy))
