# precision-guided-clarity

一个轻量、跨 agent 的全局操作风格 profile。它通过一份指令文件，引导 agent 在各类任务中保持一致的工作方式，而不引入运行时代码或外部依赖。

版本：v1.0

## 设计目标

让 agent 在执行任务时保持以下风格：

- **直接输出优先**：先给结论或可执行结果，再补充必要说明。
- **先检查最窄相关状态再猜测**：在动手前查看最小范围的相关上下文，而不是凭印象推断。
- **最小充分深度**：分析到足以支撑下一步行动即可，不过度展开。
- **简化表达但不删除逻辑**：压缩冗余措辞，保留判断链条与关键约束。
- **只在真正阻塞时提问**：仅当缺失信息确实会导致错误结果时，提出一个决定性问题。
- **被纠正时干净恢复**：接受纠正后直接调整，不反复辩解或重述上下文。
- **渐进式上下文管理**：按需引入信息，避免一次性堆叠无关内容。

## 适用对象

适用于支持以下任一指令入口的 agent 或 assistant：

- 全局指令；
- 项目指令；
- `AGENTS.md` 风格的指令文件；
- 自定义系统提示词或 profile；
- skill 风格的按需指令包。

本项目不绑定单一 agent 运行时。仓库中的 Codex 文件只是可选适配示例。

## 通用安装方式

把 `AGENTS.md` 的内容放进你的 agent 全局或项目级指令入口。

推荐约束：

```text
将 Precision-Guided Clarity 作为底层操作风格加载。不要让它覆盖更高优先级的安全、用户、项目或任务专用指令。
```

如果你的 agent 支持 `AGENTS.md`，把根目录 `AGENTS.md` 放到该 agent 期望的全局或项目指令位置即可。

## Codex 适配安装

对于 Codex CLI 和标准 Codex 运行，一个常见路径是 `~/.codex/AGENTS.md`：

```bash
set -e
mkdir -p "${HOME}/.codex"
if [ -f "${HOME}/.codex/AGENTS.md" ]; then
  cp "${HOME}/.codex/AGENTS.md" "${HOME}/.codex/AGENTS.md.bak.$(date +%Y%m%d%H%M%S)"
fi
cp AGENTS.md "${HOME}/.codex/AGENTS.md"
```

如果你已有全局指令文件，建议手动合并带有 BEGIN/END 标记的 PGC 段落，而不是直接覆盖。

如果你的 Codex Desktop 已经使用 `model_instructions_file`，可以追加 Codex Desktop 适配片段：

```bash
set -e
DESKTOP_INSTRUCTIONS="${HOME}/.codex/desktop-instructions.md"
cp "${DESKTOP_INSTRUCTIONS}" "${DESKTOP_INSTRUCTIONS}.bak.$(date +%Y%m%d%H%M%S)"
cat profiles/codex-desktop-instructions.append.md >> "${DESKTOP_INSTRUCTIONS}"
```

`profiles/codex-config.profile.toml` 是可选 Codex 配置片段，用于需要命名 profile 的用户。

## 可选 skill 兼容

`precision-guided-clarity/` 目录是可选的 skill 风格产物，供支持按需 skill 或可复用指令包的 agent 使用。

对于 Codex 兼容的 skill 目录：

```bash
set -e
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
rm -rf "${CODEX_HOME:-$HOME/.codex}/skills/precision-guided-clarity"
cp -R precision-guided-clarity "${CODEX_HOME:-$HOME/.codex}/skills/"
```

skill 不是主载体。只有在需要逻辑保真改写、歧义分解、纠错恢复、上下文压缩、有状态执行或发布级文档处理时，才需要显式使用它。

## 卸载

从你安装它的指令文件中删除带标记的 PGC 段落即可。若安装了可选 Codex profile，从 Codex 配置中删除 `[profiles.pgc]`。若安装了可选 skill，删除复制进去的 `precision-guided-clarity` skill 目录。

## 项目结构

```text
AGENTS.md                                      # 标准全局操作风格 profile
profiles/codex-AGENTS.override.md             # 可选 Codex override 适配文件
profiles/codex-desktop-instructions.append.md # 可选 Codex Desktop 追加片段
profiles/codex-config.profile.toml            # 可选 Codex 配置片段
docs/install.md                               # 通用安装和适配说明
docs/context-management.md                    # 常驻上下文与按需深度的边界
precision-guided-clarity/                     # 可选 skill 兼容目录
```

## 安全姿态

- **仅指令文本**：仓库内不包含可执行代码、安装脚本或运行时 hook。
- **无网络行为**：不在任何阶段拉取远程内容。
- **无凭证**：不附带任何 API key、token 或账户信息。
- **无预授权工具配置**：不会替你打开任何工具的自动执行权限。
- **可审计**：所有文件均为纯文本，安装前可直接阅读全部内容。

启用本 profile 不会改变 agent 的工具权限，也不替代你的工具沙箱与权限策略。

## 许可证

MIT License。详见 `LICENSE` 文件。
