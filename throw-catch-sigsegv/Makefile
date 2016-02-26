include $(TOPDIR)/rules.mk

PKG_NAME:=throw-catch-sigsegv
PKG_VERSION:=2016-02-25
PKG_RELEASE:=$(PKG_SOURCE_VERSION)

## local files setup
# PKG_SOURCE_URL:=file:///home/user/Documents/openwrt-test/openwrt-test
# PKG_SOURCE_SUBDIR:=$(PKG_NAME)

## repository-based setup
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://github.com/coolspot/openwrt-test.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
#PKG_SOURCE_VERSION:=62e2debda87fd70229a09f8df3730c368cf778af
PKG_SOURCE_VERSION:=HEAD


PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
CMAKE_INSTALL:=1

PKG_MAINTAINER:=Ivan Kold <openwrt@coolspot.33mail.com>

include $(INCLUDE_DIR)/uclibc++.mk
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Build/Prepare
	echo pkg_build_dir=$(PKG_BUILD_DIR)
	$(call Build/Prepare/Default)
## comment 3 following lines for local-file-based setup
	$(CP) $(PKG_BUILD_DIR)/throw-catch-sigsegv $(PKG_BUILD_DIR)-tmp
	rm -r $(PKG_BUILD_DIR)
	mv $(PKG_BUILD_DIR)-tmp $(PKG_BUILD_DIR)
	echo Downloaded.
endef

define Package/throw-catch-sigsegv
	SECTION:=test
	CATEGORY:=Test
	SUBMENU:=test-sub
	TITLE:=Test case for simple try-catch.
	DEPENDS:= $(CXX_DEPENDS)
	URL:=http://www.pixus.ru/
	MAINTAINER:=Ivan Kold <openwrt@coolspot.33mail.com>
endef

define Package/throw-catch-sigsegv/description
	The binary throw-catch-sigsegv does throw std::runtime_error inside try-catch.
	That causes SIGSEGV on the musl-uclibc++ OpenWRT build due incorrect implementation of C++ exception ABI in uClibc++ .
endef


define Package/throw-catch-sigsegv/install
	# main binary
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/throw-catch-sigsegv $(1)/usr/bin/
endef

$(eval $(call BuildPackage,throw-catch-sigsegv))
