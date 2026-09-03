# reread-rules

重新加载全局和项目级规则文件（Claude Code 的 CLAUDE.md，DSH 侧为硬链接的 AGENTS.md）的技能。

## 相关技能

- [git-commit](https://github.com/huzhw/git-commit-skill)：Git 提交规范
- [daily-record-gitlab-md](https://github.com/huzhw/daily-record-gitlab-md-skill)：日报记录
- [daily-merge-gitlab-excel](https://github.com/huzhw/daily-merge-gitlab-excel-skill)：日报合并
- [claude-code-token-3000](https://github.com/huzhw/claude-code-token-3000-skill)：Claude Code API Token 切换
- [code-check](https://github.com/huzhw/code-check-skill)：增量代码隐患检查
- [deepseek-harness-settings-curator](https://github.com/huzhw/deepseek-harness-settings-curator)：DSH 模型配置梳理
- [agent-config-sync-check](https://github.com/huzhw/agent-config-sync-check)：四端同步守卫：链接/硬链接/README 同步检查与修复
- [coding-rules](https://github.com/huzhw/coding-rules)：编码规则库（独立仓库，非 skill）
- [service-manager](https://github.com/huzhw/service-manager)：服务管理器（关联仓库，非 skill）

---

## 核心机制：用"亲爱的架构师"当上下文压缩探针

全局 CLAUDE.md 要求 AI 回复开头加"亲爱的架构师"。**这句不是客套——是特意设计的探针。** 当 AI 不再说这句话，说明上下文已被压缩、规则已经丢了。

发现漏了这句 → 说"规则丢了" → AI 重读规则文件 → 规则恢复。

## 解决了什么问题

长对话中上下文逐步压缩，规则文件里的规则可能在多轮后被丢弃，AI 行为出轨。这个技能提供一键重载：说句触发词，AI 重新加载规则文件。

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
3. AI 读取 `~/.claude/CLAUDE.md`（DSH 侧 `~/.dsh/AGENTS.md`）+ `<项目>/CLAUDE.md`
4. 关键规则重新生效
5. 后续回复恢复正常

## 触发词

"重新读 claude.md"、"重读规则"、"规则丢了"、"规则呢"、"reread"

## 安装

```bash
git clone https://github.com/huzhw/reread-rules-skill.git ~/.claude/skills/reread-rules
```

重启 Claude Code 生效。

## 许可

MIT