# reread-claude-md

重新加载全局和项目级 CLAUDE.md 规则的 Claude Code 技能。

## 核心机制：用"亲爱的架构师"当上下文压缩探针

全局 CLAUDE.md 要求 AI 回复开头加"亲爱的架构师"。**这句不是客套——是特意设计的探针。** 当 AI 不再说这句话，说明上下文已被压缩、规则已经丢了。

发现漏了这句 → 说"规则丢了" → AI 重读两份 CLAUDE.md → 规则恢复。

## 解决了什么问题

Claude Code 长对话中上下文逐步压缩，CLAUDE.md 里的规则可能在多轮后被丢弃，AI 行为出轨。这个技能提供一键重载：说句触发词，AI 重新加载规则文件。

## 为什么 Skill 比文件靠谱

| 方式 | 可靠性 |
|------|--------|
| 靠 AI 记忆 | ❌ 上下文压缩就忘 |
| 项目 memory 文件 | ❌ 一样会被压缩 |
| 用户手动提醒 | ⚠️ 得打一堆字说明 |
| **Skill 外部触发** | ✅ 系统级加载，不受对话压缩影响 |

## 怎么工作

1. 发现"亲爱的架构师"没出现 → 上下文压缩了
2. 说"规则丢了"
3. AI 读取 `~/.claude/CLAUDE.md` + `<项目>/CLAUDE.md`
4. 关键规则重新生效
5. 后续回复恢复正常

## 触发词

"重新读 claude.md"、"重读规则"、"规则丢了"、"规则呢"、"reread"

## 安装

```bash
git clone https://github.com/huzhw/reread-claude-md-skill.git ~/.claude/skills/reread-claude-md
```

重启 Claude Code 生效。

---

## 相关技能

- [git-commit](https://github.com/huzhw/git-commit-skill)：Git 提交规范
- [coding-rules](https://github.com/huzhw/coding-rules)：AI 编码协作规范
- [daily-record](https://github.com/huzhw/daily-record-skill)：日报记录
- [daily-merge](https://github.com/huzhw/daily-merge-skill)：日报合并
- [token-3000](https://github.com/huzhw/token-3000-skill)：API 一键切换（公司免费 ↔ 自己花钱）

## 许可

MIT
