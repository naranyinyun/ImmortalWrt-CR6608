# CR6608 ImmortalWrt 自动构建
自动拉取最新 ImmoralWrt ImageBuilder 并构建镜像，每日 0：00 执行。    
构建目标，添加和移除的软件包在 `config` 下，通过 `Matrix` 自动构建多版本镜像，资产从 `Action` 获取。    


# 版本说明
`cr6608-full` 针对图形化管理以及透明代理提供了内建软件包支持，并删去了 `ppp`,`pppoe` 等拨号相关的服务，没有 `iptables` 支持。    
`cr6608-mini` 针对简单的旁路由需求优化，删去了 `ppp`,`pppoe` 等拨号相关的服务，没有 `iptables` 支持。   


# 复用
如需修改安装和修改的软件包，请修改 `config` 下的版本文件，用法：    
```
# 添加的软件包
PACKAGES=htop kmod-nft-tproxy

# 移除的软件包
PACKAGES=-ppp -pppoe

# 构建目标
PROFILE=xiaomi_mi-router-CR6608
```

如须修改或添加已有的版本，请更改 `.github/workflows/build.yaml` 的 `matrix`.    
如需修改构建目标，请填写正确的 `PROFILE`，可以拉取 `ImageBuilder` 并执行 `make info` 获得。    

# 故障排查
1. `ImageBuilder` 下载链接目前被硬编码在 `build.yaml` 中, 如遇下载问题, 尝试修正下载链接.     
2.  默认使用 `Cache` 缓存下载的资产和构建中间产物用于加速构建, 如遇构建问题, 可以尝试删除所有 `Cache` 重试.
3.  `Matrix` 目标必须与 `config` 下配置文件名一致. 配置文件格式必须遵循上述格式, 或者修改 `build.yaml` 中的裁剪规则使其工作.
