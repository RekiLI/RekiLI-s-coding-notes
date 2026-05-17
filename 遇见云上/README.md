# 遇见云上（元书版） v1.5

“遇见云上”是一款以 `Pantone 2026 年度代表色 “云上舞白”` 为共同底色、内置六套完整配色主题的元书输入法皮肤。  
比起 `LILIRIA` 主要是多了可选的几套配色。  

## v1.5 更新

- 中英切换联动万象方案：切到英文键盘时尝试启用 `wanxiang_english`，切回中文键盘时启用 `wanxiang`。
- 英文键盘默认仍使用 `symbol` 直输；只有当前 Rime schema 实际为 `wanxiang_english` 时，26 个主字母才通过 `character` 进入 Rime。
- 因此未安装 / 未启用万象英文时，英文键盘仍可作为普通直输键盘使用；手动切到其他 Rime 方案时，也不会让英文键盘意外参与中文输入。
- 条件接管依赖支持 `schemaChanged + rimeSchemaID` 的元书版本。
- 因为这个皮肤的toolbar特别容易卡，我个人习惯删到不超过五个，如果要使用RimeSwitcher而又塞不进toolbar，可以在 `jsonnet/modules/longPressEnabled.libsonnet` 模仿别的按键，随便选取一个喜欢的按键加入长按快捷键设置。  

## 关于皮肤

PANTONE 11-4201 Cloud Dancer（云上舞白）是 Pantone 2026 年度代表色。本皮肤的主题方向参考了潘通小红书官方账号发布的“云上舞白”配色组合图，并针对手机屏幕、按键层级与长时间输入的可读性重新调整。

> 皮肤中的十六进制色号是屏幕显示用的近似设计值，不是 Pantone 官方专色色值，也不代表官方 RGB 转换结果。

## 内置主题

在 `jsonnet/skin/default.colors.libsonnet` 中修改 `selectedTheme` 即可切换：

| 编号 | 主题 | 主要方向 |
| --- | --- | --- |
| `C01` | 光影叠韵 | 云白、薄荷灰、海蓝与柔金，默认主题 |
| `C02` | 氛围空境 | 轻蓝、青灰与明净水色 |
| `C03` | 舒适之域 | 沙色、珊瑚、木玫瑰与暖棕 |
| `C04` | 柔雾粉彩 | 冰蓝、淡桃、浅绿与雾紫 |
| `C05` | 魅光流熠 | 云白、石墨黑、绯红与暗金 |
| `C06` | 极简黑白 | 柔和近黑、暖白与极简描边，不使用按键下阴影 |

首版从参考图中的组合里选取五组；“片刻休憩”暂未收录，以避免高频输入界面出现过多高饱和暖色。

### 切换示例

```jsonnet
local selectedTheme = 'C03';
```

保存后回到皮肤界面，长按“遇见云上”，运行 `main.jsonnet` 生效。Panel 中的“主题”按钮会直接打开这一选择文件。

## 透明背景

键盘容器背景在所有主题、日间模式和夜间模式下都固定为：

```jsonnet
'#00000000'
```

这样可以尽量规避 iOS 不同应用中键盘圆角、顶部衔接与底部安全区的背景适配差异。普通键帽、功能键、回车键与候选高亮仍保留实体颜色，不会变成悬空文字。

## 修改入口速查

- 选择主题：`jsonnet/skin/default.colors.libsonnet`
- 查看或微调六套主题色号：`jsonnet/skin/themes/`
- 改按键宽度、键盘高度、按键 inset、横屏分栏比例与显示密度：`jsonnet/skin/default.layout.libsonnet`
- 改边框、圆角、字体大小：`jsonnet/skin/default.visualdata.libsonnet`
- 改上滑 / 下滑快捷键：`jsonnet/modules/swipeEnabled.libsonnet`
- 改长按快捷键：`jsonnet/modules/longPressEnabled.libsonnet`
- 改非滑动功能键动作：`jsonnet/lib/shortcutData.libsonnet`
- 切换二十六键 / 九键：`jsonnet/modules/keyboardConfig.libsonnet`，默认值为 `26`
- 改二十六键布局：`jsonnet/keyboard/Pinyin26.libsonnet`
- 改九键布局：`jsonnet/keyboard/Pinyin9.libsonnet`
- 改九键按键与滑动快捷键：`jsonnet/modules/t9ShortcutEnabled.libsonnet`
- 改横屏结构开关与数字区位置：`jsonnet/keyboard/LandscapeConfig.libsonnet`
- 改 toolbar 配置：`jsonnet/modules/toolbarConfig.libsonnet`
- 改 toolbar 左侧浮动面板：`jsonnet/keyboard/Panel.libsonnet`

## 拼音九键说明

- 默认使用二十六键，不改变原有输入习惯。
- 需要九键时，将 `jsonnet/modules/keyboardConfig.libsonnet` 中的 `keyboardLayout` 从 `'26'` 改为 `'9'`。
- 保存后长按皮肤并运行 `main.jsonnet`，配置会自动切换为 `pinyin_9_portrait / pinyin_9_landscape`。
- 九键左侧拼音选择栏必须保留内置 `type: t9Symbols`，它负责动态选择拼音切分，不是普通符号列表。
- 九键数字上滑、空格上滑输入 0、重输键等动作集中在 `t9ShortcutEnabled.libsonnet`。

## 继承的键盘结构

本皮肤以 LILIRIA 的重规范结构为基础继续调整，并保留：

- 二十六键横屏左右双区；拼音九键横屏候选区 + 九键区。
- 数字键盘横屏数字区 + 分类符号区。
- 符号与颜文字键盘的横屏密度适配。
- `swipeEnabled.libsonnet` 与 `longPressEnabled.libsonnet` 作为真实总开关。
- `w` 下滑输入 `……`、`e` 下滑输入 `、`、`h` 下滑输入 `—` 等快捷输入。
- 最左侧 `A` 键长按切换左手模式、最右侧 `L` 键长按切换右手模式。
- 回车键长按强制换行。
- 候选栏、toolbar、自定义符号键盘与颜文字键盘。

## 结构说明

`jsonnet/skin/default.colors.libsonnet` 只负责选择主题，不直接堆放色号。六套完整颜色表位于 `jsonnet/skin/themes/`，通过 `themes/index.libsonnet` 统一登记；`themes/fixed.libsonnet` 强制锁定透明背景。

键盘组件仍统一从 `modules/dr.libsonnet` 读取颜色，因此切换主题不会改变布局、快捷键、横屏结构或九键逻辑。

## TODO

- [ ] 现在的配色模式还比较简单，考虑日后设计更复杂更美观的款式。 ~~当然现在简简单单的样子也很好~~  
- [ ] 进一步规范语法、文件名和文件位置。  
