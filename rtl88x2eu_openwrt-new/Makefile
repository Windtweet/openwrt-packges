include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=rtl88x2eu-windtweet
# 重点1：版本号需与驱动实际版本一致
PKG_VERSION:=5.15.182_30362
PKG_RELEASE:=1

# 重点2：包的基本信息
PKG_LICENSE:=GPLv2
PKG_MAINTAINER:=Your Name <your@email.com>

# 重点3：指定源码位置（使用本地src目录）
#PKG_SOURCE_PROTO:=local
#PKG_SOURCE_URL:=./src
PKG_SOURCE_DATE:=2025-11-12

# 重点4：构建目录设置
PKG_BUILD_DIR:=$(KERNEL_BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

# 重点5：内核模块包定义
define KernelPackage/rtl88x2eu
  SUBMENU:=Wireless Drivers
  TITLE:=Realtek RTL88X2EU Wireless Driver Windtweet
  # 重点6：依赖关系
  DEPENDS:=+kmod-cfg80211 +kmod-usb-core +@DRIVER_11N_SUPPORT +@DRIVER_11AC_SUPPORT
  # 重点7：指定生成的模块文件路径
  FILES:=$(PKG_BUILD_DIR)/8812eu.ko
  AUTOLOAD:=$(call AutoProbe,8812eu)
  PROVIDES:=kmod-rtl88x2eu
endef

# 重点8：模块描述
define KernelPackage/rtl88x2eu/description
  Kernel module for Realtek RTL8812EU/RTL8822EU USB wireless adapters.
  This driver supports the 88x2eu chipset.
endef

# 重点9：准备源码（从本地src目录复制）
define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) -r ./src/* $(PKG_BUILD_DIR)/
	# 可选：修复可能的Makefile规则冲突
	-(cd $(PKG_BUILD_DIR) && \
	 find . -name "Makefile" -o -name "*.mk" | xargs sed -i 's/^\([a-zA-Z0-9_-]*\)::/\1:/g')
endef

# 重点10：配置编译环境
NOSTDINC_FLAGS = \
	-I$(PKG_BUILD_DIR) \
	-I$(PKG_BUILD_DIR)/include \
	-I$(STAGING_DIR)/usr/include/mac80211-backport \
	-I$(STAGING_DIR)/usr/include/mac80211-backport/uapi \
	-I$(STAGING_DIR)/usr/include/mac80211 \
	-I$(STAGING_DIR)/usr/include/mac80211/uapi \
	-include backport/backport.h

# 重点11：添加OpenWrt特定标志
NOSTDINC_FLAGS+=-DCONFIG_IOCTL_CFG80211 -DRTW_USE_CFG80211_STA_EVENT -DCONFIG_ACK_5_15_LTS_KERNEL -DBUILD_OPENWRT

# 重点12：编译指令（使用驱动源码的Makefile）
define Build/Compile
	# 重点13：使用OpenWrt内核头文件，但驱动自身的构建系统
	+$(MAKE) $(PKG_JOBS) -C "$(LINUX_DIR)" \
		$(KERNEL_MAKE_FLAGS) \
		M="$(PKG_BUILD_DIR)" \
		ARCH="$(LINUX_KARCH)" \
		CROSS_COMPILE="$(TARGET_CROSS)" \
		NOSTDINC_FLAGS="$(NOSTDINC_FLAGS)" \
		CONFIG_RTL8822E=y \
		CONFIG_USB_HCI=y \
		modules
endef

# 重点14：评估生成包
$(eval $(call KernelPackage,rtl88x2eu))
