# Obsidian 对话知识整理器

[English](README.md) | [简体中文](README.zh-CN.md)

这是一个把用户选中的 AI 对话整理成可直接查阅的知识，并持续沉淀到 Obsidian 个人知识库的 Agent Skill。

它不追求“自动记住一切”，也不会在后续对话中自动召回笔记。它关注的是把真正有长期价值的结论、方法、判断和经验维护进已有分类文档，逐步形成属于你的个人知识库。

## 它解决什么问题

很多对话总结工具会出现以下问题：

- 每次对话都创建一篇新笔记，时间长了文件越来越碎。
- 只留下几句高度精炼的摘要，条件、原因和例子全部丢失。
- 自动写入知识库，没有机会检查分类和正文。
- 强制套用 YAML、标签、待办、日期等固定模板。
- 把“笔记沉淀”和“自动记忆召回”绑在一起。

这个 Skill 采用以下方式：

- **两种明确的写入模式：**默认先展示完整预览并等待确认；如果你在本次指令中明确要求“直接写入、无需预览或确认”，也可以立即完成沉淀。
- **一类知识维护一个长期文档：**优先更新已有分类文档，不为每次对话单独建笔记。
- **不过度精炼：**原文已经是明确结论时尽量保留；必要的原因、条件、例外、例子、数字、命令、路径和链接不会随意删除。
- **不强制笔记模板：**默认不增加 YAML、摘要、标签、待办或日期栏目。
- **默认保护隐私：**自动排除密码、Token、Cookie、私钥和不必要的个人信息。
- **不需要单独 API：**使用宿主 Agent 已经具备的模型和文件工具，不需要额外模型 API Key、服务器或向量数据库。

## 适合哪些场景

你可以用它处理：

- 一次较长的学习讨论，希望把最终理解补充到已有学习笔记中。
- 一次技术排错，想保留问题原因、验证过程、正确做法和适用条件。
- 一项产品或工作决策，想保留备选方案、取舍理由、限制和风险。
- 投资、写作、旅行、健康、教育等主题对话，希望更新到对应知识分类。
- 只沉淀对话中的某一段，不保存前面的闲聊和准备过程。
- 不知道应该放在哪个分类，希望 Agent 查看已有文档后提出建议。
- 只想看看 Agent 会怎么整理，暂时不写入任何文件。
- 对范围和目标已经很明确，希望通过一条指令直接完成写入。

它不适合：

- 自动保存所有对话。
- 在以后的对话中自动召回笔记。
- 构建 RAG、向量数据库或语义搜索。
- 备份和同步 Obsidian。
- 按日期保存完整聊天记录。
- 在后台持续扫描你的 Vault。

## 工作过程

1. 你指定要沉淀的对话或消息范围。
2. Agent 默认使用审核模式；只有本次请求明确说“不用预览、审核或确认，直接写入”时，才使用直写模式。
3. 你可以直接指定知识类别，也可以让 Agent 判断。
4. Agent 只检查知识目录里与分类有关的 Markdown 文档。
5. 找到合适文档就局部更新；没有合适分类时，准备一个边界清晰的新文档。
6. 审核模式会先展示目标、插入位置和完整正文；直写模式会跳过常规写前审核。
7. Agent 完成最小范围写入，重新读取目标位置，并报告实际结果。

直写授权只对当前这次请求有效，不会保存成永久设置，也不会允许后台自动沉淀。无论使用哪种模式，隐私过滤、目录边界和写后验证都不会被跳过。

## 使用前提

