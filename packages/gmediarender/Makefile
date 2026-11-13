
include $(TOPDIR)/rules.mk

PKG_NAME:=gmediarender
PKG_VERSION:=2020-01-10
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/hzeller/gmrender-resurrect.git
PKG_SOURCE_VERSION:=26d8f7edf5336bc30f7334c6ad459bf7f4f90ff2

PKG_LICENSE:=GPL-2.0

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

PKG_REMOVE_FILES:=aclocal.m4

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/$(PKG_NAME)
  SECTION:=multimedia
  CATEGORY:=Multimedia
  DEPENDS:=+glib2 +libupnp +gst1-libav
  TITLE:=Headless UPnP Renderer
endef

define Package/$(PKG_NAME)/description
  Resource efficient UPnP/DLNA renderer for embedded devices.
  Based on the gmrender-resurrect project.
endef

CONFIGURE_ARGS+= \
  --with-build-cc="$(HOSTCC)" \
  --prefix=/usr

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/$(PKG_NAME) $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/gmediarender.init $(1)/etc/init.d/gmediarender

	$(INSTALL_DIR) $(1)/usr/share/$(PKG_NAME)
	$(CP) $(PKG_BUILD_DIR)/data/*.png $(1)/usr/share/$(PKG_NAME)/

	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/set-gmediarender-enabled.sh $(1)/etc/uci-defaults/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))

