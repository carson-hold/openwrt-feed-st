#
# Copyright (C) 2024 Bootlin
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_VERSION:=2023.10-stm32mp-r1-bp
#PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://e.coding.net/holdiot/openwrt-stm32mp/u-boot-2023.10-stm32mp-r1.git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_MIRROR_HASH:=skip

UBOOT_USE_INTREE_DTC:=1

include $(INCLUDE_DIR)/u-boot.mk
include $(INCLUDE_DIR)/package.mk

define U-Boot/Default
  BUILD_TARGET:=stm32
  UBOOT_IMAGE:=u-boot.bin u-boot.dtb
endef

define U-Boot/stm32mp15
  BUILD_SUBTARGET:=stm32mp1
  UBOOT_CONFIG:=stm32mp15
endef

define U-Boot/stm32mp13
  BUILD_SUBTARGET:=stm32mp1
  UBOOT_CONFIG:=stm32mp13
endef

define U-Boot/stm32mp25
  BUILD_SUBTARGET:=stm32mp2
  UBOOT_CONFIG:=stm32mp25
endef

define U-Boot/stm32mp157f-dk2
  $(call U-Boot/stm32mp15)
  NAME:=STM32MP157F-DK2
  DEVICE_TREE:=stm32mp157f-dk2
endef

define U-Boot/stm32mp135f-dk
  $(call U-Boot/stm32mp13)
  NAME:=STM32MP135F-DK
  DEVICE_TREE:=stm32mp135f-dk
endef

define U-Boot/bp-stm32mp135d-256m
  $(call U-Boot/stm32mp13)
  NAME:=BP-STM32MP135D-256M
  DEVICE_TREE:=bp-stm32mp135d-256m
  UBOOT_CONFIG:=bp-stm32mp135d-256m
endef

define U-Boot/stm32mp257f-ev1
  $(call U-Boot/stm32mp25)
  NAME:=STM32MP257F-EV1
  DEVICE_TREE:=stm32mp257f-ev1
endef

define U-Boot/stm32mp257f-dk
  $(call U-Boot/stm32mp25)
  NAME:=STM32MP257F-DK
  DEVICE_TREE:=stm32mp257f-dk
endef

UBOOT_TARGETS := \
	stm32mp157f-dk2 \
	stm32mp135f-dk \
  bp-stm32mp135d-256m \
	stm32mp257f-ev1 \
	stm32mp257f-dk

UBOOT_MAKE_FLAGS += DEVICE_TREE=$(DEVICE_TREE)

define Build/InstallDev
	$(INSTALL_DIR) $(STAGING_DIR_IMAGE)
	$(foreach img,$(UBOOT_IMAGE), \
		$(CP) $(PKG_BUILD_DIR)/$(img) $(STAGING_DIR_IMAGE)/$(BUILD_VARIANT)-$(img); \
	)
endef

define Package/u-boot/install/default
endef

$(eval $(call BuildPackage/U-Boot))
