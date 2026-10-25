# 安装与使用：rebuttal-response-skills

评审意见映射、证据整理与 rebuttal 回复。

## 依赖与兼容性

文本工作流无需额外运行时；需要正式 reviews 和论文证据。新增实验依赖目标项目工具链；独立盲审依赖宿主多 Agent 能力。外部投稿平台与发布权限需要单独配置。

此目录是仓库收录副本。适用于能读取 Agent Skills 的宿主；上游工作流和元数据面向 Codex，其他宿主需核对工具名和能力。
无需为复制操作安装 Python、Node.js、MCP 或外部工具；依赖只在使用相应功能时需要。

## 复制安装

按本仓库 [安装管理说明](../../docs/skills-management.md) 选择目标宿主的发现目录。
例如，先将 PowerShell 的当前目录切换到需要使用此 Skill 的目标项目，再执行：

```powershell
$skillTarget = Join-Path (Get-Location) '.agents/skills/rebuttal-response-skills'
if (Test-Path -LiteralPath $skillTarget) { throw '目标已存在，请先比较差异' }
New-Item -ItemType Directory -Force -Path (Split-Path -Parent $skillTarget) | Out-Null
Copy-Item -LiteralPath 'E:/Skills-Library/skills/rebuttal-response-skills' -Destination $skillTarget -Recurse
```

源路径按本仓库的实际位置调整。安装时保留整个目录及全部许可证。

## 验证、更新与卸载

1. 检查目标中存在 `SKILL.md`、`LICENSE`、`agents/openai.yaml` 及完整配套资源。
2. 在支持的宿主显式调用 `$rebuttal-response-skills`，先用本地样例验证基本流程，再验证需要联网或外部连接的能力。
3. 上游版本见 [SOURCE.md](SOURCE.md)。更新前比较差异并保存目标中的本地修改，再同步完整目录。
4. 卸载时仅移除所选发现目录下的 `rebuttal-response-skills`，确认路径及其他宿主是否共用；仓库收录副本另行保留。

本次只完成复制和文件一致性检查，未安装到宿主发现目录，也未验证实际任务行为。
