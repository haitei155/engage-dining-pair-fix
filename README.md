# Fire Emblem Engage — 自定义人物支持 / Custom Unit Support

[English](README.en.md)

**v0.3** · 特技继承列表扩展、双人用餐对话回退与六帧 PNG Loading 小人支持。

**必须先安装 [Cobalt](https://github.com/Raytwo/Cobalt)。** 感谢 **Raytwo** 开发并维护 Cobalt，为本项目提供 MOD 加载与扩展基础。

当前编译版面向《火焰纹章 Engage》2.0.0，使用 Cobalt 1.31.0 作为兼容基线。

## 下载与安装

**[下载 v0.3 完整安装包：engage_custom_unit_support.zip](https://github.com/haitei155/engage-custom-unit-support/releases/download/v0.3/engage_custom_unit_support.zip)** · [发布页面](https://github.com/haitei155/engage-custom-unit-support/releases/tag/v0.3) · [SHA256SUMS](https://github.com/haitei155/engage-custom-unit-support/releases/download/v0.3/SHA256SUMS)

完整 ZIP 已包含 `engage_custom_unit_support.nro` 和三个界面资源文件：`godinfo.bundle`、`unitselectroot.bundle`、`skillselectroot.bundle`，无需分别下载。Bundle 是原始界面的扩展资源包，包含扩充后的控件及布局，与负责插件逻辑的 NRO 配合使用。**仅安装或替换 NRO，无法获得 v0.3 的界面容量扩展。**

1. 先按 [Cobalt](https://github.com/Raytwo/Cobalt) 的说明安装基础运行环境，然后完全退出游戏。
2. 选择一种安装方式：将完整 ZIP 原样放入 `engage/mods/`；或将 ZIP 内的全部内容解压至 `engage/mods/engage-custom-unit-support/`，保留内部 `Data/` 目录结构。不要同时安装 ZIP 和解压副本。
3. 升级已有安装时替换完整插件包；使用解压方式时，同时更新 NRO 和 `Data/` 中的三个 Bundle。**移除旧 `engage_dining_pair_fix.nro`**，避免新旧插件重复加载。若整合包已包含本插件，使用整合包内版本，无需另装独立副本。
4. 完整重启游戏。模拟器使用其配置的虚拟 SD 卡目录；返回标题界面不等于完整重启。

解压安装后的目录如下；直接使用 ZIP 时，这些文件位于 ZIP 内：

```text
engage/mods/engage-custom-unit-support/
├─ engage_custom_unit_support.nro
├─ Data/StreamingAssets/aa/Switch/fe_assets_ui/hub/godroom/prefabs/
│  ├─ godinfo.bundle
│  ├─ unitselectroot.bundle
│  └─ skillselectroot.bundle
└─ RELEASE_NOTES.md
```

Release 中的单独 NRO 只包含插件程序，不能代替完整安装包。Loading 小人的六帧 PNG 由对应人物包另行提供，不包含在上述三个界面 Bundle 中，制作与命名方法见下文。

## v0.3 新增内容

### 特技继承列表扩展

添加纹章士后，选人页右侧“与纹章士的牵绊等级”面板可能放不下全部条目；进入继承详情后，翻到第 20 项之后也可能卡住。两处界面分别受原有 19 个显示格和 20 个导航槽限制。

v0.3 将右侧牵绊面板扩为 **22 项，两列、11 行**，同时补足背景行。面板向下延伸至屏幕底部附近，并增加行高，缓解文字拥挤。持有超过 22 枚纹章士时，该面板最多显示 22 项。

继承详情页预置 **30 个导航槽**，保留原生排序、左右切换和首尾循环；圆点行缩小至原来的三分之二，以容纳 30 个槽。超过 30 项时需继续扩展界面资源。仅显示实际持有的纹章士，不会额外获得戒指、技能或牵绊等级。

本功能需要完整安装包中的 NRO 和三个界面资源文件，具体文件名与目录见上方“下载与安装”。控件在资源中预先扩好，进入页面时由原生流程初始化；NRO 为导航增加越界保护。更新后须完整重启游戏。

**界面资源权利声明：**这三个 Bundle（含完整 ZIP 内的副本）不适用插件代码的 Apache-2.0 许可，其权利范围单独说明，见[界面资源权利声明](resources/inheritance/NOTICE.md)。

## v0.2 功能

### 六帧 PNG Loading 小人

原生 Loading 找不到人物贴图时，本插件按人物转换后的实际 UnitIconID 从已启用的 Cobalt 包读取资源。优先路径：`patches/icon/loading/Dot_Run_<UnitIconID>.png`，格式为透明 **288×48 RGBA PNG，横排六个 48×48 帧**，身份键的拼写与大小写须匹配。这是一张六帧横排图，运行时不读取 GIF 或六张独立图片；没有可用 PNG 时仍可回退到对应 Loading Bundle。资源不存在或无效时跳过。

**六帧 PNG Loading 小人需要 MOD 制作者自行制作。** 本插件提供素材读取与原生动画支持，不负责生成图像。目前提供的琉弥艾尔样例为作者本人自行制作的素材；其他人物仍需由其 MOD 制作者自行制作对应的六帧图。

#### 琉弥艾尔 PNG 样例

![琉弥艾尔（Lumera）的六帧横排 Loading 跑步图](images/lumera-loading-run-six-frames.png)

样例文件：[`lumera-loading-run-six-frames.png`](images/lumera-loading-run-six-frames.png)。这是作者本人制作的琉弥艾尔 Loading 动画素材，采用透明 **288×48 RGBA PNG**，横排六个 **48×48** 帧，可供 MOD 制作者参考素材格式与接入方法。

用于琉弥艾尔人物包时，将下载的样例重命名为 `Dot_Run_555Lumiere.png`，放入 `patches/icon/loading/Dot_Run_555Lumiere.png`。样例的英文文件名用于文档展示，游戏读取名称必须匹配琉弥艾尔实际 UnitIconID：`555Lumiere`。其他人物应提供本人六帧图并使用其对应身份键；NRO 不自动生成缺失素材。

Loading 模式、邀请参与者、出场队列和六帧动画继续使用原生规则；原本不显示队列的 Loading 不强制增加队列。v0.2 在清理自定义槽位前恢复保留的材质模板，保护缓存贴图不被 Unity 的资源清理卸载，并在缓存失效时重新读取。这些改动用于修正后续 Loading 显示白色方块的问题。

正式构建不输出本插件诊断日志。游戏期间缓存素材，修改 PNG 或 ZIP 后须完整重启游戏。

## v0.1 功能

### 双人用餐

- 为部分缺少专用对话标签的双人用餐组合提供回退。
- 只在原标签为空时调用游戏原生料理评价台词选择，根据人物、料理品质和喜好选择好吃／一般／不喜欢的台词。
- 已有正常双人对话保持原标签。

### 用餐修复场景与截图

下图为自定义新增角色参与双人用餐的开场界面。根据作者实测，没有本补丁时，受影响组合大概率在此界面结束、准备进入后续对话时卡死。部分组合缺少专用双人对话标签，原流程取到空标签后无法正常继续；本补丁在此处改用原生料理评价台词回退。

![双人用餐开场：受影响组合可能在这一界面结束后卡住](images/paired-dining-opening-before-dialogue.jpg)

启用补丁后，下面两张截图展示了这组角色继续进入正常用餐评价对话的过程。截图中的支援提示是正常游戏流程的显示，本补丁的作用是避免缺失对话标签阻断用餐，不额外创建支援事件。

![修复后继续进入琉尔的用餐评价对话](images/paired-dining-dialogue-alear.jpg)

![修复后继续进入艾莉可的用餐评价对话](images/paired-dining-dialogue-eirika.jpg)

## 项目改名与升级

项目由 `engage-dining-pair-fix` 更名为 `engage-custom-unit-support`，v0.2 NRO 为 `engage_custom_unit_support.nro`。新版已经包含原用餐修复，旧名与新名 NRO 同时加载会造成重复钩子；升级时用新 NRO 替换旧 NRO。

## 源码与构建

见 [构建说明](docs/BUILD.md)。源码包括特技继承列表扩展、双人用餐回退、Loading 素材支持和实际使用的本地依赖快照；构建产物输出到 `dist/`。`Releases/` 保存 v0.3 编译版与校验值。

## 许可与致谢

| 内容 | 许可或权利声明 |
|---|---|
| 本项目自行新增的代码、修改脚本和文档 | [Apache License 2.0](LICENSE) |
| 三个配套界面 Bundle（含完整 ZIP 内的副本） | [界面资源权利声明](resources/inheritance/NOTICE.md)，不适用上述代码许可 |
| 第三方依赖与上游派生部分 | 保留各自许可，见 [THIRD_PARTY.md](THIRD_PARTY.md) 和 [NOTICE](NOTICE) |

完整安装包包含不同许可范围的内容，不能将整个 ZIP 视为统一采用 Apache-2.0。

感谢 [Raytwo](https://github.com/Raytwo/Cobalt)、[skyline-rs](https://github.com/skyline-rs) 以及相关依赖贡献者。
