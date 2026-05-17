# LILIRIA（元书版）  
  
基于 `天有四时` 的稳定结构制作的视觉换皮。  
注： `天有四时` 是我最早期制作的一个非常不成熟的皮肤 ~~，现在有了没什么属性的 `LILIRIA` 和 `遇见云上` 之后就彻底摆烂不维护这个皮肤了。~~  
~~（其实看到“天有四时”这个舟属性很重的名字就能明白我为什么懒得继续维护了……）~~  
  
本皮肤主题为“圣女与魔女”：  
  
- 日间模式：Maria，金发碧眼圣女感，使用象牙白、圣金、浅蓝。  
- 夜间模式：Lilith，黑发红瞳魔女感，使用黑紫、酒红、骨白。  
  
## 万象英文 Rime 通道测试说明

- 保留 `wanxiang ↔ wanxiang_english` 的中英方案联动。
- 英文 26 键主字母与 Shift 大写态由 `symbol` 改为 `character`，使按键进入 Rime 引擎。
- 英文逗号同样改为 `character`。
- 滑动、长按中的符号动作保持原样，避免扩大测试变量。

## 视觉风格  
  
LILIRIA 的重点是“同一套键盘骨架下的昼夜双人格”：  
  
- 日间不是纯白，而是偏温柔的象牙米白底。  
- 夜间不是大面积黑红，而是黑紫底、骨白字、酒红强调。  
- 红色只用于高亮和局部强调，避免夜间模式累眼。  
- 边框从 `天有四时` 的厚重边框调整为更细的 1px 。  
- 圆角调整为 12，让整体更接近圣像 / 哥特卡牌 UI，而不是完全方正的工业感。  
- 推荐字体：比较随意，也许可以尝试一些优雅的衬线字体。  
  
## 隐藏的小功能（同 `天有四时` ）  

- 最左边A键长按可选择左侧单手模式，最右边L键长按可选择右侧单手模式。  
- 回车键长按可强制换行，对于iOS端DeepSeek等回车即发送的场合可能有奇效。  
- 以上前提是 `jsonnet/modules/longPressEnabled.libsonnet` 里填了true（启用长按快捷键）。  
  
## 修改入口速查  
  
- 改配色： `jsonnet/skin/default.colors.libsonnet`  
- 改按键宽度、键盘高度、按键 inset、横屏分栏比例与显示密度： `jsonnet/skin/default.layout.libsonnet`  
- 改边框、圆角、字体大小： `jsonnet/skin/default.visualdata.libsonnet`  
- 改上滑 / 下滑快捷键： `jsonnet/modules/swipeEnabled.libsonnet`  
- 改长按快捷键： `jsonnet/modules/longPressEnabled.libsonnet`  
- 改非滑动功能键动作： `jsonnet/lib/shortcutData.libsonnet`  
- 切换二十六键 / 九键： `jsonnet/modules/keyboardConfig.libsonnet` （默认值为 `26` ）  
- 改二十六键布局： `jsonnet/keyboard/Pinyin26.libsonnet`  
- 改九键布局： `jsonnet/keyboard/Pinyin9.libsonnet`  
  - 左侧拼音选择栏必须保留内置 `type: t9Symbols` ；它用于动态选择拼音切分，并非普通符号列表。  
- 改九键按键与滑动快捷键： `jsonnet/modules/t9ShortcutEnabled.libsonnet`  
- 改横屏结构开关与数字区位置： `jsonnet/keyboard/LandscapeConfig.libsonnet`
- 改横屏分栏比例、按键宽度、符号栏宽度与颜文字列数： `jsonnet/skin/default.layout.libsonnet` 的 `landscape` 区块  
- 改英文键盘布局： `jsonnet/keyboard/Alphabetic26.libsonnet`  
- 改数字键盘： `jsonnet/keyboard/Numeric9Portrait.libsonnet`  
- 改符号键盘： `jsonnet/keyboard/Symbolic.libsonnet`  
- 改颜文字键盘： `jsonnet/keyboard/Kaomoji.libsonnet`  
- 改 toolbar 左侧浮动面板： `jsonnet/keyboard/Panel.libsonnet`  
  
## 拼音九键说明  

- 默认仍使用二十六键，不改变原有输入习惯。  
- 需要九键时，将 `jsonnet/modules/keyboardConfig.libsonnet` 中的 `keyboardLayout` 从 `26` 改为 `9` 。  
- 保存后长按皮肤并运行 `main.jsonnet`，配置会自动改为 `pinyin_9_portrait / pinyin_9_landscape` 。  
- 九键竖屏采用三栏结构；横屏左侧显示九键候选区，右侧保留九键输入区。  
- 九键数字上滑、空格上滑输入 0、重输键等动作集中在 `t9ShortcutEnabled.libsonnet`，不会改动二十六键的 `swipeEnabled.libsonnet` 。  
  
## 当前版本说明  
  
除了结构方面的小巧思，还额外加了一个我自己的颜文字键盘。  
toolbar选了超过五个就可以左右滑动了！！！  

## 键盘组件命名规范

`jsonnet/keyboard` 内的组件参考空山素影，统一采用 PascalCase 命名并使用 `.libsonnet` 扩展名；例如 `Pinyin26.libsonnet`、`Numeric9Portrait.libsonnet`。生成后的 YAML 文件名仍保持原样，不影响皮肤配置映射。  
（空山素影真的很强啊家人们，不想折腾的直接用这个肯定没错。回头我查查怎么引用比较合适……）  
