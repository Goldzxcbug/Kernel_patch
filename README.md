| 内核系列 | 版本 | 状态 | 说明 | NTsync 所需补丁 |
|----------|------|----------|------|----------------|
| **OKI** | 6.12 | ⚠️ 测试中 | Droidspaces ≥ v5.9.5 | `ntsync_compat_android16-6.12.patch`（仅此一个） |
| | 6.6 | ✅ 完美运行 | Droidspaces 全版本支持 | `ntsync_base.patch` + `ntsync_compat_android15-6.6.patch` |
| | 6.1 | ✅ 完美运行 | • Droidspaces ≥ v5.9.5：仅打 `04.use_android_abi_padding_for_sysvipc_task_struct.patch`<br>• 更低版本：打全所有补丁 | `ntsync_base.patch` + `ntsync_compat_android14-6.1.patch` |
| | 5.15 | ✅ 完美运行 | • Droidspaces ≥ v5.9.5：仅打 `04.use_android_abi_padding_for_sysvipc_task_struct.patch`<br>• 更低版本：打全所有补丁 | `ntsync_base.patch` + `ntsync_compat_android13-5.15.patch`|
| **GKI** | 6.12 | ✅ 完美运行 | Droidspaces 全版本支持 | `ntsync_compat_android16-6.12.patch`（仅此一个）  |
| | 6.6 | ✅ 完美运行| Droidspaces ≥ v5.9.5 | ❓未测试 |
| | 6.1 | ✅ 完美运行| Droidspaces ≥ v5.9.5 | ❓未测试 |
| | 5.15 | ✅ 完美运行| Droidspaces ≥ v5.9.5 | ❓未测试 |
> `⚠️ 测试中` 代表的是可能出现不定时重启
> 
> `✅ 完美运行 ` 代表的是经过多数设备的长期验证，可以稳定运行
> 
> `❓ 未测试` 代表的是无设备验证，不确定是否稳定
>
> `GKI` 只代表米系设备经过验证,但其他设备应该也可以
>
> `💡Droidspaces` 所要文件 [点我跳转](https://cdn.goldzxcbug.top/%E7%A7%BB%E5%8A%A8-Droidspaces-OSS)
## Droidspaecs ≥ v5.9.5 所要配置
```txt
# IPC
CONFIG_SYSVIPC=y
CONFIG_POSIX_MQUEUE=y

# 命名空间
CONFIG_IPC_NS=y
CONFIG_PID_NS=y

# 硬件访问
CONFIG_DEVTMPFS=y
```

## Droidspaecs < v5.9.5 所要配置
```txt
# 修复 [✗] PID namespace 和 [✗] IPC
CONFIG_SYSCTL=y
CONFIG_SYSVIPC=y
CONFIG_POSIX_MQUEUE=y
CONFIG_NAMESPACES=y
CONFIG_PID_NS=y
CONFIG_IPC_NS=y
CONFIG_UTS_NS=y
CONFIG_USER_NS=y
# 修复 [✗] devtmpfs support
CONFIG_DEVTMPFS=y
CONFIG_DEVTMPFS_MOUNT=y
# 修复 cgroup devices support
CONFIG_CGROUPS=y
CONFIG_CGROUP_DEVICE=y
CONFIG_CGROUP_PIDS=y
CONFIG_MEMCG=y
```
## Droidspaecs 格外配置（可选）
```txt
#网络（Docker/NAT支持）
CONFIG_NETFILTER_XT_MATCH_ADDRTYPE=y

#UFW 支持
CONFIG_NETFILTER_XT_TARGET_REJECT=y
CONFIG_NETFILTER_XT_TARGET_LOG=y
CONFIG_NETFILTER_XT_MATCH_RECENT=y

#Fail2ban 支持
CONFIG_IP_SET=y
CONFIG_IP_SET_HASH_IP=y
CONFIG_IP_SET_HASH_NET=y
CONFIG_NETFILTER_XT_SET=y
```
## NTsync 所要配置
```txt
CONFIG_NTSYNC=y
```

## Patch 补丁来源
- [Droidspaces](https://github.com/ravindu644/Droidspaces-OSS/tree/main/Documentation/resources/kernel-patches)
- [WildKernels](https://github.com/WildKernels/kernel_patches/tree/main/common)
