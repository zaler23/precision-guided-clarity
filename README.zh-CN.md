# precision-guided-clarity

Precision-Guided Clarity 是一份通用的智能体指令 profile，可复制或合并到任意兼容 agent 的指令入口，例如 system prompt、项目指令、`AGENTS.md` 风格文件或自定义指令字段。它不是某个具体客户端的适配包。

PGC 不只是为了生成清楚答案，也用于支持强理解：让答案帮助用户澄清意图、落地关键判断、提升判断力，但不把普通任务变成教学。

**版本：** 1.2.0  
**主产物：** `AGENTS.md`  
**可选产物：** `precision-guided-clarity/` reference pack，供兼容的按需 skill 或参考系统使用

## 设计目标

PGC 优先保证 agent 行为好用，其次才是轻量、可复制和低 token。它帮助 agent：

- 先给答案、命令、补丁、建议或一个阻塞问题；
- 在猜测前检查最窄相关状态；
- 用最小但完整的深度支撑正确行动；
- 简化表达，但不删除假设、判断标准、因果链、机制、边界、验证步骤或失败信号；
- 在有用时让重要判断落在具体结构、边界、决策规则或失败模式上；
- 只在真正阻塞时提出一个决定性问题；
- 被纠正时替换错误假设，而不是辩解或过度道歉；
- 保持常驻上下文短小，只在任务需要时加载更深参考。

## 包含内容

- `AGENTS.md` 是唯一标准的常驻通用 profile。
- `precision-guided-clarity/SKILL.md` 是可选路由索引，供兼容的 reference 或 skill 系统使用。
- `precision-guided-clarity/references/*.md` 提供更深的歧义处理、强理解、推理输出、技术执行、工具使用和多轮恢复指导。
- `docs/` 提供通用安装、上下文管理与 conformance 说明。

本仓库不发布客户端专用配置文件、运行时代码、安装 hook、自动化脚本或自定义 Release 压缩包。

## 通用安装

把 `AGENTS.md` 的内容复制或合并到你的 agent 已支持的指令入口。

推荐集成约束：

```text
将 Precision-Guided Clarity 作为底层操作风格加载。不要让它覆盖更高优先级的用户、项目或任务专用指令。
```

如果你的 agent 支持项目指令文件，把根目录 `AGENTS.md` 放到或合并到该 agent 期望的项目级或全局指令位置。

## 可选参考包

`precision-guided-clarity/` 目录是可选的。只有当你的 agent 能读取本地参考资料或按需加载 skill 时，才需要使用它。

对于兼容系统，把该目录复制到该系统用于 reference pack 或 skill 的位置。如果你移动到不同路径，请更新 `AGENTS.md` 中的 reference 路径，或保持相同的相对目录结构。

reference pack 不是主载体。普通行为应来自 `AGENTS.md`；只有任务触发更深流程时才加载参考文件。

## 更新或移除

PGC 使用可见 marker，便于更新或删除。删除以下标记之间的内容即可：

```text
<!-- BEGIN precision-guided-clarity v1.2.0 -->
<!-- END precision-guided-clarity v1.2.0 -->
```

如果安装了可选 reference pack，删除你复制到目标位置的 `precision-guided-clarity` 目录。

修改全局或项目级指令后，重启 agent 或开启新会话。

## 项目结构

```text
AGENTS.md                          # 标准常驻通用 profile
README.md                          # 英文说明
README.zh-CN.md                    # 简体中文说明
docs/install.md                    # 通用安装指南
docs/context-management.md         # 常驻上下文与可选参考边界
docs/conformance.md                # 手动行为检查
precision-guided-clarity/          # 可选 reference pack
```

## 分发方式

以源码仓库作为分发形式。需要可复现性时，请使用 `git clone` 并校验 commit hash。

本项目不提供自定义 zip、tar、checksum、安装器或可执行 Release 产物。

## 许可证

MIT License。详见 `LICENSE`。
