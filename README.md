# proportionate-work ｜ 适度工作与充分验证

**让 AI Agent 按实际风险工作：必要验证不缺失，无关工作不追加。**

一个轻量 Agent Skill 规则包，面向 Codex（含 GPT 系列模型）与 Claude Code 等支持 Agent Skills 的 Harness。它约束可观察行为——重复测试、过度防御、免责声明堆砌——而不引入审批流程，不降低交付质量。

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## English Abstract

A lightweight Agent Skill that keeps AI coding/writing agents proportionate: verification depth matches actual risk, already-passed deterministic checks are not re-run, and defensive code or disclaimers are not added without a concrete reason — while necessary verification is never skipped, known problems are never hidden, and explicitly requested audits are done in full. It ships a ~1.5k-character resident rule set, on-demand engineering and writing references, a 250-character adapter for AGENTS.md / CLAUDE.md, and 12 acceptance cases covering both over-work and under-work failure modes.

## 解决的问题

通用模型 Agent 常见两类偏差：

- **过度工作**：已通过的确定性检查反复重跑；小改动触发全仓库扫描与安全审计；无关产物（哈希清单、审计报告）机械生成；文档中反复堆砌免责声明与 Limitations 章节。
- **工作不足**：跳过必要验证、隐瞒已知问题、编造测试成功、夸大研究结果。

本技能用一条核心原则同时约束两者：**最低额外负担，充分完成任务**。"最低"针对无关负担，不针对交付质量。

每项额外操作必须明确服务至少一项：用户明确要求的交付或验收；与本次改动直接相关、具有合理发生机制的故障；适用的项目/安全/研究规范；已出现的失败信号。

## 项目亮点

- **常驻负担小**：SKILL.md 正文约 1.5k 字；工程与写作细则按需加载，不占用常驻上下文。
- **跨 Harness**：通用 SKILL.md 格式，兼容 Codex 与 Claude Code；附可并入 AGENTS.md / CLAUDE.md 的 250 字短约定。
- **可验收**：12 个验收场景，每个同时定义"过度工作"与"验证不足"两个方向的错误行为，可作为评测设计起点。
- **证据导向**：验证去重规则有明确边界（复用条件、允许重跑的理由、默认重复预算）；平台接入细节经官方文档核验，未核验项如实标注。
- **守住底线**：禁止以删除测试、吞异常、伪造日志节省成本；发现数据泄漏或错误结论必须如实报告；用户要求深入审计时认真完成。

## 项目结构

```
proportionate-work/
  SKILL.md                        # 核心规则（触发后加载）
  references/
    engineering.md                # 工程规则（按需读取）
    writing.md                    # 论文与文档写作规则（按需读取）
  examples/
    acceptance-cases.md           # 12 个验收场景
  adapters/
    minimal-rules.md              # 可并入 AGENTS.md / CLAUDE.md 的短约定
  LICENSE
  README.md
```

## 快速开始

### Codex

1. 将本目录复制为 `~/.codex/skills/proportionate-work/`。
2. 在 `~/.codex/config.toml` 设置 `[features] skills = true` 并重启；或单次运行 `codex --enable skills`。
3. 按 description 自动触发，或用 `$proportionate-work` 显式调用。

### Claude Code

1. 放入 `<项目>/.claude/skills/proportionate-work/`（项目级）或 `~/.claude/skills/proportionate-work/`（个人级）。
2. 重启 Claude Code。
3. 自动触发，或用 `/proportionate-work` 显式调用。

### 可选：常驻短约定

将 `adapters/minimal-rules.md` 的内容人工并入项目的 AGENTS.md（Codex）或 CLAUDE.md（Claude Code）。本技能不会自动修改这些文件。

## 使用示例

- 修正 README 中的一句话 → 只改那句话并核对相关事实；不运行测试套件、不生成哈希、不写审计报告。
- 修改鉴权逻辑 → 覆盖鉴权分支的定向与集成测试，遵守项目规定的安全流程；不默认启动全面安全审计，也不只跑一个正常路径冒烟测试。

## 能力边界（如实说明）

- 提示性行为约束：效果取决于模型遵循程度与 Harness 的触发机制，不构成绝对保证。
- 未包含 hooks、守护进程、命令拦截器、预算引擎、评测平台等需要额外代码的强制控制；第一版刻意不开发。
- 本技能不自动修改 AGENTS.md / CLAUDE.md、全局配置或权限设置；不自动安装到全局目录；不提交、推送或发布。

## 参考资料与核验

核验日期：2026-09-16。核验方式：本机网络策略拦截了直连与页面抓取，平台要点来自对官方文档的搜索结果，请以官方当前文档为准：

- Codex Skills：https://developers.openai.com/codex/skills/ — 必填 `name`（≤100 字符）与 `description`（≤500 字符），均单行；description 用于触发匹配；实验性功能需显式启用。
- Codex AGENTS.md：https://developers.openai.com/codex/guides/agents-md/ — 全局 `~/.codex/AGENTS.md`；项目内从仓库根到当前目录逐级读取；合计大小约 32 KiB 上限。
- Claude Code Skills：https://code.claude.com/docs/en/skills — 必填 `name`（≤64 字符，与目录名一致）与 `description`（≤1024 字符）；触发时只读 name 与 description，激活后加载正文。

## 许可

MIT License，详见 [LICENSE](LICENSE)。
