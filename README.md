# leekinbun

通用的个人 skill 安装仓库。每个 skill 一份 Markdown，写给 AI 读的，放在 `skills/<name>/` 下，与具体 Agent 无关；各 Agent 怎么装见下文。

## 目录结构

```
skills/<name>/SKILL.md        # skill 正文（权威版本在这里）
AGENTS.md                     # 可选模板：用户级指令文件，只引入 skill，不含规则副本
```

## 怎么装

通用做法：把 `skills/<name>/` 整个目录复制到目标 Agent 的用户级 skills 目录，保持 `<name>/SKILL.md` 的形状。

| Agent | 用户级 skills 目录 |
| --- | --- |
| ZCode | `~/.agents/skills/` |
| Qoder | `~/.qoder-cn/` |
| Claude Code | `~/.claude/skills/` |
| WorkBuddy | `~/.workbuddy/skills/` |

### 只认 skills 目录的 Agent（如 ZCode、Claude Code）

```
~/.agents/skills/<name>/SKILL.md
```

直接复制即可，不需要 `AGENTS.md`。

### 支持 @ 引入的 Agent（如 Qoder）

额外把 `AGENTS.md` 放到用户级目录，形状保持一致：

```
~/.qoder-cn/AGENTS.md
~/.qoder-cn/skills/leekinbun/SKILL.md
```

`AGENTS.md` 里那句 `@./skills/<name>/SKILL.md` 会被展开成正文，注入本机所有项目、所有会话的上下文，包括新开的子会话。相对路径按 `AGENTS.md` 所在目录解析，所以两处文件的相对位置不能改。

## 改规则

只改 `skills/<name>/SKILL.md` 这一份，然后按上文重装。**不要往 `AGENTS.md` 或 Agent 的配置文件里抄规则**——两处各一份必然会漂。

每次修订以 commit 为版本（v3 → v3.1 → …），改完同步 `SKILL.md` 头部的版本号与日期，并重装本机各 Agent 的副本。

## 当前状态

`leekinbun`：`Active`（执行中），2026-10-12 起，当前版本 v3.8。本机 ZCode（`~/.agents/skills/`）与 Qoder（`~/.qoder-cn/`）两份副本均与仓库逐字节一致。**更新治理见 [UPDATE.md](UPDATE.md)**：修改触发、分级验证流程、字数预算与反膨胀原则、条款级回滚、变更日志。

版本沿革：v3.1（5000 字）→ v3.3 瘦身（约 3200 字，40 次盲评验证后转正）→ v3.5（并入人机协作回路：需求穿透澄清与类比复述、修复循环收敛与反掩盖、经验沉淀路由、每一次回答交互式与结论先行；v3.3 vs v3.5 对照实验零回退、结论先行 10/10 vs 3/10）→ v3.7（规模相称硬触发、成本自报、分诊落地细则、风险对应验证、单一事实来源；依据 skill-eval 12 runs，Δ=+0.078）→ v3.8（风险对应验证默认反转，成本自报改为停止条件）。v3.2、v3.4 原文均保留在仓库提交历史中。

`anomaly`：`Active`（试用中），2026-10-26 起，当前版本 v6。用于**复杂、开放问题的思考伴随**：先猜定一个具体对象并对齐 → 十五问全扫（元方法层）→ 角色反转与盲区自检 → 三池合并后按「是否改变任何动作」严格收敛 → 沿映射表下沉到领域方法、具体技巧与当天可执行动作。每轮只设一个停点，用户每轮只做一个动作（改一句／指一条／删几条／挑一条）。

与 `leekinbun` 的分工：后者管**开发任务怎么执行**（需求、MVP、测试、汇报）；前者管**复杂判断怎么想**（对齐、广度、收敛、落地）。两者不重叠，也不互相引用——各自独立演进，避免规则在两处各存一份。

安装：`~/.workbuddy/skills/anomaly/SKILL.md` 与仓库逐字节一致；其余 Agent 按上表复制 `skills/anomaly/` 整个目录即可。
