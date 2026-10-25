# Skills 管理方式

整理日期：**2026-10-20（Asia/Shanghai）**。以下为当日核查记录；工具、命令和发现路径可能继续变化，更新时重新核对对应官方网页。

## 本仓库采用的方式

以 `skills/<name>/` 保存可独立复制的完整 Skill，以 Git 保存版本；每项配套 `INSTALL.md` 和 `SOURCE.md`。先维护收录内容，需要使用时再安装到目标 Agent 的发现目录。

当前采用普通目录和固定 commit 的来源记录，不引入 submodule。安装器管理的是安装副本，不负责维护本仓库中的本地适配；上游变动由维护者比较、合并并验证。

这些是本仓库约定。标准要求的入口是 `SKILL.md`，并未强制要求 `INSTALL.md` 或 `SOURCE.md`。[Agent Skills 标准](https://agentskills.io/specification)

## 当前可选方式

| 方式 | 适用场景 | 管理重点 |
| --- | --- | --- |
| 完整目录复制或链接 | 个人收录、开发适配、离线分发 | 明确发现目录；复制后需重新同步；链接依赖源目录持续存在 |
| Codex `$skill-installer` | 在 Codex 中安装精选 Skill 或 GitHub 来源 | 安装后仍需检查运行依赖，按宿主文档验证发现情况 |
| Vercel Skills CLI | 为多个 Agent 安装、列出、检查更新、移除 Skill | 指定 Agent、安装范围与 CLI 版本，保留安装器生成的追踪文件 |
| GitHub CLI `gh skill` | 已使用新版 GitHub CLI，希望从 GitHub 安装和固定来源版本 | 先用 `gh skill --help` 确认本机支持；支持 pin，更新可 dry-run |
| Codex/ChatGPT 插件 | 对外分发多个工作流，或同时打包 MCP 等能力 | 额外维护插件清单和分发配置，安装 Skill 不等于连接服务 |

依据：[OpenAI 本地 Skills 文档](https://learn.chatgpt.com/docs/build-skills)、[Skills CLI](https://github.com/vercel-labs/skills)、[GitHub CLI 安装文档](https://cli.github.com/manual/gh_skill_install)、[GitHub CLI 更新文档](https://cli.github.com/manual/gh_skill_update)、[插件打包文档](https://developers.openai.com/plugins/build/plugins)。

## 格式与发现目录

通用格式是目录中的 `SKILL.md`，含 YAML `name`、`description` 和工作流正文；按需要增加 `scripts/`、`references/`、`assets/`。环境约束可写入 `compatibility`，详细安装步骤保留在配套说明中。[格式规范](https://agentskills.io/specification)

Codex 当前文档列出的主要本地位置：

| 范围 | 位置 |
| --- | --- |
| 目标项目 | `<project>/.agents/skills/<name>/` |
| 当前用户 | `~/.agents/skills/<name>/` |

Codex 支持链接目录，可显式调用 `$skill-name`，也可按描述自动选择。新文件通常自动发现，未显示时重启。安装前检查同名项，避免重复加载。以[当前发现规则](https://learn.chatgpt.com/docs/build-skills)为准；本机可能存在旧版或安装器使用的 `~/.codex/skills`，不要仅凭旧教程选择路径。

跨 Agent 安装时按 [CLI 的宿主路径表](https://github.com/vercel-labs/skills/blob/main/docs/agents.md)选择，目录可移植不代表工具、权限和工作流完全兼容。

## 常用管理命令

本次从 npm 核查到 `skills` 最新发布版本为 **1.7.4**，要求 **Node.js >= 22.20.0**。示例固定该版本；这不是上游 Skill 的版本锁定。[CLI 源码与运行要求](https://github.com/vercel-labs/skills)

以下在目标项目运行，安装源为已 clone 并审核的本仓库：

```powershell
# 列出来源中可发现的 Skills，不安装
npx skills@1.7.4 add "E:/Skills-Library" --list

# 安装指定 Skill；--copy 避免依赖 clone 路径长期存在
npx skills@1.7.4 add "E:/Skills-Library" --skill search-first --agent codex --copy

# 查看已安装项、检查更新
npx skills@1.7.4 list
npx skills@1.7.4 check

# 适用于该 CLI 管理的安装副本
npx skills@1.7.4 update search-first
npx skills@1.7.4 remove search-first
```

默认是项目范围，`--global` 为用户范围。本次实测本地来源能安装和列出，但 `check` 返回“无项目 Skills 可更新”，因此本地副本应在比较后重新执行安装命令同步，不能依赖更新检查。`check`/`update` 示例用于安装器能够追踪更新的来源。不要用安装副本的更新命令覆盖本仓库收录目录。选项详见 [CLI 命令参考](https://github.com/vercel-labs/skills/blob/main/docs/commands.md)。

卸载示例会移除该范围内此 Skill 的全部 Agent 安装引用。多个 Agent 可能共用 `.agents/skills`，卸载前确认影响范围。本次 Windows 本地复制安装实测中，指定 `remove --agent codex` 后目录仍在；省略 `--agent` 后完整移除，CLI `list` 为空。

GitHub CLI 提供另一种安装路径，适合直接使用未经本地适配的上游固定快照：

```powershell
gh skill --help
gh skill install sidiangongyuan/codex-skills-library skills/search-first --agent codex --scope project --pin 41f5a211b1a8d210023f51f9d56088311a3dae79
gh skill update --dry-run
```

固定项不会随普通更新自动升级。此命令获取的是上游版本，未包含本仓库的安装指引和兼容补充；当前机器没有 `gh`，本次仅核对官方文档，未实跑。[安装及 pin 规则](https://cli.github.com/manual/gh_skill_install)、[更新规则](https://cli.github.com/manual/gh_skill_update)

插件分发可在需要时加入：在插件根目录创建 `plugin.json`，将工作流放在 `skills/`；需要额外初始化时可设置 onboarding Skill。本仓库现阶段保留普通目录结构。[插件打包方式](https://developers.openai.com/plugins/build/plugins)

## 新增与更新流程

1. 核查来源和许可证，固定 commit；需要时在临时目录 clone 模板或上游仓库。
2. 保存完整 Skill，检查文件引用、硬编码路径、依赖和宿主专用命令。
3. 在 `INSTALL.md` 写清哪些能力必须安装、哪些可以降级；在 `SKILL.md` 放入指向安装说明的入口，确保 Agent 能发现。
4. 用目标宿主可用的工具表达工作流，记录与上游的差异。
5. 校验格式和资源；在临时项目验证安装。结构校验、安装成功和实际行为验证分别记录。
6. 更新 `SOURCE.md`、README 索引和整理日期。升级前用 Git 保存本地修改，合并后重新安装目标副本；回退时取已验证 commit 的完整目录重新安装。

## 本次核查结果

已收录 `search-first`；来源固定到 `41f5a211b1a8d210023f51f9d56088311a3dae79`。它没有自带执行脚本，基础工作流无需 Python/Node.js 运行依赖；Node.js 仅为选择 Skills CLI 安装时所需。学术证据分支、GitHub 检索、子 Agent 等按实际能力启用，详见 [安装说明](../skills/search-first/INSTALL.md)。
