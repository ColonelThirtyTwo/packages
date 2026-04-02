include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/nls.mk

PKG_NAME:=blocky
PKG_VERSION:=0.30.0
PKG_RELEASE:=1

PKG_SOURCE:=v$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/0xERR0R/blocky/tar.gz/refs/tags/v$(PKG_VERSION)?
PKG_HASH:=bcb8671d54581374ce1683492fd5722e0f0c3361d10c9d32ded10ea5e40f6443

PKG_MAINTAINER:=Alex Parrill <alex@col32.net>
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE
PKG_CPE_ID:=cpe:/a:blocky:blocky

PKG_BUILD_DEPENDS=golang/host
PKG_BUILD_PARALLEL:=1
PKG_BUILD_FLAGS:=no-mips16

GO_PKG:=github.com/0xERR0R/blocky
GO_PKG_BUILD_PKG:=github.com/0xERR0R/blocky
GO_PKG_LDFLAGS:=-X github.com/0xERR0R/blocky/util.Version=${PKG_VERSION}

include $(INCLUDE_DIR)/package.mk
include ../../lang/golang/golang-package.mk

define Package/blocky
	SECTION:=net
	CATEGORY:=Network
	TITLE:=DNS proxy and ad blocker
	URL:=https://0xerr0r.github.io/blocky/latest/
	DEPENDS:=$(GO_ARCH_DEPENDS) +ca-bundle
	USERID:=blocky:blocky
endef

define Package/blocky/conffiles
/etc/blocky.yaml
endef

define Package/blocky/description
Fast and lightweight DNS proxy as ad-blocker for local network with many features
endef

define Package/blocky/install
	$(call GoPackage/Package/Install/Bin,$(1))
	
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/blocky.init $(1)/etc/init.d/blocky

	$(INSTALL_DIR) $(1)/etc/
	$(INSTALL_CONF) ./files/blocky.yaml $(1)/etc/blocky.yaml

	$(INSTALL_DIR) $(1)/etc/capabilities
	$(INSTALL_CONF) ./files/capabilities.json $(1)/etc/capabilities/blocky.json
endef

$(eval $(call GoBinPackage,blocky))
$(eval $(call BuildPackage,blocky))
