<table>
  <thead>
    <tr>
      <th width="10%">内核系列</th>
      <th width="8%">版本</th>
      <th width="12%">状态</th>
      <th width="30%">说明</th>
      <th width="20%">NTsync 所需补丁</th>
      <th width="20%">测试通过的机型</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="4" align="center"><b>OKI</b></td>
      <td align="center">6.12</td>
      <td align="center">⚠️ 测试中</td>
      <td>Droidspaces ≥ v5.9.5</td>
      <td><code>仅打 android16-6.12.patch</code></td>
      <td>• 一加 15</td>
    </tr>
    <tr>
      <td align="center">6.6</td>
      <td align="center">✅ 完美运行</td>
      <td>Droidspaces 全版本支持</td>
      <td><code>ntsync_base.patch</code> + <code>android15-6.6.patch</code></td>
      <td>• 一加 Pad 2 Pro<br>• 一加 13<br>• 一加 Ace 6<br>• 一加 Ace 5 Pro<br>• 一加 13T<br>• 一加 Ace5至尊版(⚠️ 测试中)</td>
    </tr>
    <tr>
      <td align="center">6.1</td>
      <td align="center">✅ 完美运行</td>
      <td>• Droidspaces ≥ v5.9.5：仅打 <code>04.sysvipc_task_struct.patch</code> 补丁<br>• 更低版本：打全所有补丁</td>
      <td><code>ntsync_base.patch</code> + <code>android14-6.1.patch</code></td>
      <td>• 一加 Ace 3 Pro<br>• 一加 12<br>• 一加 Pad Pro<br>• 真我 GT 5 Pro</td>
    </tr>
    <tr>
      <td align="center">5.15</td>
      <td align="center">✅ 完美运行</td>
      <td>• Droidspaces ≥ v5.9.5：仅打 <code>04.sysvipc_task_struct.patch</code> 补丁<br>• 更低版本：打全所有补丁</td>
      <td><code>ntsync_base.patch</code> + <code>android13-5.15.patch</code></td>
      <td>• 一加 Ace 3</td>
    </tr>
    <tr>
      <td rowspan="5" align="center"><b>GKI</b></td>
      <td align="center">6.12</td>
      <td align="center">✅ 完美运行</td>
      <td>Droidspaces 全版本支持</td>
      <td><code>仅打 android16-6.12.patch</code></td>
      <td>• 红米 K90 ProMax<br>• 小米 17 Pro Max<br>• 红魔 11</td>
    </tr>
    <tr>
      <td align="center">6.6</td>
      <td align="center">✅ 完美运行</td>
      <td>Droidspaces ≥ v5.9.5</td>
      <td align="center">❓未测试</td>
      <td>• 小米 Pad 8 Pro</td>
    </tr>
    <tr>
      <td align="center">6.1</td>
      <td align="center">✅ 完美运行</td>
      <td>Droidspaces ≥ v5.9.5</td>
      <td align="center">❓未测试</td>
      <td>• 小米 14<br>• 红魔9SPro+</td>
    </tr>
    <tr>
      <td align="center">5.15</td>
      <td align="center">✅ 完美运行</td>
      <td>Droidspaces ≥ v5.9.5 💥特殊<br>• 小米 Pad6S pro :使用3-4-5<br>• 红米 K70 :使用6-7-8<br>• 其他机型自行测试</td>
      <td align="center">❓未测试</td>
      <td>• 小米 Pad6S Pro<br>• 红米 K70</td>
    </tr>
    <tr>
      <td align="center">5.10</td>
      <td align="center">✅ 完美运行</td>
      <td>Droidspaces ≥ v5.9.5</td>
      <td align="center">❓未测试</td>
      <td>• 小米 Pad 6 Max<br>• 小米 Pad 6 Pro</td>
    </tr>
  </tbody>
</table>



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
