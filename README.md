# git-commit-message-zh

一个用于生成中文 Git 提交信息的 Codex Skill。

首次提交时，它会直接阅读当前项目的代码及必要配置，覆盖已暂存、未暂存和未跟踪的有效文件；已有提交时，分析当前分支相对上游的本地提交及工作区改动。根据实际内容自动选择合适的 Conventional Commits 类型，最终输出一条包含简洁标题和分条描述正文的中文提交信息。

## 支持的提交类型

| 类型 | 适用改动 |
| --- | --- |
| `feat` | 新增用户可感知的能力或行为 |
| `fix` | 修复错误、缺陷或异常行为 |
| `refactor` | 改变内部实现但不改变外部行为 |
| `docs` | 仅修改文档 |
| `test` | 仅新增或调整测试 |
| `chore` | 常规维护或非功能性调整 |
| `perf` | 提升性能 |
| `style` | 仅调整代码格式 |
| `build` | 修改构建系统或依赖 |
| `ci` | 修改持续集成配置 |
| `revert` | 撤销已有改动 |

类型按主要改动目的选择，不按文件数量或文件名判断。界面样式变化不等于 `style`；功能附带的测试和文档沿用主要类型；依赖调整通常用 `build`。互不相关的改动会建议拆分；已确认的不兼容变更使用 `!` 和 `BREAKING CHANGE` 标记。完整边界见 [类型判断规则](SKILL.md#判断规则)。

分析过程只会读取仓库信息，不会执行 `git add`、`git commit` 或 `git push`。

## 安装

### 推荐：使用 npx

请先安装 [Node.js](https://nodejs.org/)，然后运行：

```bash
npx skills add haishishushu/git-commit-message-zh -a codex -g
```

该命令使用 [Vercel Labs Skills CLI](https://github.com/vercel-labs/skills)，并将本 Skill 全局安装到 Codex。

### 手动安装

下载或克隆本项目后，将整个 `git-commit-message-zh` 目录复制到：

```text
~/.agents/skills/git-commit-message-zh
```

如果 Codex 没有自动识别，请重启 Codex。

## 使用

在需要生成提交信息的 Git 仓库中打开 Codex，然后输入：

```text
$git-commit-message-zh 根据当前 Git 改动生成一条中文提交信息
```

或者

```text
git-commit-message-zh
```

- 首次提交：仓库已初始化但当前分支尚无提交时，无需设置上游；根据当前已经写好的代码总结，不固定输出“初始化项目”。若没有任何有效文件，则说明没有可总结的内容。
- 已有提交：当前分支需有本地上游跟踪引用，并存在尚未同步到上游的改动。仅缺少上游不会被当作首次提交。

默认输出“标题 + 空行 + 描述正文”，标题使用半角冒号加一个空格（`feat: 中文摘要`），描述根据实际改动归纳，通常为 2–5 条，简单改动可只写 1 条。若只需要标题，可明确要求“仅标题”或“单行”。

输出示例（假设实际改动包含文件上传、大小限制和超限提示）：

```text
feat: 新增文件上传功能并添加大小限制

- 支持选择文件并上传至服务端
- 上传前校验文件大小，超限时阻止上传并提示原因
```
