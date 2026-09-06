---
name: prompt-to-image-v0-4
description: 将视觉需求路由为普通图像生成或受控设定板生成。适用于角色、群像、道具、载具、场景和室内空间概念设计；不用于 Logo、UI、普通图片编辑或文档插图。
---

# 提示词生成图片 v0.4

## 优先级

1. 安全政策与图像工具限制。
2. 用户明确的任务类型与输出结构要求。
3. 当前选定模板的结构与约束。
4. 用户提供的主体事实信息。
5. 用户风格偏好。
6. 用户指定的主参考图。
7. 其他相关参考图。
8. 模型推断。

低等级信息不得覆盖高等级信息。文字高于图片；多张图片不可平均融合不同主体。

## 路由

普通概念图或普通图片：直接按用户文字生成。仅当用户明确请求设定板、排版图、三视图、拆解板、资料板或海报时进入模板路由。

- 单个角色主体（人物、动物、幻想生物、机器人或机甲生命体）：[character-sheet.md](references/character-sheet.md)
- 群像资料板、阵营资料、NPC 档案、多人角色库：[group-lineup-sheet.md](references/group-lineup-sheet.md)
- 群像宣传海报、阵营海报、KV：[group-poster-sheet.md](references/group-poster-sheet.md)
- 武器、装备、工具、饰品、机械物件或载具零件：[prop-sheet.md](references/prop-sheet.md)
- 汽车、飞机、火车、船舶、飞船、机甲载具的整体本体：[vehicle-sheet.md](references/vehicle-sheet.md)
- 整体环境、建筑外部、道路、机场、车站、港口或场地：[environment-sheet.md](references/environment-sheet.md)
- 驾驶舱、客舱、车厢、船舱、电梯、房间等封闭空间内部：[interior-sheet.md](references/interior-sheet.md)

当用户提供封闭空间但未说明内部或外部时，询问：“需要生成内部场景还是外部场景？”用户已明确时直接按对应路由执行。

若无法确定模板，不强制套用。询问：“你希望生成：1. 单张概念图；2. 场景设定板；3. 空间拆解板；4. 资产设计板？”

## 模板发送与变量绑定

读取选定 reference 的 `# Template variables`，仅用于确定槽位值；不得将该章节内容发送给图像工具。

发送给图像工具时，只发送该 reference 的 `# Image prompt` 下代码块内部内容。以该代码块为唯一提示词骨架：非占位文本、版式与约束不得拼接、删减、改写、扩写或替换。

仅绑定 `【】` 槽位：优先使用用户当前明确提供的信息，再使用用户指定主参考图可识别的信息，缺失时填写“未指定，由模型合理补全”。用户明确要求调整模板结构时，仅修改所指定结构；不得添加无关提示词。

按 [execution-protocol.md](references/execution-protocol.md) 执行变量绑定、模板冻结与发送；不得在冻结后重新润色提示词。按 [routing-rules.md](references/routing-rules.md) 处理类型冲突。

## 生成前检查

在调用图像工具前确认：

- 已读取正确的唯一 reference。
- 仅发送 `# Image prompt` 代码块。
- 仅绑定变量槽位，未添加模板外提示词。
- 主体身份、比例、材质与参考图保持一致。
- 版式和用户明确的结构要求均已满足。

若图像工具无法可靠生成中文文字，优先保留标题区域、标签位置与版式层级；文字可近似或留作后处理，不视为失败。

