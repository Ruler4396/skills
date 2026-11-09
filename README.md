# skills

个人 skill 安装仓库。每个 skill 一份 Markdown，写给 AI 读的，放在 `skills/<name>/` 下，与具体 Agent 无关。**本文件只做索引；规则不写在这里。**

## 有哪些

| skill | 管什么 | 状态 |
| --- | --- | --- |
| [`leekinbun`](skills/leekinbun/SKILL.md) | **开发任务怎么执行**：需求穿透澄清与类比复述、MVP 边界、分层测试与回归锁、结论先行汇报 | Active，v3.8（2026-10-31）。治理见 [`skills/leekinbun/UPDATE.md`](skills/leekinbun/UPDATE.md) |
| [`anomaly`](skills/anomaly/SKILL.md) | **复杂判断怎么想**：对齐 → 十五问全扫（元方法层）→ 角色反转与盲区自检 → 三池收敛 → 三层下沉 → 四个停点 | Active，v6（2026-10-26），试用中。暂未立治理文档 |

两者分工：一个管执行，一个管思考；不重叠，也不互相引用——各自独立演进，避免规则在两处各存一份。

## 目录结构

```
skills/<name>/SKILL.md     # skill 正文，唯一权威载体
skills/<name>/UPDATE.md    # 可选：该 skill 自己的更新治理，不适用于仓库内其他 skill
AGENTS.md                  # 可选模板：用户级指令文件，只引入 skill，不含规则副本
```

## 怎么装

通用做法：把 `skills/<name>/` 整个目录复制到目标 Agent 的用户级 skills 目录，保持 `<name>/SKILL.md` 的形状。

| Agent | 用户级 skills 目录 |
| --- | --- |
| ZCode | `~/.agents/skills/` |
| Qoder | `~/.qoder-cn/` |
| Claude Code | `~/.claude/skills/` |
| WorkBuddy | `~/.workbuddy/skills/` |

### 只认 skills 目录的 Agent（如 ZCode、Claude Code、WorkBuddy）

```
~/.agents/skills/<name>/SKILL.md
```

直接复制即可，不需要 `AGENTS.md`。

### 支持 @ 引入的 Agent（如 Qoder）

额外把 `AGENTS.md` 放到用户级目录，形状保持一致：

```
~/.qoder-cn/AGENTS.md
~/.qoder-cn/skills/<name>/SKILL.md
```

`AGENTS.md` 里那句 `@./skills/<name>/SKILL.md` 会被展开成正文，注入本机所有项目、所有会话的上下文，包括新开的子会话。相对路径按 `AGENTS.md` 所在目录解析，所以两处文件的相对位置不能改。

## 改规则

只改 `skills/<name>/SKILL.md` 这一份，然后按上文重装。**不要往 `AGENTS.md` 或 Agent 的配置文件里抄规则**——两处各一份必然会漂。

每个 skill 的修订流程、字数预算、验证方式、回滚规则，写在它自己目录下的 `UPDATE.md`，**不放在仓库根目录**：不同 skill 的验证方式不同（一个靠盲评与对照实验，一个靠停点是否被触发），混成一份通用规则必然用错标准。

每次修订以 commit 为版本，改完同步该 skill 头部的版本号与日期，并重装本机各 Agent 的副本。
