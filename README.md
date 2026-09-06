# prompt-to-image v0.4

一个用于把自然语言视觉需求**稳定路由为高质量设定板/排版图**的 Prompt Engineering Skill。

> 为爱发电，免费开源。

## 解决的问题

直接用 AI 出“三视图”“资料板”“阵营 KV”时，模型经常：

- 版面乱排、标签错位
- 把多张参考图平均融合成四不像
- 文字提示词互相覆盖，主体不突出
- 缺少比例、材质、结构说明

这个 Skill 通过**严格模板路由 + 变量绑定 + 版式冻结**，让 AI 按固定结构输出角色、道具、载具、场景、室内等设定资料板。

## 支持模板

| 模板 | 用途 | 示例 |
|---|---|---|
| `character-sheet` | 单个角色/生物/机甲生命体 | 三视图 + 表情/细节 |
| `group-lineup-sheet` | 群像资料板、阵营档案 | 多人并列 + 身份标注 |
| `group-poster-sheet` | 群像宣传海报、阵营 KV | 主视觉 + 排版 |
| `prop-sheet` | 武器、装备、饰品、机械物件 | 全景 + 结构/材质细节 |
| `vehicle-sheet` | 汽车、飞机、船舶、飞船、机甲载具 | 多视图 + 剖面 |
| `environment-sheet` | 建筑外部、场地、环境 | 全景 + 分区标注 |
| `interior-sheet` | 驾驶舱、客舱、房间等封闭空间内部 | 全景 + 功能区拆解 |

## 原理

1. **路由**：先判断用户需求属于哪种输出类型，只选择唯一模板。
2. **变量绑定**：只替换模板中 `【】` 包裹的槽位，不额外扩写提示词。
3. **版式冻结**：将 `# Image prompt` 代码块作为唯一提示词骨架直接发给图像模型。
4. **执行协议**：按 `execution-protocol.md` 完成变量绑定与模板冻结，冻结后不再润色。

## 文件结构

```
prompt-to-image-v0.4/
├── SKILL.md                        # 主入口与路由逻辑
├── agents/
│   └── openai.yaml                 # Agent 配置
└── references/
    ├── character-sheet.md          # 角色模板
    ├── group-lineup-sheet.md       # 群像资料板模板
    ├── group-poster-sheet.md       # 群像海报模板
    ├── prop-sheet.md               # 道具模板
    ├── vehicle-sheet.md            # 载具模板
    ├── environment-sheet.md        # 场景模板
    ├── interior-sheet.md           # 室内模板
    ├── execution-protocol.md       # 执行协议
    ├── routing-rules.md            # 路由规则
    └── routing-tests.md            # 路由测试用例
```

## 使用方法

本 Skill 适用于任何支持 Markdown Skill 格式的 AI 平台或工作流编排工具。

1. 将整个文件夹放入你的 Skill 目录。
2. 在对话中描述你想要的视觉内容，例如：
   - “生成一张赛博朋克雇佣兵小队的群像资料板”
   - “做一把外星科技的仪式长矛设定图，要结构拆解”
   - “画一个火星基地的全景设定板，标注功能区”
3. Skill 会自动选择模板并生成对应提示词。

## 示例

见公众号文章 / 仓库示例文件夹（由社区持续补充）。

## 仓库地址

GitHub: https://github.com/kanzuori/prompt-to-image-v0.4

## 授权

MIT License —— 可自由使用、修改、再分发。

## 作者

砍做日
