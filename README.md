<p align="center">
  <img src="./cover.png" width="100%" alt="prompt-to-image v0.4">
</p>

<h1 align="center">prompt-to-image v0.4</h1>

<p align="center">
  将自然语言视觉需求稳定路由为高质量设定板 / 资料板 / 排版图的 Prompt Engineering Skill
</p>

<p align="center">
  <strong>严格模板路由 · 变量绑定 · 版式冻结 · 稳定输出</strong>
</p>

<p align="center">
  免费开源 · MIT License
</p>

---

## ✦ 解决的问题

直接让 AI 生成「三视图」「角色资料板」「阵营 KV」「载具设定图」时，经常会出现：

- 版面随机，信息层级混乱
- 标签错位，文字与主体对应错误
- 多张参考图被平均融合，失去明确特征
- 提示词互相覆盖，主体不突出
- 缺少比例、材质、结构、功能区等专业说明
- 同一需求重复生成时，排版稳定性较差

**prompt-to-image** 通过：

> **严格模板路由 + 变量绑定 + 版式冻结 + 执行协议**

将自然语言需求映射到固定的视觉模板，让图像模型按照预设结构生成角色、群像、道具、载具、场景与室内空间等专业设定资料板。

---

## ✦ 示例效果

<table>
  <tr>
    <td align="center" width="50%">
      <img src="./example-mercenary.jpg" width="100%">
      <br>
      <strong>角色 / 雇佣兵设定</strong>
    </td>
    <td align="center" width="50%">
      <img src="./example-xuanning.jpg" width="100%">
      <br>
      <strong>角色设定资料板</strong>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="./example-spear.jpg" width="100%">
      <br>
      <strong>道具 / 武器结构设定</strong>
    </td>
    <td align="center">
      <img src="./example-cockpit.jpg" width="100%">
      <br>
      <strong>驾驶舱 / 室内空间设定</strong>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="./example-mars.jpg" width="100%">
      <br>
      <strong>火星基地 / 环境设定</strong>
    </td>
    <td align="center">
      <img src="./example-fox.jpg" width="100%">
      <br>
      <strong>生物 / 角色设定</strong>
    </td>
  </tr>
</table>

---

## ✦ 支持模板

| 模板 | 适用内容 | 典型输出 |
|---|---|---|
| `character-sheet` | 单个角色、生物、机甲生命体 | 三视图、表情、局部细节 |
| `group-lineup-sheet` | 群像资料板、阵营档案 | 多人并列、身份标注 |
| `group-poster-sheet` | 群像宣传海报、阵营 KV | 主视觉、宣传排版 |
| `prop-sheet` | 武器、装备、饰品、机械物件 | 全景、结构、材质细节 |
| `vehicle-sheet` | 汽车、飞机、船舶、飞船、机甲载具 | 多视图、结构、剖面 |
| `environment-sheet` | 建筑外部、场地、自然环境 | 全景、分区、功能标注 |
| `interior-sheet` | 驾驶舱、客舱、房间等封闭空间 | 空间全景、功能区拆解 |

---

## ✦ 工作原理

### 1. Routing / 路由

首先判断用户需求属于哪一种视觉输出类型。

每次只选择 **一个唯一模板**，避免不同版式规则相互污染。

### 2. Variable Binding / 变量绑定

模板中的：

```text
【变量】
```

作为唯一可替换槽位。

执行过程中只进行变量绑定，不随意重写模板结构。

### 3. Layout Freeze / 版式冻结

模板中的：

```text
# Image prompt
```

代码块作为最终图像提示词骨架。

模板一旦冻结，不再重新组织结构或二次润色。

### 4. Execution Protocol / 执行协议

按照 `execution-protocol.md`：

```text
用户需求
   ↓
需求解析
   ↓
模板路由
   ↓
变量绑定
   ↓
模板冻结
   ↓
Image Prompt
   ↓
图像模型
```

从而尽可能减少模型在执行过程中的自由改写。

---

## ✦ 文件结构

```text
prompt-to-image-v0.4/
│
├── SKILL.md
│   └── 主入口 / 路由逻辑
│
├── agents/
│   └── openai.yaml
│       └── Agent 配置
│
├── references/
│   ├── character-sheet.md
│   │   └── 单角色设定模板
│   │
│   ├── group-lineup-sheet.md
│   │   └── 群像资料板模板
│   │
│   ├── group-poster-sheet.md
│   │   └── 群像海报模板
│   │
│   ├── prop-sheet.md
│   │   └── 道具 / 武器模板
│   │
│   ├── vehicle-sheet.md
│   │   └── 载具模板
│   │
│   ├── environment-sheet.md
│   │   └── 环境 / 建筑模板
│   │
│   ├── interior-sheet.md
│   │   └── 室内空间模板
│   │
│   ├── execution-protocol.md
│   │   └── 执行协议
│   │
│   ├── routing-rules.md
│   │   └── 路由规则
│   │
│   └── routing-tests.md
│       └── 路由测试用例
│
├── cover.png
│
├── example-cockpit.jpg
├── example-fox.jpg
├── example-mars.jpg
├── example-mercenary.jpg
├── example-spear.jpg
└── example-xuanning.jpg
```

---

## ✦ 使用方法

本 Skill 适用于支持 Markdown Skill / Agent Skill 机制的 AI 平台或工作流。

### Step 1

将整个：

```text
prompt-to-image-v0.4
```

目录放入对应的 Skill 目录。

### Step 2

直接使用自然语言描述你希望生成的视觉内容。

例如：

```text
生成一张赛博朋克雇佣兵小队的群像资料板
```

```text
做一把外星科技仪式长矛的设定图，需要结构拆解
```

```text
画一个火星基地的全景设定板，并标注主要功能区
```

```text
设计一艘深空运输舰，需要侧视图、俯视图和结构剖面
```

### Step 3

Skill 自动完成：

```text
需求识别
→ 模板路由
→ 变量绑定
→ Prompt 冻结
→ 输出最终 Image Prompt
```

无需手动选择模板。

---

## ✦ 一个核心原则

这个项目并不是试图让模型：

> 「更会写 Prompt」

而是尽可能限制模型在关键结构上的自由度：

```text
不让模型重新设计版式
不让模型任意增加模块
不让模型混合多个模板
不让模型冻结后继续润色 Prompt
```

把更多不确定性从：

```text
Prompt Generation
```

转移到：

```text
Template Selection
+
Variable Binding
```

从而提高复杂视觉设定任务的稳定性和可复现性。

---

## ✦ 适用场景

特别适合：

- 游戏角色设定
- 动画 / 影视概念设计
- 世界观资料板
- 游戏道具设计
- 武器与装备设计
- 科幻载具设计
- 建筑与环境概念设计
- 驾驶舱 / 室内空间设计
- AI 视觉工作流
- Prompt Engineering
- Concept Art Pipeline

---

## ✦ 示例

更多案例可查看本仓库中的：

```text
example-*.jpg
```

后续示例由社区持续补充。

公众号文章：**砍做日**

---

## ✦ License

MIT License

可自由：

- 使用
- 修改
- 分发
- 商业使用

具体条款见 [`LICENSE`](./LICENSE)。

---

## ✦ 作者

**砍做日**

如果这个项目对你的 AI 视觉工作流有帮助，欢迎 Star / Fork / 提交新的模板与案例。
