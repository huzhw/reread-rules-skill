# JUNCTION 说明 — reread-rules

> 本目录已与全局 skill 目录建立 junction，**实时双向同步，改哪边都一样**。

## 指向关系

| 项 | 路径 |
|----|------|
| 全局路径（junction，Claude Code） | `C:\Users\Administrator\.claude\skills\reread-rules` |
| 全局路径（junction，DSH） | `C:\Users\Administrator\.dsh\skills\reread-rules` |
| 全局路径（junction，Codex） | `C:\Users\Administrator\.codex\skills\reread-rules` |
| 全局路径（junction，Zcode） | `C:\Users\Administrator\.zcode\skills\reread-rules` |
| 实际目录（F 仓库） | `F:\idea-workspase-skills\reread-rules` |
| 更名记录 | 原 `reread-claude-md`，2026-08-28 更名为 `reread-rules` |

## 说明

- 全局两个目录都是指向 F 仓库的 junction，两侧是**同一个目录**，不是副本。
- 修改 F 仓库，全局立刻生效；在全局路径下改文件，F 仓库同步变化。
- 日常维护只改 F 仓库（git 提交推送后全局自动一致），**不需要手动复制同步**。

## 检查是否正常

```bash
cmd /c dir "C:\Users\Administrator\.claude\skills" | findstr reread-rules
cmd /c dir "C:\Users\Administrator\.dsh\skills"    | findstr reread-rules
cmd /c dir "C:\Users\Administrator\.codex\skills" | findstr reread-rules
cmd /c dir "C:\Users\Administrator\.zcode\skills" | findstr reread-rules
```

正常应显示 `<JUNCTION>  ...  reread-rules`。

## 回滚方法（恢复成独立副本）

```bat
rd "C:\Users\Administrator\.claude\skills\reread-rules"
rd "C:\Users\Administrator\.dsh\skills\reread-rules"
rd "C:\Users\Administrator\.codex\skills\reread-rules"
rd "C:\Users\Administrator\.zcode\skills\reread-rules"
```

> 注意：`rd` 不要加 `/s`，否则可能递归进 F 源目录。删除 junction 只删链接，不删 F 源目录。

## 本 skill 特殊差异

- 更名只动名字与描述，规则内容（CLAUDE.md/AGENTS.md 重载逻辑）不变。
- 更名前全局原目录是独立 git checkout，junction 后以 F 仓库为准；备份位于 `F:\idea-workspase-skills\_skills_backup_20260802\reread-claude-md`。