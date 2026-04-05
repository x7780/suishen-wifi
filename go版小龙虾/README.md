# PicoClaw 小龙虾 - 轻量级个人 AI 助手

## 项目介绍

[PicoClaw](https://github.com/sipeed/picoclaw) 是由 Sipeed（知名开源硬件厂商）开发的轻量级个人 AI 助手，使用 Go 语言编写，主打"小而快、随处部署"的设计理念。

PicoClaw 具有以下特点：
- **轻量级**：可运行在仅 10 MB 内存的设备上
- **高性能**：Go 语言编写，响应速度快
- **易于部署**：支持多种平台，包括资源有限的设备
- **功能丰富**：提供多种 AI 辅助功能
- **开源免费**：完全开源，可自由使用和修改

**重要说明**：通过提供的购买链接购买的设备已经集成了 PicoClaw 小龙虾，用户不需要再手动安装。本指南主要用于参考和了解 AI 助手的配置与使用方法。

## 系统要求

- **CPU**: 高通骁龙 410 (4核1.2GHz) 或更高
- **内存**: 至少 512MB 可用内存
- **存储**: 至少 100MB 可用空间
- **网络**: 稳定的网络连接（用于更新和在线功能）
- **操作系统**: OpenWrt
- **设备购买地址** (闲鱼): [https://m.tb.cn/h.ikewKeE?tk=sY5z5265Lof%20CZ007](https://m.tb.cn/h.ikewKeE?tk=sY5z5265Lof%20CZ007)

## 设备说明

通过提供的购买链接购买的设备已经预装了 PicoClaw 小龙虾，并且已经完成了以下配置：

- 系统已刷入 OpenWrt
- PicoClaw 已安装在 `/root/picoclaw` 目录
- 服务已配置为开机自启
- 基本设置已完成

## 手动安装步骤（仅供参考）

如果你需要重新安装或升级 PicoClaw，可以按照以下步骤操作：

### 1. 准备工作

确保你的设备已经刷入了OpenWrt系统，并且可以通过SSH登录。

**注意**：OpenWrt系统可能需要安装一些必要的软件包，如 `wget`、`tar` 和 `nano` 等。

### 2. 创建安装目录

```bash
# 创建安装目录
mkdir -p /root/picoclaw
cd /root/picoclaw
```

### 3. 下载 PicoClaw

请访问 [PicoClaw GitHub 仓库](https://picoclaw.io/) 下载适合你设备架构的版本：

1. 打开浏览器，访问 https://picoclaw.io/
2. 下载适合你设备架构的最新版本
3. 将下载的文件上传到设备的 `/root/picoclaw` 目录

### 4. 解压文件

```bash
# 假设下载的文件名为 picoclaw-arm.tar.gz
tar -xzf picoclaw_Linux_arm64.tar.gz
```

### 5. 首次运行

```bash
# 赋予执行权限
chmod +x picoclaw

# 首次运行（会生成配置文件）
./picoclaw-launcher -public
```

首次运行会生成必要的配置文件，然后自动退出。

### 6. 访问 PicoClaw

在浏览器中访问：
- 地址: `http://你的设备IP:18800`
- 端口: 18800（或你在配置文件中设置的端口）

## 功能特性

PicoClaw 提供以下主要功能：

1. **对话助手**：提供智能对话服务
2. **信息查询**：查询天气、新闻等信息
3. **任务管理**：帮助管理待办事项
4. **智能家居控制**：控制智能设备（需要相应硬件支持）
5. **自定义技能**：支持添加自定义技能和功能

## 自动启动设置（仅供参考）

通过购买链接购买的设备已经配置了服务自启功能。如果你需要重新配置或修改启动脚本，可以按照以下步骤操作：

```bash
OpenWrt 添加到启动项里面
# 1. 启动 Picoclaw（修正版，后台运行+输出日志）
cd /root/picoclaw && ./picoclaw-launcher -public > /tmp/picoclaw.log 2>&1 &

## 故障排除

1. **启动失败**：
   - 检查端口是否被占用
   - 查看 `picoclaw.log` 文件了解具体错误
   - 确保文件权限正确

2. **连接超时**：
   - 检查防火墙设置，确保端口开放
   - 确认网络连接正常
   - 检查服务是否正在运行

3. **功能异常**：
   - 检查 API 密钥配置
   - 确认网络连接正常
   - 查看日志文件了解具体错误

## 总结

PicoClaw 小龙虾是一个轻量级的个人 AI 助手，非常适合在资源有限的设备上运行，如高通410随身WiFi设备。通过合理的配置，可以获得流畅的 AI 辅助体验。

## 参考链接

- [PicoClaw GitHub 仓库](https://github.com/sipeed/picoclaw)
- [Sipeed 官方网站](https://www.sipeed.com/)
- [OpenWrt 官方网站](https://openwrt.org/)