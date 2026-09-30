# Demand Essence Loop

一个帮助 AI 编程代理识别真实需求、避免 XY Problem，并以最小安全改动推动系统演进的通用 skill。

它适合处理带有明显“方案先行”倾向的需求、测试反馈、跨角色冲突，以及会影响状态机、数据、权限、接口兼容性或外部副作用的变更。对于已经定义清楚、没有实质设计取舍的简单修改，它不会强行引入额外流程。

## 它解决什么问题

需求方经常描述一个解决方案，而不是问题本身。例如“增加一个全局强制按钮”“把所有数据导出来”“再加一个特殊状态”。直接照做可能修复表象，却制造重复能力、破坏领域模型或留下难以演进的契约。

本 skill 引导代理完成一个风险适配的闭环：

1. 分离观察、目标、约束和提议方案；
2. 从代码、契约、Schema、测试或运行行为中确认当前系统事实；
3. 识别真正缺失的是能力，还是可发现性、流程摩擦或实现缺陷；
4. 评估相关的用户体验、状态、数据、权限、并发和外部副作用；
5. 选择解决完整用户旅程的最小安全方案；
6. 只在有可信演进路径时保留兼容空间，并用匹配风险的证据完成验证。

## 设计原则

- 不把用户提出的第一个实现方案等同于需求本身；
- 不以“需求分析”为由拖慢清晰、低风险的简单工作；
- 不预设技术栈、业务领域、仓库结构或验证命令；
- 不把 `metadata`、布尔开关、兼容层或规则引擎当作默认的“未来兼容”；
- 不强制每次输出固定的长报告；
- 不在缺少实现或风险相关验证时宣称完成。

## 目录结构

```text
demand-essence-loop/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── requirements-discovery.md
    ├── impact-and-evolution.md
    └── response-patterns.md
```

- `SKILL.md`：触发边界、核心工作流与决策规则。
- `requirements-discovery.md`：需求下潜、证据优先和 XY Problem 诊断。
- `impact-and-evolution.md`：风险分级、影响面、可逆性与演进判断。
- `response-patterns.md`：按决策复杂度选择的沟通结构。

## 安装

### Codex

将仓库复制或软链接到 Codex skills 目录：

```bash
git clone https://github.com/huxy2023/demand-essence-loop.git
ln -s "$(pwd)/demand-essence-loop" "$HOME/.codex/skills/demand-essence-loop"
```

重启或刷新 Codex 后，可直接使用：

```text
Use $demand-essence-loop to analyze this change request and recommend the smallest safe solution.
```

### Gemini CLI

将仓库复制或软链接到 Gemini skills 目录：

```bash
mkdir -p "$HOME/.gemini/config/skills"
ln -s "$(pwd)/demand-essence-loop" "$HOME/.gemini/config/skills/demand-essence-loop"
```

### 其他支持 `SKILL.md` 的代理

把整个目录放入该代理的 skills 搜索路径。不同产品的发现机制可能不同，请以其本地配置为准。

## 使用示例

```text
使用 $demand-essence-loop 分析“给审批页面增加一个绕过审核的快捷按钮”这个需求。
请先确认真实目标与现有恢复路径，再给出最小安全方案、影响面和验证范围。
```

```text
Use $demand-essence-loop to review this proposed schema change. Separate the current requirement from speculative future needs and identify the least reversible decisions.
```

## 触发边界

适合：

- 用户直接给出实现方案，但真实问题尚未确认；
- 多个角色或系统边界存在利益与风险冲突；
- 变更涉及共享状态、公共接口、持久化数据、权限、并发或外部副作用；
- 团队需要在“只修表象”和“过度设计”之间做出可解释的决策。

不适合：

- 文案、格式、命名等没有实质设计取舍的明确修改；
- 已有清晰验收标准且只需按既有模式实现的低风险任务；
- 与软件或产品变更无关的一般性需求。

## 许可

[MIT License](LICENSE)

---

## English

Demand Essence Loop is a project-agnostic skill for AI coding agents. It helps distinguish an underlying outcome from a proposed implementation, inspect the current source of truth, assess relevant system impact, choose the smallest complete solution, and preserve credible evolution paths without speculative infrastructure.

Use it for ambiguous or cross-cutting change requests. Skip it for straightforward edits that contain no material design decision. See [`SKILL.md`](SKILL.md) for the full invocation behavior.
