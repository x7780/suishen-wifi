# Cuberite 服务端安装指南 (高通410随身WiFi)

## 项目介绍

[Cuberite](https://cuberite.org/) 是一个高性能的 Minecraft 服务端实现，使用 C++ 编写，相比官方服务端具有更低的资源占用和更快的响应速度，非常适合在资源有限的设备上运行，如高通410随身WiFi设备。

## 支持版本

- Minecraft Java 版: 1.8 - 1.12
- 客户端版本兼容性良好，支持大多数现代客户端
- 注意：Minecraft Java Edition 1.13+ 支持正在开发中

## 系统要求

- **CPU**: 高通骁龙 410 (4核1.2GHz)
- **内存**: 至少 512MB 可用内存
- **存储**: 4GB (实际可用空间)
- **网络**: 稳定的网络连接
- **操作系统**: OpenWrt
- **设备购买地址** (闲鱼): [https://m.tb.cn/h.ikewKeE?tk=sY5z5265Lof%20CZ007](https://m.tb.cn/h.ikewKeE?tk=sY5z5265Lof%20CZ007)

## 安装步骤

### 1. 准备工作

确保你的高通410随身WiFi设备已经刷入了OpenWrt系统，并且可以通过SSH登录。

**注意**：OpenWrt系统可能需要安装一些必要的软件包，如 `wget`、`tar` 和 `nano` 等。

### 2. 创建安装目录

```bash
# 创建服务端目录
mkdir -p /root/cuberite
cd /root/cuberite
```

### 3. 下载 Cuberite

根据你的系统架构选择合适的版本：

```bash
# 对于 32位 ARM 系统 (高通410通常是32位)
wget https://builds.cuberite.org/job/linux-armhf/lastSuccessfulBuild/artifact/Cuberite.tar.gz

# 对于 64位 ARM 系统
# wget https://builds.cuberite.org/job/linux-aarch64/lastSuccessfulBuild/artifact/Cuberite.tar.gz
```

### 4. 解压文件

```bash
tar -xzf Cuberite.tar.gz
```

### 5. 首次运行

```bash
# 赋予执行权限
chmod +x Cuberite

# 首次运行（会生成配置文件）
./Cuberite
```

首次运行会生成必要的配置文件，然后自动退出。

### 6. 配置服务端

编辑 `server.properties` 文件进行基本配置：

```bash
nano server.properties
```

主要配置项：
- `server-name`: 服务器名称
- `gamemode`: 游戏模式 (survival/creative/adventure)
- `difficulty`: 难度 (peaceful/easy/normal/hard)
- `max-players`: 最大玩家数 (建议 1-3，受限于设备硬件)
- `server-port`: 服务器端口 (默认 25565)

### 7. 启动服务端

```bash
# 前台运行
./Cuberite

# 后台运行 (推荐)
nohup ./Cuberite > server.log 2>&1 &
```

### 8. 连接服务器

在 Minecraft 客户端中添加服务器：
- 服务器地址: 你的随身WiFi IP地址
- 端口: 25565 (或你在配置文件中设置的端口)

## 优化配置

由于高通410资源有限，建议进行以下优化：

1. **内存优化**：编辑 `Cuberite.ini` 文件
   ```ini
   [Server]
   MaxChunkCacheSize=100
   ```

2. **视距优化**：在 `server.properties` 中
   ```properties
   view-distance=4
   ```

3. **禁用不必要的功能**：在 `Cuberite.ini` 中禁用不需要的插件

## 常用命令

- `stop`: 停止服务器
- `say <消息>`: 发送服务器消息
- `op <玩家名>`: 给玩家管理员权限
- `deop <玩家名>`: 移除玩家管理员权限
- `kick <玩家名> [原因]`: 踢出玩家
- `ban <玩家名> [原因]`: 封禁玩家
- `unban <玩家名>`: 解除封禁

## 自动启动设置

在OpenWrt系统中，创建启动脚本实现开机自启：

```bash
# 创建启动脚本
nano /etc/init.d/cuberite
```

添加以下内容：

```bash
#!/bin/sh /etc/rc.common

START=99
STOP=10

start() {
    # 进入服务端目录
    cd /root/cuberite
    # 后台运行服务端
    ./Cuberite > /var/log/cuberite.log 2>&1 &
}

stop() {
    # 查找并停止Cuberite进程
    killall Cuberite
}
```

设置脚本权限并启用服务：

```bash
# 设置执行权限
chmod +x /etc/init.d/cuberite

# 启用服务
/etc/init.d/cuberite enable

# 启动服务
/etc/init.d/cuberite start
```

## 故障排除

1. **内存不足**：
   - 减少视距 (`view-distance`)
   - 降低最大玩家数 (`max-players`)
   - 关闭不必要的插件

2. **启动失败**：
   - 检查端口是否被占用
   - 查看 `server.log` 文件了解具体错误

3. **连接超时**：
   - 检查防火墙设置，确保端口开放
   - 确认网络连接正常

## 总结

Cuberite 是一个轻量级的 Minecraft 服务端，非常适合在资源有限的高通410随身WiFi设备上运行。由于设备硬件限制（512MB内存，4GB存储），建议最多支持1-3人同时游戏。通过合理的配置和优化，可以获得流畅的游戏体验。

## 参考链接

- [Cuberite 官方网站](https://cuberite.org/)
- [Cuberite 文档](https://book.cuberite.org/)
- [Cuberite GitHub 仓库](https://github.com/cuberite/cuberite)