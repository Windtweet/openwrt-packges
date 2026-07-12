# rtl88x2eu_openwrt

rtl88x2eu_openwrt 是一个用于 OpenWrt 系统的驱动程序，适用于 Realtek RTL88x2EU 芯片组的无线网卡。该驱动程序提供了对 802.11a/b/g/n/ac 协议的支持，并实现了无线网络的连接、配置和管理功能。

## 功能特性

- 支持 802.11a/b/g/n/ac 协议
- 支持基础设施模式（Infrastructure Mode）和自组网模式（Ad-Hoc Mode）
- 支持 WPA/WPA2 安全协议
- 支持多频段（2.4GHz 和 5GHz）和多天线配置（MIMO）
- 支持无线网络扫描、连接和断开操作
- 支持无线网络接口的配置和管理

## 安装方法

1. 下载 OpenWrt SDK 并解压。
2. 将本仓库克隆到 `package` 目录下。
3. 运行 `make menuconfig`，选择 `Network` -> `Wireless` -> `rtl88x2eu`。
4. 保存配置并运行 `make package/rtl88x2eu/compile` 编译驱动。
5. 编译完成后，将生成的 `.ipk` 文件上传到 OpenWrt 设备并安装。

## 使用方法

1. 插入 RTL88x2EU 芯片的无线网卡。
2. 运行 `ifconfig` 或 `ip link` 查看无线网络接口是否识别成功。
3. 使用 `iw` 或 `wpa_supplicant` 配置无线网络连接。
4. 使用 `udhcpc` 或 `dhclient` 获取 IP 地址。

## 依赖项

- OpenWrt SDK
- Realtek RTL88x2EU 芯片的无线网卡
- Linux 内核头文件

## 注意事项

- 本驱动程序仅适用于 OpenWrt 系统。
- 驱动程序的性能和稳定性可能因硬件和固件版本而异。
- 如果遇到兼容性问题，请参考 Realtek 官方文档或联系技术支持。

## 开源许可

本项目采用 MIT 许可证。详情请查看 [LICENSE](LICENSE) 文件。

## 贡献者

感谢所有为本项目做出贡献的开发者和支持者。

## 联系方式

如有任何问题或建议，请提交 issue 或联系项目维护者。