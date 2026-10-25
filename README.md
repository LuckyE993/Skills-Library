# Skills-Library

整理个人总结和经过适配的 Agent Skills，保留来源，并提供 Agent 可执行的安装、验证和维护说明。

## Skills 索引

| Skill | 用途 | 安装与兼容性 | 来源与改动 | 整理日期 |
| --- | --- | --- | --- | --- |
| [search-first](skills/search-first/SKILL.md) | 编码前检查本地复用，必要时调研现有方案 | [安装说明](skills/search-first/INSTALL.md) | [来源记录](skills/search-first/SOURCE.md) | 2026-10-20 |
| [research-evidence](skills/research-evidence/SKILL.md) | 文献检索、引用核验与研究主张的证据检查 | [安装说明](skills/research-evidence/INSTALL.md) | [来源记录](skills/research-evidence/SOURCE.md) | 2026-10-22 |
| [feishu-paper-reading](skills/feishu-paper-reading/SKILL.md) | 近期论文深读、跨论文综合与飞书阅读报告 | [安装说明](skills/feishu-paper-reading/INSTALL.md) | [来源记录](skills/feishu-paper-reading/SOURCE.md) | 2026-10-22 |
| [experiment-planner](skills/experiment-planner/SKILL.md) | 研究想法拆解、可证伪主张与最小实验矩阵 | [安装说明](skills/experiment-planner/INSTALL.md) | [来源记录](skills/experiment-planner/SOURCE.md) | 2026-10-22 |
| [paper-writing](skills/paper-writing/SKILL.md) | 论文章节写作、润色与全文一致性检查 | [安装说明](skills/paper-writing/INSTALL.md) | [来源记录](skills/paper-writing/SOURCE.md) | 2026-10-22 |
| [paper-review-panel](skills/paper-review-panel/SKILL.md) | 投稿前模拟评审与接收风险分析 | [安装说明](skills/paper-review-panel/INSTALL.md) | [来源记录](skills/paper-review-panel/SOURCE.md) | 2026-10-22 |
| [rebuttal-response-skills](skills/rebuttal-response-skills/SKILL.md) | 评审意见映射、证据整理与 rebuttal 回复 | [安装说明](skills/rebuttal-response-skills/INSTALL.md) | [来源记录](skills/rebuttal-response-skills/SOURCE.md) | 2026-10-22 |
| [paper-framework-figure-studio-pro](skills/paper-framework-figure-studio-pro/SKILL.md) | 论文方法图、架构图与流程图规划 | [安装说明](skills/paper-framework-figure-studio-pro/INSTALL.md) | [来源记录](skills/paper-framework-figure-studio-pro/SOURCE.md) | 2026-10-22 |
| [paper-visual-craft](skills/paper-visual-craft/SKILL.md) | 论文图表设计、重绘与证据一致性验证 | [安装说明](skills/paper-visual-craft/INSTALL.md) | [来源记录](skills/paper-visual-craft/SOURCE.md) | 2026-10-22 |
| [paper-share-html](skills/paper-share-html/SKILL.md) | 论文组会分享与 HTML 演示页面 | [安装说明](skills/paper-share-html/INSTALL.md) | [来源记录](skills/paper-share-html/SOURCE.md) | 2026-10-22 |

## 快速使用

可以直接交给 Agent：

```text
请阅读本仓库 README.md，以及 skills/search-first/INSTALL.md。
将 search-first 安装到当前目标项目，检查相关依赖，并按说明验证。
若目标已有同名 Skill，先比较差异，保留已有修改。
```

安装前先阅读对应 `INSTALL.md`。仓库的 `skills/` 是收录目录；仅 clone 本仓库不代表已安装到 Agent 的发现目录。Codex 的当前本地发现规则见 [OpenAI 官方文档](https://learn.chatgpt.com/docs/build-skills)。

在**需要使用 Skill 的目标项目根目录**运行以下命令，可安装本仓库本地副本（将路径改为实际 clone 位置）：

```powershell
npx skills@1.7.4 add "E:/Skills-Library/skills/search-first" --agent codex --copy
```

此方法需要 Node.js >= 22.20.0 和 npm；CLI 版本按本次整理固定。完整步骤、无 Node.js 的复制方式和其他系统用法见 [安装说明](skills/search-first/INSTALL.md)。CLI 参数依据 [Skills CLI 文档](https://github.com/vercel-labs/skills/blob/main/docs/commands.md)。

## 仓库结构

```text
docs/
  skills-management.md       管理方式、参考网页、整理日期
skills/
  search-first/
    SKILL.md                  Agent 的工作流入口
    INSTALL.md                安装、依赖、验证、更新、卸载
    SOURCE.md                 来源、固定 commit、本地改动
    LICENSE                   直接上游许可证
    LICENSE.upstream          更早来源的许可证（如有）
    agents/openai.yaml        Codex 元数据
```

## 收录与维护约定

1. 每个 Skill 放入 `skills/<name>/`，保留完整配套资源和第三方许可证。
2. `INSTALL.md` 写明支持环境、必要/可选依赖、安装范围、验证、更新和卸载；不需要的依赖明确写“无需”。
3. `SOURCE.md` 记录来源 URL、上游 commit、整理日期、本地改动和验证范围；自创 Skill 写明原创。
4. 安装前检查硬编码路径、其他 Skill、MCP、脚本和凭据要求。依赖缺失时写明降级方式或受影响的功能。
5. 上游更新先比较差异，再合并适配；同步来源记录和索引日期。

管理方式与参考资料见 [Skills 管理记录](docs/skills-management.md)。第三方内容遵循各目录中的许可证；这些许可证不自动覆盖仓库其他内容。
