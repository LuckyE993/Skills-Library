# search-first 安装与使用

整理日期：**2026-10-20**。来源及适配记录见 [SOURCE.md](SOURCE.md)。

## 给安装 Agent 的指引

先确认目标项目和 Agent，阅读本文件及 [SKILL.md](SKILL.md)，检查目标是否已有同名 Skill，再选择一种安装方式。复制整个目录，包括许可证和 `agents/`。安装后检查发现情况和下方验证场景；有本地修改的旧版先比较差异。

## 环境与依赖

| 能力 | 要求与缺失处理 |
| --- | --- |
| 基础工作流 | 能读取 `SKILL.md`、检查目标项目文件的 Agent；无自带脚本，无 Python/Node.js 运行依赖 |
| 本地搜索 | 使用宿主提供的文件工具（如 FastCtx）或 `rg`；工具缺失时说明可检查范围 |
| 外部调研 | 可用的联网搜索/官方文档工具；离线时仅做本地复用检查，声明证据缺口 |
| GitHub CLI | 可选；没有 `gh` 或认证时使用公开网页、已有本地 Git 信息 |
| npm / pip 等 | 仅查询相应生态时需要；可改用官方文档，不为基础使用安装全部包管理器 |
| MCP | 可选；优先使用已连接工具，未配置时使用可用的官方文档/搜索渠道 |
| `research-evidence` | 学术证据分支的可选配套 Skill，本次未收录；缺失时明确告知，按用户范围使用可用的一手论文/文档检索，不声称完成其专门流程 |
| `iterative-retrieval` | 可选组合；未安装不影响独立使用 |
| researcher / planner / architect | 上游使用的角色称呼；无需安装这些命名 Agent。有必要且已获授权时使用宿主的子 Agent 工具，否则当前 Agent 完成有界检索 |

`Agent(subagent_type=...)` 是上游的宿主示例，不能作为 shell 命令运行。正文中的库名、评分和示例结果是示意，选择依赖前重新核查。

主要适配对象为 Codex。其他支持 Agent Skills 格式的宿主可复用工作流，但需自行验证工具映射和调用入口。本目录保留上游的自动选择策略。

## 方式一：Skills CLI

需要 Node.js >= 22.20.0、npm；首次 `npx` 需要联网获取 CLI。安装器版本固定为本次核查的 `1.7.4`。[CLI 文档](https://github.com/vercel-labs/skills/blob/main/docs/commands.md)

在**目标项目根目录**运行，替换源路径：

```powershell
node --version
npx skills@1.7.4 add "E:/Skills-Library/skills/search-first" --agent codex --copy
npx skills@1.7.4 list
```

macOS/Linux 同样可用，将源路径替换为本机绝对路径。默认安装到项目范围；明确需要跨项目使用时增加 `--global`。`--copy` 安装独立副本，之后源目录的修改需要重新同步。

## 方式二：完整目录复制

无需 Node.js。Codex 当前官方路径为项目的 `.agents/skills/` 或用户的 `~/.agents/skills/`。[Codex 发现规则](https://learn.chatgpt.com/docs/build-skills)

PowerShell：先进入目标项目根目录，再运行：

```powershell
$skillSource = 'E:\Skills-Library\skills\search-first'
$skillParent = Join-Path (Get-Location).Path '.agents\skills'
$skillTarget = Join-Path $skillParent 'search-first'
if (Test-Path -LiteralPath $skillTarget) { throw '目标已有 search-first，请先比较差异。' }
New-Item -ItemType Directory -Path $skillParent -Force | Out-Null
Copy-Item -LiteralPath $skillSource -Destination $skillTarget -Recurse
Test-Path -LiteralPath (Join-Path $skillTarget 'SKILL.md')
```

macOS/Linux，在目标项目根目录运行：

```bash
skill_source='/absolute/path/Skills-Library/skills/search-first'
skill_parent="$PWD/.agents/skills"
skill_target="$skill_parent/search-first"
if [ -e "$skill_target" ] || [ -L "$skill_target" ]; then
  printf '%s\n' '目标已有 search-first，请先比较差异。'
else
  mkdir -p "$skill_parent" && cp -R "$skill_source" "$skill_target"
fi
```

用户范围：PowerShell 将 `$skillParent` 改为 `Join-Path $HOME '.agents\skills'`，Bash 将 `skill_parent` 改为 `"$HOME/.agents/skills"`。只选择一个范围，避免重复安装。

## 验证

1. 确认目标 `<skill-directory>/SKILL.md`、两份许可证和 `agents/openai.yaml` 存在，避免多嵌套一层目录。
2. 在目标项目打开 Codex，查看 Skills 列表；未显示时重启。CLI/IDE 可通过 `/skills` 或 `$search-first` 选择。[调用方式](https://learn.chatgpt.com/docs/build-skills)
3. 在临时项目中运行以下请求，观察是否先查本地、说明可用工具，并给出有依据的选择：

```text
使用 $search-first：我想增加 Markdown 死链接检查。
先检查本项目已有工具，再判断是否需要外部检索。
本次只给建议，不安装依赖或修改配置。
```

另一个验证场景：准备一个已有 HTTP 客户端的临时项目，请它只修补该客户端的一个明确问题。预期先复用或修复已有实现，只有遇到具体未知信息才定向查询。

## 更新、卸载和回退

- 本仓库：按 `SOURCE.md` 的 commit 比较上游变化，合并本地适配，再更新日期和验证记录。
- CLI 安装副本：先保存本地改动，再重新执行本地来源的安装命令；`npx skills@1.7.4 remove search-first` 移除此 Skill 的全部项目 Agent 安装引用，用户范围额外指定 `--global`。共享 `.agents/skills` 目录的其他 Agent 也会受影响，先确认使用范围。
- 手工复制副本：先备份修改，再以新完整目录替换；卸载时核实绝对路径，只移除当时安装的 `search-first` 目录或链接。
- 回退：从本仓库已验证的旧 commit 取出完整目录，按原方式重新安装。

## 本次验证范围

验证内容包括格式、来源文件完整性、文档本地链接，以及在临时项目中用 Skills CLI 复制安装和发现。未对用户项目或用户级 Skill 目录执行安装；实际 Agent 行为需在目标宿主按上述场景验证。

本次本地来源安装可由 CLI `list` 列出，但 `check` 未将其列为可更新项；同步本地修改应重新执行安装命令。

本次定向卸载 `remove --agent codex` 后共享目录仍在；省略 `--agent` 完整卸载后，CLI `list` 为空。卸载后应检查目录及列表，不仅依赖成功提示。
