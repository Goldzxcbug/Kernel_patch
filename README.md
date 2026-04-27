<table>
  <thead>
    <tr><th style="width:10%">内核系列</th>
      <th style="width:8%">版本</th>
      <th style="width:40%">目前状态</th>
      <th style="width:32%">说明</th>
      <th style="width:10%">NTsync 所需补丁</th>
    </tr>
  </thead>
  <tbody>
    <tr><td rowspan="4"><b>OKI</b></td><td>6.12</td><td>⚠️ 测试中<br>(容器可能不定时重启)</td><td>Droidspaces ≥ v5.9.5</td><td><code>ntsync_compat_android16-6.12.patch</code>（仅此一个）</td></tr>
    <tr><td>6.6</td><td>✅ 完美运行</td><td>Droidspaces 全版本支持</td><td><code>ntsync_base.patch</code> + <code>ntsync_compat_android15-6.6.patch</code></td></tr>
    <tr><td>6.1</td><td>✅ 完美运行</td><td>• Droidspaces ≥ v5.9.5：仅打 <code>04.use_android_abi_padding_for_sysvipc_task_struct.patch</code><br>• 更低版本：打全所有补丁</td><td><code>ntsync_base.patch</code> + <code>ntsync_compat_android14-6.1.patch</code></td></tr>
    <tr><td>5.15</td><td>✅ 完美运行</td><td>• Droidspaces ≥ v5.9.5：仅打 <code>04.use_android_abi_padding_for_sysvipc_task_struct.patch</code><br>• 更低版本：打全所有补丁</td><td>❌ 未测试</td></tr>
    <tr><td rowspan="2"><b>GKI</b></td><td>6.12</td><td>✅ 完美运行</td><td>Droidspaces 全版本支持</td><td>仅需打一个补丁（具体名称见发布包）</td></tr>
    <tr><td>6.6</td><td>❓ 未测试</td><td>未测试</td><td>未测试</td></tr>
  </tbody>
</table>

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
