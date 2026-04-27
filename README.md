| 内核系列 | 版本 | 目前状态 | 说明 | NTsync 所需补丁 |
|---------|------|------|------|----------------|
| **OKI** | 6.12 | ⚠️ 测试中（容器可能不定时重启） | Droidspaces ≥ v5.9.5 | `ntsync_compat_android16-6.12.patch`（仅此一个） |
| | 6.6 | ✅ 完美运行 | Droidspaces 全版本支持 | `ntsync_base.patch` + `ntsync_compat_android15-6.6.patch` |
| | 6.1 | ✅ 完美运行 | • Droidspaces ≥ v5.9.5：仅打 `04.use_android_abi_padding_for_sysvipc_task_struct.patch`<br>• 更低版本：打全所有补丁 | `ntsync_base.patch` + `ntsync_compat_android14-6.1.patch` |
| | 5.15 | ✅ 完美运行 | • Droidspaces ≥ v5.9.5：仅打 `04.use_android_abi_padding_for_sysvipc_task_struct.patch`<br>• 更低版本：打全所有补丁 | ❌ 未测试 |
| **GKI** | 6.12 | ✅ 完美运行 | Droidspaces 全版本支持 |  `ntsync_compat_android16-6.12.patch`（仅此一个） |
| | 6.6 | ❓ 未测试 | 未测试 | 未测试 |

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
## NTsync 所要配置
```txt
CONFIG_NTSYNC=y
```
