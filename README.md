# 自动为 CR6608 构建 ImmortalWrt
自动拉取最新 ImmoralWrt ImageBuilder 并构建镜像，每日 0：00 执行。
构建目标，添加和移除的软件包在 `config` 下，通过 `Matrix` 自动构建多版本镜像，资产从 `Action` 获取。

# 版本说明
`cr6608-full` 针对图形化管理以及透明代理提供了内建软件包支持，并删去了 `ppp`,`pppoe` 等拨号相关的服务，没有 `iptables` 支持。
`cr6608-mini` 针对简单的旁路由需求优化，删去了 `ppp`,`pppoe` 等拨号相关的服务，没有 `iptables` 支持。

# 复用
如需修改安装和修改的软件包，请修改 `config` 下的版本文件，用法：
```
# 添加的软件包
PACKAGES:htop kmod-nft-tproxy

# 移除的软件包
PACKAGES:-ppp -pppoe

# 构建目标
PROFILE:xiaomi_mi-router-CR6608
```

如须修改或添加已有的版本，请更改 `.github/workflows/build.yaml` 的 `matrix`.
如需修改构建目标，请填写正确的 `PROFILE`，可以拉取 `ImageBuilder` 并执行 `make info` 获得。
