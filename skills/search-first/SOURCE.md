# search-first 来源与适配记录

| 项目 | 记录 |
| --- | --- |
| 整理日期 | 2026-10-20（Asia/Shanghai） |
| 直接上游 | [sidiangongyuan/codex-skills-library](https://github.com/sidiangongyuan/codex-skills-library) |
| 上游路径 | `skills/search-first/` |
| 收录 commit | `41f5a211b1a8d210023f51f9d56088311a3dae79` |
| 固定快照 | [查看对应目录](https://github.com/sidiangongyuan/codex-skills-library/tree/41f5a211b1a8d210023f51f9d56088311a3dae79/skills/search-first) |
| 许可证 | MIT；保留 [LICENSE](LICENSE) 和 [LICENSE.upstream](LICENSE.upstream) |
| 状态 | 已收录并做最小兼容补充；安装验证，行为待目标宿主验证 |

## 原始资源

完整复制上游以下四个文件；其中 `SKILL.md` 含下述本地补充，其他三个文件保持收录时内容：

```text
SKILL.md
LICENSE
LICENSE.upstream
agents/openai.yaml
```

`LICENSE` 的署名为 sidiangongyuan，`LICENSE.upstream` 的署名为 Affaan Mustafa。两份声明均随目录保留，不将第三方许可证自动应用到本仓库其他文件。

## 本地改动

- 新增 `INSTALL.md` 和本文件。
- 在 `SKILL.md` 增加安装说明入口、宿主文件工具适配、学术配套 Skill 缺失时的处理。
- 保留原有名称、描述、主工作流、MIT 声明和 `allow_implicit_invocation: true`。
- 未额外收录 `research-evidence`、`iterative-retrieval`，未增加 MCP、脚本或运行包依赖。

## 后续同步

1. 在临时目录 clone 上游，记录候选 commit；不要把其 `.git` 复制进本仓库。
2. 对照本文件的固定 commit 比较 `skills/search-first/`，核查新增/删除资源和许可证变化。
3. 合并上述本地补充，重新检查依赖和宿主兼容性。
4. 验证格式及临时项目安装，更新本文件、安装说明和 README 日期；最后重新安装需要使用的副本。

本次为单目录收录，不建立自动跟随上游的 submodule 或后台更新。

## 验证记录（2026-10-20）

- 环境：Windows PowerShell、Node.js 26.7.0、Skills CLI 1.7.4、Python 3.13.13（仅用于校验）。
- `skill-creator` 的 `quick_validate.py` 校验通过；YAML 和文档相对文件链接检查通过。
- 在新建的临时 Git 项目中，从本地来源列出、`--agent codex --copy` 安装并由 CLI `list` 发现成功；安装的六个文件与本仓库逐字节一致。
- 两份许可证及 `agents/openai.yaml` 与上游逐字节一致。
- CLI `check` 未追踪本地来源更新；按安装说明重新安装同步。
- 定向卸载后共享目录仍保留；省略 `--agent` 完整卸载后，CLI `list` 返回空列表。相关范围说明已写入安装文档。
- 未测试实际 Agent 选择与工作流行为、其他宿主、用户范围安装或 GitHub CLI。
