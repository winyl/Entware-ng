#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libnftnl
PKG_VERSION:=1.1.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://netfilter.org/projects/$(PKG_NAME)/files
PKG_HASH:=a5c7b7a6c13c9c5898b13fcb1126fefce2015d5a96d7c354b19aaa40b6aece5d
PKG_MAINTAINER:=Steven Barth <steven@midlink.org>
PKG_LICENSE:=GPL-2.0+

PKG_FIXUP:=autoreconf

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

DISABLE_NLS:=

define Package/libnftnl
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libmnl
  TITLE:=Low-level netlink library for the nf_tables subsystem
  URL:=http://www.netfilter.org/projects/libnftnl
  ABI_VERSION:=7
endef

define Package/libnftnl/description
 libnftnl is a userspace library providing a low-level netlink
 programming interface (API) to the in-kernel nf_tables subsystem.
endef

TARGET_CFLAGS += $(FPIC)

CONFIGURE_ARGS += \
	--enable-static \
	--enable-shared \
	--without-json-parsing

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include/libnftnl
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/include/libnftnl/*.h \
		$(1)/opt/include/libnftnl/

	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/libnftnl.{so*,a,la} \
		$(1)/opt/lib/

	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/pkgconfig/libnftnl.pc \
		$(1)/opt/lib/pkgconfig/
endef

define Package/libnftnl/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/libnftnl.so.* \
		$(1)/opt/lib/
endef

$(eval $(call BuildPackage,libnftnl))
