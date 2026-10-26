# DevFlow 测试仓库说明

## 项目用途

本仓库由 HTTPX fork 而来，用于体验 DevFlow AI 的仓库同步、Issue 分析、PR 评审、CI 排障、项目索引和知识检索。测试用改动仅位于本仓库。

## 正确版本

默认分支是 `master`。演示函数位于 `demo/calculator.py`，`add(a, b)` 应返回 `a + b`。

运行以下命令，预期输出为 `5`：

```text
python -c "from demo.calculator import add; print(add(2, 3))"
```

## 故障样例

分支 `test/broken-add` 故意将实现改为 `return a - b`。关联缺陷为 Issue #1，关联变更为 PR #2。此时 `add(2, 3)` 返回 `-1`。这份故障 PR 用来验证分析能力，应保持未合并，直到需要体验修复流程。

## CI 检查

演示工作流名为 `DevFlow Demo CI`，配置文件是 `.github/workflows/devflow-demo.yml`。它使用 Python 3.12，在 `Check addition` 步骤检查：

| 输入 | 正确结果 |
| --- | --- |
| add(2, 3) | 5 |
| add(-2, 3) | 1 |
| add(0, 0) | 0 |

故障分支的预期错误为 `AssertionError: add(2, 3): expected 5, got -1`。修复方式是把实现改回 `return a + b` 并提交到该分支。

仓库还继承了 HTTPX 的 `Test Suite` 工作流；排查本演示时应区分它与 `DevFlow Demo CI` 的运行记录。

## 需求样例

- Issue #1：add 计算结果错误，适合体验缺陷分诊与代码定位。
- Issue #3：增加 HTTP 请求超时与重试示例，适合体验需求拆解与负责人推荐。
- Issue #4：补充本地演示与 CI 排障文档，适合体验文档分类和周报汇总。

## 知识检索问题

1. 演示函数在哪个文件，默认分支是什么？
2. 故障分支为什么让 add(2, 3) 返回 -1？
3. 哪个 CI 步骤失败，预期与实际结果分别是什么？
4. 如何修复故障，修复后应通过哪些检查？

建立项目索引时，本文件可作为 `project_doc` 被收集。也可以下载后上传至知识库，用于检查切片、向量检索和带引用问答。
