---
name: yishui-juesezichan
description: |
  将人物照片、角色设定或自然语言人物描述，沉淀为可复用的 AI 角色资产系统（Character Bible），用于 AI 短剧、故事板、海报、职业 IP、数字人和连续镜头生成。自动完成角色 DNA、不可变视觉锚点、锁脸规则、标准三视图、动作姿态、表情库、细节资产、日常工作形象、日常生活形象与连续场景调用提示词。用户说“创建角色资产”“做人物资产图”“锁定这个人物”“生成三视图/动作/表情库”“做一套日常工作形象”“做一套日常生活形象”“后续都用这个角色”时触发。若用户提供真实人物照片，必须把照片作为身份最高优先级参考，不得重新设计成相似但不同的人；默认不把真实人物照片写入或发布到公开仓库。
---

# Yishui 角色资产 Skill

把“每次重新生一个人”，变成“调用同一个演员去演不同镜头”。

## 1. 适用任务

使用本 Skill 处理以下请求：

- 从真实人物照片建立职业 IP / 数字人角色资产。
- 从文字设定建立虚构角色 Character Bible。
- 生成角色资产总览板、三视图、动作库、表情库、细节库。
- 生成同一角色的“日常工作形象”“日常生活休闲形象”“演讲形象”“短剧角色形象”。
- 在后续海报、分镜、故事板、视频首尾帧中保持角色连续性。
- 把已有角色升级成稳定的角色 DNA + 视觉锚点系统。

不适合：只需要一张无连续性要求的普通人物图、单纯换背景、与角色一致性无关的图像任务。

## 2. 核心原则

### 2.1 身份参考优先级

当用户提供真实人物照片时：

1. 用户当前提供的身份母图（Identity Master Reference）优先级最高。
2. 已确认的角色 DNA 与视觉锚点次之。
3. 风格、服装、场景、动作只能在不破坏身份的前提下变化。
4. 禁止“优化”成另一张 AI 网红脸。

真实人物的脸部结构、年龄感、发际线、五官比例、基础发型特征不得被重新设计。

### 2.2 角色资产不是拼图

目标是专业 `Character Bible / Character Asset Sheet`，不是九宫格照片拼贴。

默认资产结构采用 **1 + 3 + 3 + 6 + 3**：

- 1 张 Hero 主视觉
- 3 张 Turnaround：正面 / 侧面 / 背面
- 3 张 Pose：角色代表动作
- 6 张 Detail：脸、发型、领口、腰部/配饰、手部/鞋履、关键道具
- 3 张 Expression：默认 + 两种关键情绪

职业 IP 可扩展为：

- 6 套 Daily Work Looks
- 6 个 Work Scenarios
- 6 个 Daily Life Looks
- 6 个 Life Scenarios

### 2.3 不可变视觉锚点

先提取 5–8 个视觉锚点，再写最终出图指令。

典型锚点：

- 身份锚点
- 脸部锚点
- 发型锚点
- 身形锚点
- 色彩锚点
- 服装锚点
- 配饰锚点
- 轮廓锚点

必须加入：

> These visual anchors are immutable. Do not redesign, simplify, replace, remove, or reinterpret them across views, poses, expressions, or scenes.

## 3. 标准工作流

### Step A — 解析输入

从用户输入提取：

- 角色姓名 / 代号
- 性别与大致年龄
- 时代 / 地域 / 职业身份
- 核心性格
- 外貌特征
- 基础发型
- 常用服装
- 关键道具
- 使用场景
- 目标视觉风格

缺失信息如果不影响第一版，可合理补全，不要频繁追问。

### Step B — 建立 Character DNA

按 `references/character-dna-template.md` 输出内部 DNA。

真实人物不要从敏感或不可见信息推断身份属性；只描述照片中可用于视觉一致性的外观与用户明确提供的职业定位。

### Step C — 建立视觉锚点

从 DNA 提取 5–8 个不可变锚点。

### Step D — 选择资产模式

根据任务自动路由：

- “角色资产 / Character Bible” → 资产总览板
- “三视图” → Front / Side / Back
- “日常工作” → Work Looks + Work Scenarios
- “日常生活” → Life Looks + Life Scenarios
- “故事板 / 分镜 / 视频” → Continuity Mode

### Step E — 生成出图指令

使用 `references/prompt-library.md` 对应模板，并始终附带一致性硬约束。

