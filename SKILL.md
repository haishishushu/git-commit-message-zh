---
name: git-commit-message-zh
description: Use when a user asks for one specific Chinese Git commit message from current changes, Conventional Commit wording, or automatic commit-type selection.
---

# 中文 Git 提交信息

## 核心原则

以当前分支的本地上游跟踪引用 `@{upstream}` 为唯一基准，完整理解上游之后的本地提交、已暂存、未暂存和未跟踪文件，再输出一条具体的中文提交信息。

## 只读分析

1. 确认当前目录是 Git 仓库、当前处于分支上，并解析 `@{upstream}`。
2. 获取完整的受跟踪文件差异：

   ```bash
   git status --short
   git diff --stat '@{upstream}' --
   git diff --name-status '@{upstream}' --
   git diff '@{upstream}' --
   ```

   这组差异必须作为统一语义视图；不要改用 `HEAD`，否则会漏掉尚未进入上游的本地提交。

3. 获取未跟踪文件并检查其实际内容：

   ```bash
   git ls-files --others --exclude-standard
   ```

4. 只执行只读命令。不得运行 `fetch`、`pull`、`push` 或任何网络命令，也不得执行 `add`、`commit`、`reset`、`checkout` 等修改仓库状态的操作。

如果不在 Git 仓库、处于 detached HEAD、没有本地上游跟踪引用或没有任何改动，只输出一行明确原因；不要退回使用 `HEAD`，也不要编造提交信息。

## 类型选择

根据主要改动目的而不是文件数量或文件名选择类型：

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

## 输出契约

最终输出严格为一行：

```text
<type>：<具体中文摘要>
```

- 类型使用小写英文，类型与摘要之间使用中文全角冒号 `：`，不添加作用域和结尾句号。
- 摘要描述业务能力、用户行为或系统效果，不出现具体类名、方法名、变量名或文件名。
- 以主要目标为中心，最多用“并”连接两个紧密相关的结果，不按文件罗列改动。
- 输出前通读摘要；若同一词在短句中重复出现，改写为“原因导致结果”的自然表达。例如，将“避免重复提交重复创建订单”改为“修复重复提交导致订单多次创建的问题”。
- 使用具体动词和结果，避免“更新代码”“优化功能”“修复问题”“调整逻辑”“完善项目”“修改相关内容”等宽泛表述。
- 只输出提交信息本身，不添加 Markdown、引号、改动列表或判断过程。

示例：

```text
feat：新增文件上传功能并添加大小限制
```

## 常见错误

- 分别比较 `HEAD`、暂存区和工作区：会遗漏上游之后的本地提交。应统一比较 `@{upstream}` 与当前工作区。
- 只读取 `git diff`：会遗漏未跟踪文件。应单独列出并检查其内容。
- 按新增文件数量选择 `feat`：类型应由整体改动目的决定。
