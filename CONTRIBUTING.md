# 贡献指南

感谢你为 coze-workflow-creator 贡献节点样本！

---

## 如何添加新节点样本

### 1. 从 Coze 导出节点 JSON

1. 在 Coze 工作流画布中，添加目标节点类型
2. 配置好该节点的**所有必要参数**（不要留空）
3. 右键该节点 → **复制**
4. 粘贴到文本编辑器，保存原始 JSON

### 2. 创建样本文件

在 `samples/nodes/` 目录下创建或更新 `[节点类型].json`，使用以下格式：

```json
{
  "meta": {
    "node_type": "节点类型英文名",
    "description": "节点用途的中文说明",
    "collected_date": "YYYY-MM-DD",
    "coze_note": "采集时的配置说明，帮助他人复现",
    "fields": {
      "字段名": "该字段的用途说明（重要字段都注释）"
    }
  },
  "node": { 从 Coze 复制的原始节点 JSON 粘贴在这里（替换这段注释） }
}
```

### 3. 验证 JSON 格式

```bash
python3 -m json.tool samples/nodes/[节点类型].json
```

输出无报错即为合法 JSON。

### 4. 更新 skill.md 中的内嵌样本（如为 P0 节点）

如果你更新的是大模型节点（llm）或代码节点（code），请同步更新 `skill.md` 中"节点 JSON 样本库"部分对应的 JSON 内容。

### 5. 提交 PR

PR 标题格式：`feat: add [节点类型] node sample` 或 `fix: update [节点类型] node sample`

PR 描述请包含：
- Coze 版本（在 Coze 界面设置中查看）
- 采集日期
- 节点配置说明（方便他人验证）

---

## 样本文件命名规范

| 节点类型 | 文件名 |
|----------|--------|
| 大模型 | `llm.json` |
| 代码 | `code.json` |
| 选择器（条件分支） | `condition.json` |
| HTTP 请求 | `http.json` |
| 插件调用 | `plugin.json` |
| 循环 | `loop.json` |
| 批处理 | `batch.json` |
| 变量聚合 | `variable_aggregation.json` |
| 意图识别 | `intent.json` |
| 异步任务 | `async_task.json` |
| 子工作流 | `subworkflow.json` |
| 输入 | `input.json` |
| 输出 | `output.json` |
| SQL 自定义 | `sql.json` |
| 其他 | 使用 Coze 界面显示的英文节点名（小写，下划线分隔） |

---

## 注意事项

- 提交前请确认 JSON 中**不包含任何个人信息**（API Key、用户 ID、私人数据等）
- `node` 字段中的敏感变量值可替换为占位符，如 `"YOUR_VALUE_HERE"`
- 样本应尽可能通用，避免依赖特定业务逻辑
