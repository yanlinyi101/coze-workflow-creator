# coze-workflow-creator

[中文](./README.md) | English

> Why learn to build Coze workflows yourself? Teach [openclaw](https://openclaw.ai) or Claude Code this skill, describe what you need, and let the AI Agent build your Coze workflow for you.

Build Coze platform workflows through AI conversation — generates paste-ready node JSON automatically.

**No API credentials. No coding knowledge. Just click a button and paste.**

---

## How It Works

Coze supports right-clicking nodes to copy their full JSON, which can be pasted back onto the canvas to restore nodes and edges. This project provides a Claude Skill that guides you through describing your requirements, generates valid Coze-format node JSON, and delivers it via an HTML helper page that writes clean plain text to your clipboard.

---

## Quick Start

**1. Install the Skill**

Copy `skill.md` to your Claude Code skills directory:

```bash
# macOS / Linux
cp skill.md ~/.claude/skills/coze-workflow-creator.md
```

**2. Trigger the Skill**

In Claude Code, type:

```
/coze-workflow-creator
```

**3. Follow the Conversation**

The AI will guide you through:
- Describing your workflow requirements
- Confirming the flow design
- Generating node JSON and automatically opening the helper page

**4. Paste into Coze**

The AI opens a helper page in your browser. Click the "**Copy Workflow JSON**" button, then Command+V (Mac) or Ctrl+V (Windows) on the Coze workflow canvas. Your nodes appear instantly.

> ⚠️ **Important**: Do not copy JSON directly from the Claude chat window. Always use the helper page button. See below for why.

---

## Why the Helper Page?

When you copy JSON from a Claude Code code block, the clipboard receives two formats simultaneously:
- `text/plain` — pure JSON (correct)
- `text/html` — JSON wrapped in syntax-highlighting `<span>` tags (broken)

Coze's paste handler reads `text/html` first, resulting in HTML tag garbage that it cannot parse — nodes silently fail to appear.

The helper page uses `navigator.clipboard.writeText()` to write **only** plain text to the clipboard, eliminating the problem entirely.

**Alternative (macOS Terminal):**
```bash
pbpaste | pbcopy
```
Running this in Terminal strips all non-plain-text clipboard formats before you paste.

---

## Known Paste Failure Traps

The following JSON format issues cause silent paste failure (no error message, no nodes appear):

| Issue | Bad Example | Fix |
|-------|-------------|-----|
| `settingOnError` contains `switch` field | `"settingOnError":{"switch":true,...}` | Remove the `switch` field |
| `outputs` contains `required` field | `"required":false` | Remove the `required` field |
| Code node `_temp.externalData` contains `skills` | `"skills":[]` | Remove the `skills` field |
| Clipboard contains HTML MIME type | Copying directly from a code block | Use the helper page button |

---

## Node Sample Library

The `samples/nodes/` directory contains verified node JSON samples:

| Node Type | File | Status |
|-----------|------|--------|
| LLM | `samples/nodes/llm.json` | ✅ Verified |
| Code | `samples/nodes/code.json` | ✅ Verified |
| Condition (branch) | `samples/nodes/condition.json` | ✅ Verified |
| HTTP Request | `samples/nodes/http.json` | ✅ Verified |
| Plugin | `samples/nodes/plugin.json` | ✅ Verified |

More node types coming soon. Contributions welcome.

---

## Troubleshooting SOP

If something goes wrong after pasting, follow these steps:

### Problem A: No nodes appear after pasting

1. Confirm you used the helper page button (not copied directly from the Claude chat)
2. Tell the AI: "No nodes appeared after pasting"
3. The AI will split the JSON into smaller chunks and use binary search to isolate the problematic node
4. Once the problem node is identified, follow the general fix steps below

### Problem B: Nodes appear but fail at runtime

1. Share the Coze error message with the AI
2. The AI will pinpoint the failing node and debug it

### General Fix Steps (after identifying the problem node)

1. **Manually create the same node type** in Coze and configure it fully
2. **Right-click the node → Copy**
3. Paste into a text editor and send the content to the AI
4. The AI regenerates the workflow using the up-to-date format

### Contributing Updated Samples (optional)

Help the community: update the latest node JSON in `samples/nodes/`, submit a PR, and note the Coze version and capture date. See [CONTRIBUTING.md](./CONTRIBUTING.md).

---

## Contributing Node Samples

See [CONTRIBUTING.md](./CONTRIBUTING.md) for how to add or update node samples.

---

## License

MIT
