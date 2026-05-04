# OKI内核 云端编译指南 
- 适用设备：一加，OPPO，真我
- 适用内核版本：6.1-6.12
>[!TIP]
>
>本教程仅适用于编译支持 **Droidspaces** 和 **NTsync** 的内核
>
>请严格按照教学，以确保内核编译不出错并完美运行


## 前提准备：
- 知道 [Droidspaces项目](https://github.com/ravindu644/Droidspaces-OSS) 是干什么的
- 一台解了 Bootloader 锁的设备，设备建议高通骁龙(否则没有GPU加速)
- 查看 `设置－>关于手机->版本信息->内核版本` 是否为 `6.1.xxx~6.12.xxx` 内核版本
- 备份好你的手机对应的原 `Boot` 文件
- 系统必须是 `ColorOS` `OxygenOS`

## 配置
### 1.Fork [cctv18](https://github.com/cctv18) 的内核项目
- OKI内核6.1系列 https://github.com/cctv18/oppo_oplus_realme_sm8650
- OKI内核6.6系列 https://github.com/cctv18/oppo_oplus_realme_sm8750
- OKI内核6.12系列 https://github.com/cctv18/oppo_oplus_realme_sm8850
>[!WARNING]
>请选择你对应的手机内核版本的项目，一旦选错，100%不开机
