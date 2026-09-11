# yishui-juesezichan

> 你做 AI 短剧、海报或职业 IP 时，最难的往往不是“生成一个好看的人”，而是 **下一张图还是同一个人**。
>
> `yishui-juesezichan` 把一张人物照片或一段角色设定沉淀成可复用的 Character Bible：角色 DNA、不可变视觉锚点、锁脸规则、三视图、动作、表情、细节、工作形象、生活形象，以及后续连续镜头调用规则。

**中文** | [English](#english)

## 为什么值得用

普通提示词往往把角色“描述一次就结束”。这个 Skill 把人物当成长期可调用的演员资产：

- **先锁身份**：真实人物照片作为 Identity Master Reference，不重新设计成“相似脸”。
- **再建 DNA**：脸、发型、身形、衣橱、配饰、轮廓全部结构化。
- **再做资产**：Hero + 三视图 + 动作 + 表情 + 细节。
- **最后连续调用**：后续只改场景、动作、情绪、镜头与允许的服装变体。

适合 AI 短剧、故事板、影视预演、职业 IP、数字人、人物海报与连续视觉生产。

## 安装

```bash
npx skills add isllyy/manju
```

## 你可以这样说

- “用这张照片建立我的人物资产，以后所有图都锁定这个人。”
- “给这个角色做一张 16:9 的 Character Bible。”
- “生成正面、侧面、背面三视图，再补动作和表情库。”
- “给伊水生成一套日常工作形象。”
- “再做一套日常生活休闲形象，但仍然是同一个人。”
- “沿用刚才角色，生成雨夜街头的电影分镜。”

## 核心资产模型

默认使用 `1 + 3 + 3 + 6 + 3`：

| 模块 | 数量 | 用途 |
|---|---:|---|
| Hero | 1 | 第一视觉印象 |
| Turnaround | 3 | 正 / 侧 / 背结构连续性 |
| Pose | 3 | 角色动作语言 |
| Detail | 6 | 脸、发型、服装、配饰、道具 |
| Expression | 3+ | 表演一致性 |

职业 IP 还可以扩展为 6 套工作形象 + 6 个工作场景；生活 IP 可扩展为 6 套休闲形象 + 6 个生活场景。

## 关键设计：不可变视觉锚点

Skill 会从人物中提取 5–8 个不能随意漂移的锚点，例如：

`脸部结构 → 发型轮廓 → 年龄感 → 身形比例 → 核心服装结构 → 标志配饰 → 主色体系 → 剪影特征`

后续镜头只允许改变场景、动作、情绪、镜头、光线，以及用户明确允许的服装变体。

## 真实人物隐私

这个仓库 **默认不包含任何真实人物身份母图**。

真实照片应在使用 Skill 时由用户提供，只作为运行时身份参考。除非人物本人明确要求公开，否则不要把原始职业照、身份证明、联系方式或其他个人信息提交到公共仓库。

## 文件结构

```text
yishui-juesezichan/
├── SKILL.md
├── README.md
├── LICENSE
├── references/
│   ├── character-dna-template.md
│   ├── prompt-library.md
│   └── quality-gates.md
└── evals/
    └── trigger_cases.json
```

## 设计来源与沉淀

本 Skill 来自真实的角色资产工作流迭代：从职业母图开始，依次建立专业角色资产板、日常工作形象、日常生活休闲形象，并进一步抽象出 Character DNA、视觉锚点和连续镜头规则。

发布流程参考 `joeseesun/qiaomu-skill-publisher` 的实践：严格 YAML frontmatter、README 产品化、一行安装和发布后的真实安装验证。参考项目本身不被复制到本仓库。  
Reference: https://github.com/joeseesun/qiaomu-skill-publisher

## 限制

- 图像模型对中文长文本的稳定性有限，资产板内建议使用短标签，复杂中文后期排版。
- 三视图是生成式视觉参考，不是精确 CAD / 3D 模型拓扑。
- 真实人物的一致性上限仍取决于所用图像模型和参考图质量。
- 若当前会话没有可用身份参考图，不应假装可以精确复原真人。

## License

MIT — 代码与 Skill 文本可复用；用户运行时提供的真人照片与生成的人物肖像不因本 License 自动获得再授权。

---

<a name="english"></a>
## English

`yishui-juesezichan` turns a portrait or character brief into a reusable Character Bible for consistent AI visual production.

It creates a structured Character DNA, immutable visual anchors, identity-lock rules, turnaround views, poses, expressions, detail studies, work/lifestyle looks, and continuity prompts for later scenes.

### Install

```bash
npx skills add isllyy/manju
```

### Natural-language triggers

- “Build a reusable character asset from this portrait.”
- “Create front / side / back views for the same person.”
- “Make a daily work-look board while preserving identity.”
- “Use the established character in a new cinematic scene.”

### Privacy

Real-person identity reference photos are runtime inputs and should not be committed to a public repository unless the person explicitly asks for them to be published.