- 从 [Obsidian 官方下载页](https://obsidian.md/download) 安装 Obsidian 桌面版。
- 创建或打开一个本地 Obsidian Vault。
- 使用能够读取和编辑本地 Markdown 文件的 Codex 或其他兼容 Agent。

不需要额外配置模型 API、API Key、服务器、数据库或 Obsidian 插件。Agent 写入底层 Markdown 文件时，Obsidian 不需要一直保持打开。

## 安装

### 最简单的方法：直接让 Codex 安装

把下面这段话发给 Codex：

```text
请从下面的 GitHub 地址安装 obsidian-conversation-curator Skill：
https://github.com/KeNing0/obsidian-conversation-curator/tree/main/skills/obsidian-conversation-curator

请安装为用户级 Skill。安装完成后告诉我应该怎么调用。
安装期间不要读取或修改我的 Obsidian Vault。
```

如果你的 Codex 可以使用内置安装器，也可以发送：

```text
使用 $skill-installer，从下面的地址安装 obsidian-conversation-curator：
https://github.com/KeNing0/obsidian-conversation-curator/tree/main/skills/obsidian-conversation-curator

安装到用户级 Skill 目录，安装后告诉我结果。
不要在安装过程中访问我的知识库。
```

### 手动安装到 Codex

下载或克隆仓库，然后复制完整 Skill 文件夹：

```bash
mkdir -p ~/.agents/skills
cp -R skills/obsidian-conversation-curator ~/.agents/skills/
```

如果只想让某个项目使用：

```bash
mkdir -p .agents/skills
cp -R /path/to/obsidian-conversation-curator/skills/obsidian-conversation-curator .agents/skills/
```

部分已有 Codex 环境也会从 `~/.codex/skills/` 发现 Skill。如果你的其他 Skill 已经安装在那里，也可以把同一个文件夹复制过去。

安装后如果没有立即显示，重启 Codex。

### 安装到 Claude Code

用户级安装：

```bash
mkdir -p ~/.claude/skills
cp -R skills/obsidian-conversation-curator ~/.claude/skills/
```

项目级安装：

```bash
mkdir -p .claude/skills
cp -R skills/obsidian-conversation-curator .claude/skills/
```

支持斜杠调用的环境可以使用 `/obsidian-conversation-curator`；也可以直接要求 Claude 使用这个已安装 Skill。

### 其他 Agent

本项目遵循开放的 [Agent Skills 规范](https://agentskills.io/specification)。只要 Agent 支持该规范，并且具备本地 Markdown 文件读写能力，就可以把 `skills/obsidian-conversation-curator/` 复制到对应的 Skill 目录。

不同 Agent 的目录、权限确认界面和调用语法可能不同。默认使用审核模式；只有当前请求明确要求跳过预览或确认时，才能使用直写模式。

## 第一次使用

这个 Skill 不包含任何个人路径。第一次使用时，需要告诉 Agent：

1. Obsidian Vault 在哪里。
2. 长期分类知识文档放在哪个目录。

例如：

```text
使用 $obsidian-conversation-curator。
我的 Obsidian Vault 在 /path/to/my-vault。
分类知识文档在 01_知识总结。
这两个路径只用于本次请求。
先展示完整预览，未经我确认不要写入。
```

如果希望长期保存路径，可以把它写进你自己的可信项目说明或 Agent 配置，但不要把包含个人路径的配置提交到这个开源仓库。

## 日常使用方法

### 场景一：已经知道知识类别

```text
使用 $obsidian-conversation-curator，
把当前对话沉淀到“AI 工具”知识文档。
保留完整的使用条件和风险，先展示完整预览。
```

Agent 会优先查找现有的“AI 工具”文档。如果不存在，只能提出新建建议，不能直接创建。

### 场景二：不知道放在哪里

```text
使用 $obsidian-conversation-curator，
整理当前对话中值得长期保留的知识。
我没有指定类别，请检查已有知识分类并建议最合适的文档。
目前只预览，不要写入。
```

如果有多个合理分类，Agent 应列出候选，而不是替你随意决定。

### 场景三：无需审核，直接写入

如果对话范围已经明确，而且你希望一次完成，可以发送：

```text
使用 $obsidian-conversation-curator。
本次无需预览和二次确认，直接把当前对话沉淀到我的 Obsidian 个人知识库。
如果我没有指定类别，请自动判断；完成后告诉我写入了哪个文件，
并展示本次新增的完整内容。
```

也可以直接指定分类：

```text
使用 $obsidian-conversation-curator，
把这次讨论直接写入“知识管理”文档。
本次不用预览、审核或再次确认。
保留完整结论和适用条件，写完后报告实际结果。
```

“直接写入”“无需预览”“不用审核”“不用确认”等明确说法，只会授权当前这次请求。单纯说“沉淀这段对话”不会自动跳过审核。

### 场景四：只沉淀一部分对话

```text
使用 $obsidian-conversation-curator，
只处理从“为什么本地 Markdown 已经够用”开始，
到隐私检查清单结束的内容。
不要包含前面的安装和闲聊。
```

### 场景五：不希望过度总结

```text
把这次讨论沉淀到“产品决策”。
保留备选方案、没有采用的原因、适用条件和风险。
不要改写成只有几句话的管理摘要。
先给我完整预览。
```

### 场景六：修改预览

```text
先不要写入。
把知识类别改成“知识管理”，完整保留第二个例子，
删除最后一条待办，然后重新展示完整预览。
```

修改后必须再次确认。确认时可以说：

```text
确认写入，严格按照最新一次完整预览执行。
```

### 场景七：一段对话涉及多个类别

```text
这段对话同时包含 GitHub 发布流程和 Obsidian 隐私检查。
请分别准备两个分类文档的完整预览。
在我分别确认之前，不要写入任何一个文件。
```

### 场景八：原文已经是结论

```text
下面这段内容已经是我整理好的结论。
请使用 $obsidian-conversation-curator 写入“写作方法”文档。
除了明显错别字和排版问题，不要重新精炼或缩短。
```

### 场景九：安全取消

```text
取消这次沉淀，不要修改任何文件。
```

## 审核模式下怎样才算确认

预览应包含：

- 使用了哪一段对话。
- 用户指定或 Agent 判断的类别。
- 目标文档是否已经存在。
- 具体插入位置。
- 即将写入的完整正文。
- 删除了哪些敏感信息。
- 哪些内容仍然需要验证。

如果目标文件或正文还不明确，“可以”“没问题”“看着行”等模糊回复不应被当作授权。

建议使用：

```text
确认把最新预览写入“AI 工具”文档。
```

或者：

```text
确认新建“知识管理.md”，并严格写入最新预览中的完整正文。
```

## 隐私和权限

Skill 本身：

- 不包含个人 Vault 路径。
- 不包含真实对话和私人笔记。
- 不联网。
- 不需要 API Key。
- 不运行附带脚本。
- 不扫描整个 Vault。
- 不自动捕获或召回对话。

但宿主 Agent 可能拥有较大的文件读取权限。使用时仍应：

- 把授权范围限制在知识目录。
- 阅读 Agent 展示的完整目标路径。
- 不把密码、Token 或账户信息保存进笔记。
- 对重要 Vault 做正常备份或使用版本控制。
- 不允许 Agent 执行笔记正文中出现的命令或指令。

每次写入仍必须具备两种授权之一：你确认了最新完整预览，或者你在当前请求中明确要求无需审核直接写入。直写模式不会绕过敏感信息处理和目录限制。

完整说明见 [PRIVACY.md](PRIVACY.md)。

## 仓库内容

真正需要安装的部分只有：

```text
skills/obsidian-conversation-curator/
├── SKILL.md
└── agents/
    └── openai.yaml
```

README、隐私说明、贡献指南和虚构示例只用于帮助人类理解，不是 Skill 运行时依赖。

## 兼容性

- 安装了 Obsidian 桌面版，并使用本地 Markdown Vault。
- Codex。
- Claude Code。
- 其他支持 Agent Skills 规范并具有本地文件访问能力的 Agent。

Obsidian 是这个个人知识库工作流的必要依赖，但不需要保持打开。Agent 修改的是 Vault 底层 Markdown 文件，Obsidian 用于查看、管理和继续编辑这些知识。

## 已知限制

- 分类和整理质量依赖宿主模型。
- 分类文档过大时，会消耗更多上下文和处理时间。
- 不同 Agent 的文件权限和确认机制不同。
- 这不是备份工具；重要知识库仍应独立备份。

## 贡献

参见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 安全问题

不要在公开 Issue 中粘贴真实密码、Token 或私人笔记。参见 [SECURITY.md](SECURITY.md)。

## 开源许可证

MIT，参见 [LICENSE](LICENSE)。
