
| OKI<br>内核 | 6.12 | 6.6 | 6.1 | 5.15 |
|:---:|:---:|:---:|:---:|:---:|
| 状态 | ⚠️测试中 | ✅完美运行 | ✅完美运行 | ✅完美运行 |
| 说明 | Droidspaces≥v5.9.5 | Droidspaces全版本支持 | • Droidspaces≥v5.9.5：仅打04.sysvipc_task_struct.patch<br>• 更低版本：打全所有补丁 | • Droidspaces≥v5.9.5：仅打04.sysvipc_task_struct.patch<br>• 更低版本：打全所有补丁 |
| NTsync所需补丁 | 仅打android16-6.12.patch | ntsync_base.patch<br>+<br>android15-6.6.patch | ntsync_base.patch<br>+<br>android14-6.1.patch | ntsync_base.patch<br>+<br>android13-5.15.patch |
| 测试通过的机型 | <div align="left">• 一加15</div> | <div align="left">• 一加Pad2Pro<br>• 一加13<br>• 一加Ace6<br>• 一加Ace5Pro<br>• 一加13T<br>• 一加Ace5至尊版(⚠️测试中)</div> | <div align="left">• 一加Ace3Pro<br>• 一加12<br>• 一加PadPro<br>• 真我GT5Pro</div> | <div align="left">• 一加Ace3</div> |

| GKI<br>内核 | 6.12 | 6.6 | 6.1 | 5.15 | 5.10 |
|:---:|:---:|:---:|:---:|:---:|:---:|
| 状态 | ✅完美运行 | ✅完美运行 | ✅完美运行 | ✅完美运行 | ✅完美运行 |
| 说明 | Droidspaces全版本支持 | Droidspaces≥v5.9.5 | Droidspaces≥v5.9.5 | Droidspaces≥v5.9.5💥特殊<br>• 小米Pad6Spro:使用3-4-5<br>• 红米K70:使用6-7-8<br>• 其他机型自行测试 | Droidspaces≥v5.9.5 |
| NTsync所需补丁 | 仅打android16-6.12.patch | ntsync_base.patch<br>+<br>android15-6.6.patch | ntsync_base.patch<br>+<br>android14-6.1.patch | ntsync_base.patch<br>+<br>android13-5.15.patch | ntsync_base.patch<br>+<br>android12-5.10.patch |
| 测试通过的机型 | <div align="left">• 红米K90ProMax<br>• 小米17ProMax<br>• 小米17Pro<br>• 红魔11<br>• 荣耀magicPad3Pro</div> | <div align="left">• 小米Pad8Pro</div> | <div align="left">• 小米14<br>• 红魔9SPro+<br>• 红魔9Pro</div> | <div align="left">• 小米Pad6SPro<br>• 红米K70</div> | <div align="left">• 小米Pad6Max<br>• 小米Pad6Pro<br>• 红米K50Ultra</div> |


> `⚠️ 测试中` 代表的是可能出现不定时重启
> 
> `✅ 完美运行 ` 代表的是经过多数设备的长期验证，可以稳定运行
> 
> `❓ 未测试` 代表的是无设备验证，不确定是否稳定
>
> `GKI` 只代表米系设备经过验证,但其他设备应该也可以
>
> `💡Droidspaces` 所要文件 [点我跳转](https://cdn.goldzxcbug.top/%E7%A7%BB%E5%8A%A8-Droidspaces-OSS)

# 内核编译指南
> [!IMPORTANT]
> 如果你是新手，你可以按照下面两个指南来编译属于你自己的内核
>- [OKI内核云编译指南](./doc/OKI_kernel.md)
>
>- [GKI内核云编译指南](./doc/GKI_kernel.md)


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
