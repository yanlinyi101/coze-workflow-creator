# coze-workflow-creator

通过 AI 对话，帮助你在 Coze 平台设计并生成可直接粘贴的工作流节点 JSON。

**无需 API 权限，无需编程知识，Ctrl+V 即可完成工作流搭建。**

---

## 工作原理

Coze 支持右键复制节点获取完整 JSON，在画布上粘贴即可还原节点及连线。本项目提供一个 Claude Skill，由 AI 引导你描述需求，生成符合 Coze 格式的节点 JSON。

---

## 快速开始

**1. 安装 Skill**

将 `skill.md` 文件复制到你的 Claude Code skills 目录：

```bash
# macOS / Linux
cp skill.md ~/.claude/skills/coze-workflow-creator.md
```

**2. 触发 Skill**

在 Claude Code 中输入：

```
/coze-workflow-creator
```

**3. 跟随对话**

AI 会逐步引导你完成：
- 描述工作流需求
- 确认流程设计
- 获取可粘贴的节点 JSON

**4. 在 Coze 中粘贴**

在 Coze 工作流画布空白处 Ctrl+V，节点即出现。

---

## 节点样本库

`samples/nodes/` 目录包含已验证的节点 JSON 样本：

| 节点类型 | 文件 | 状态 |
|----------|------|------|
| 大模型 | `samples/nodes/llm.json` | ✅ 已验证 |
| 代码 | `samples/nodes/code.json` | ✅ 已验证 |
| 选择器（条件分支） | `samples/nodes/condition.json` | ✅ 已验证 |
| HTTP 请求 | `samples/nodes/http.json` | ✅ 已验证 |
| 插件调用 | `samples/nodes/plugin.json` | ✅ 已验证 |

更多节点类型持续补充中，欢迎贡献样本。

---

## 自排障 SOP

如果粘贴 JSON 后出现问题，按以下步骤排查：

### 问题 A：粘贴后没有节点出现

1. 告知 AI："粘贴后无节点生成"
2. AI 会将 JSON 拆分，发送小段让你测试，通过二分法定位问题节点
3. 确认问题节点类型后，执行通用修复步骤

### 问题 B：节点出现但运行报错

1. 将 Coze 报错信息告知 AI
2. AI 定位问题节点，进行单点排障

### 通用修复步骤（确认问题节点后）

1. 在 Coze 中**手动创建同类型节点**，配置好所有参数
2. **右键该节点 → 复制**
3. 粘贴到文本编辑器，将内容发给 AI
4. AI 基于最新格式重新生成工作流节点

### 贡献更新的样本（可选）

帮助社区用户：将最新节点 JSON 更新到 `samples/nodes/` 对应文件，提交 PR，注明 Coze 版本和采集日期。详见 [CONTRIBUTING.md](./CONTRIBUTING.md)。

---

## 贡献节点样本

查看 [CONTRIBUTING.md](./CONTRIBUTING.md) 了解如何添加或更新节点样本。

---

## License

MIT