### Step F — 后续连续调用

一旦角色已建立，后续场景只允许修改：

- Scene
- Action
- Emotion
- Camera
- Lighting
- Wardrobe variant（如果用户允许）

身份与不可变锚点继续继承。

## 4. 真实人物锁脸规则

每次都应明确：

```text
Use the uploaded reference image as the exact identity master reference.
Preserve the subject's authentic facial structure, facial proportions, age impression,
hairline, eye shape, nose shape, mouth shape, jawline, skin tone, and recognizable identity.
Do not beautify into a different person. Do not create a lookalike.
Wardrobe, pose, setting and expression may change; identity may not.
```

若当前对话没有可用照片，但用户要求“用我/用这个人”，先要求用户上传身份参考图；不能假装仍持有不可用的图片。

## 5. 资产总览板版式

默认 16:9 横版，暖白 / 浅灰 / 冷蓝灰工作室底色，杂志级编辑设计。

推荐布局：

- 左 28–32%：Hero 全身或 3/4 主视觉 + 角色名 + 定位 + 3–5 个关键词
- 中上：正面 / 侧面 / 背面 / 可选 3/4 视图
- 中下：3–5 个角色动作
- 右上：超清脸部特写
- 右中：服装 / 发型 / 配饰 / 道具细节
- 右下：3–6 个表情

文字应少而准。中文生成不稳定时，优先减少正文，只保留短标签；必要时先生成纯视觉资产，再由排版工具加文字。

## 6. 日常工作形象模式

适用于专家、讲师、管理者、企业员工、职业 IP。

默认包含 6 类：

1. 会议汇报
2. 项目研讨
3. 团队管理 / 沟通
4. 日常办公
5. 外出调研
6. 培训 / 演讲 / 内容分享

服装不要求完全相同，但要形成同一人的稳定职业衣橱：正式商务、轻商务、培训演讲、外勤调研、内容创作等。

## 7. 日常生活休闲模式

默认包含 6 类：

1. 城市散步 / 出行
2. 咖啡馆 / 阅读
3. 运动 / 健身
4. 居家休闲
5. 旅行探索
6. 兴趣 / 摄影 / 社交

目标是“同一个人的生活面”，不是模特换装册。妆容、发型与身份应自然延续。

## 8. 连续性硬约束

所有连续角色任务必须附带：

```text
CRITICAL CHARACTER CONSISTENCY RULES:
This is one single character shown multiple times, not multiple similar-looking people.
Every depiction must preserve the same identity, facial bone structure, facial proportions,
eye shape, nose shape, mouth shape, age impression, body proportions, skin tone, hairline,
hairstyle construction, signature accessories and immutable visual anchors.
Front, side and back views must be anatomically and materially consistent.
Do not beautify or redesign the face between panels.
Do not create clones with slightly different faces.
Only pose, camera angle, expression, allowed wardrobe variant, scene and lighting may change.
```

负面约束：

```text
NEGATIVE:
different character, multiple identities, face drift, different facial structure,
random hairstyle, unexplained age change, body-type drift, random accessories,
missing signature anchors, clone faces, inconsistent scale, bad hands, extra fingers,
duplicate limbs, cropped feet, floating props, low detail, blurred face,
cheap collage aesthetic, game UI, watermark, logo, unreadable text.
```

## 9. 输出行为

当用户只是要“生成图片”时：直接构建内部 DNA 和提示词并调用图像生成，不必把完整提示词先展示给用户。

当用户要“提取指令词 / 做 Skill / 做模板”时：输出结构化 DNA、视觉锚点和可复用提示词。

当用户要求修改现有角色图时：优先继承当前角色身份，不重建角色。

## 10. 隐私与发布边界

- 真实人物照片默认只作为运行时参考，不打包进公开 Skill 仓库。
- 除非用户明确要求公开某张真实照片，否则 README、examples、docs 不嵌入真实身份母图。
- 示例应使用文字占位或匿名虚构角色。
- 不在仓库中写入用户身份证明、联系方式、账户信息或其他不必要的个人资料。

## 11. 参考文件

- `references/character-dna-template.md` — Character DNA 模板
- `references/prompt-library.md` — 资产板 / 工作 / 生活 / 连续镜头模板
- `references/quality-gates.md` — 出图验收与返修规则
- `evals/trigger_cases.json` — 路由测试
