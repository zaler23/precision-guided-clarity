# precision-guided-clarity

Precision-Guided Clarity 是一份极简、通用的智能体指令 profile。它是 instruction-only：没有 runtime、MCP 服务、安装 hook 或客户端专用适配器。

PGC 是轻量行为契约与认知塑形核心，不是能力升级器。它的作用是在模糊和不确定中保持有用：不机械顺从错误字面请求，不因为缺信息就停住，不编造未见上下文，也不把答案变成教学模板。用户应当从答案本身潜移默化地获得更强判断力和可迁移直觉。

**版本：** 1.4.0
**运行时产物：** `AGENTS.md`
**补充产物：** `precision-guided-clarity/` 与 `docs/`，仅供维护和 conformance 审查

## 设计目标

PGC 使用一个极简核心，不把请求分流成多套提示模式。它帮助 agent：

- 先给答案、补丁、命令、建议或一个阻塞问题；
- 根据可见上下文推断用户真实目标、当前瓶颈和结果风险，并在已有证据范围内行动；
- 保护用户真实目标，而不是机械执行有问题的字面请求；
- 当精确执行尚无依据时，先采取低风险、有用、可逆的一步；
- 对模糊但可逆的任务，在提缺失信息前先给默认可用版本；
- 当正确性依赖状态时，先检查最窄相关事实；
- 不声称看到了未提供的文件、日志、屏幕、工具、代码库或上下文；
- 只在能改善答案时自然嵌入一个强认知锚点；
- 简化表达，但不损失逻辑；
- 只在真正阻塞时问一个决定性问题；
- 默认使用紧凑自然段；只有列表或表格能实质改善结果时才使用。

## 包含内容

- `AGENTS.md` 是完整运行时 profile。
- `precision-guided-clarity/SKILL.md` 是补充索引，不是路由层。
- `precision-guided-clarity/references/*.md` 是维护、审查和兼容性说明用的附录。
- `docs/` 提供安装、上下文和 conformance 说明。

普通提示不需要加载补充文件。不要为了让 PGC 生效而预加载它们。如果宿主系统可以暴露这些文件，应把它们视为显式审查材料，而不是任务路由器。

## 通用安装

把 `AGENTS.md` 的内容复制或合并到 agent 已支持的指令入口，例如 system prompt、项目指令、`AGENTS.md` 风格文件或自定义指令字段。

推荐集成约束：

```text
将 Precision-Guided Clarity 作为底层操作风格加载。AGENTS.md 是完整 PGC 运行时 profile。除非用户明确要求检查或审查 PGC 文档，否则不要增加额外 PGC 路由层。
```

## 更新或移除

PGC 使用可见 marker，便于更新或删除。删除以下标记之间的内容即可：

```text
<!-- BEGIN precision-guided-clarity v1.4.0 -->
<!-- END precision-guided-clarity v1.4.0 -->
```

修改全局或项目级指令后，重启 agent 或开启新会话。

## 项目结构

```text
AGENTS.md                          # 完整运行时 profile
README.md                          # 英文说明
README.zh-CN.md                    # 简体中文说明
docs/install.md                    # 通用安装指南
docs/context-management.md         # 单核心上下文说明
docs/conformance.md                # 手动行为检查
precision-guided-clarity/          # 补充附录，不是运行时路由
```

## 分发方式

以源码仓库作为分发形式。需要可复现性时，请使用 `git clone` 并校验 commit hash。

本项目不提供自定义 zip、tar、checksum、安装器或可执行 Release 产物。

## 许可证

MIT License。详见 `LICENSE`。
