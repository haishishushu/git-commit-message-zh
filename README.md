# git-commit-message-zh

一个用于生成中文 Git 提交信息的 Codex Skill。

它会分析当前分支相对上游的本地提交、已暂存、未暂存和未跟踪文件，并根据主要改动目的自动选择合适的 Conventional Commits 类型，最终输出一条简洁、具体的中文提交信息。

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

使用前请确保当前分支已经设置上游分支，并且仓库中存在尚未同步到上游的改动。

输出示例：

```text
feat：新增文件上传功能并添加大小限制
```
