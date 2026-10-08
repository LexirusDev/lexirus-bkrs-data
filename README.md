# Lexirus BKRS data snapshot

## Summary

This repository is intended to distribute the BKRS snapshot used by Lexirus. The app package applies cleanup to displayed definitions while retaining source DSL fields for traceability. It is an app-specific binary, not a source-free cleaned text export. Please credit BKRS; see “Third-party dictionary data and terms” below.

Lexirus 使用的 BKRS 词库快照。数据来自 BKRS 官方 2026-08-30 每日版；Lexirus 对产品显示层做了拼音、英文片段和排版残片清理，同时保留俄语及其重音。

## 下载文件

从 GitHub Release 下载 `bkrs.lexdb`：

- 快照：`260830.6`
- 记录数：4,633,605
- 文件大小：1,124,354,013 字节（约 1.05 GiB）
- SHA-256：`40e49c5dd41d07ff40ff678e3be5a5cecbaffcdd3e8d0faab4a554ff4843826f`
- 格式：Lexirus 应用使用的压缩词库包，不是通用 DSL 或 SQLite 文件；供 Lexirus 离线词典使用。

| 数据方向 | 上游快照文件 | 记录数 | 上游压缩文件 SHA-256（应用清单记录） |
| --- | --- | ---: | --- |
| 俄汉 | `dabruks_260830.gz` | 255,351 | `f931f3b166b94bff33be22b4f886900771e8668e7900e74e87b123766ae89606` |
| 汉俄 | `dabkrs_260830.gz` | 3,459,626 | `7eabdd4cc08bd09dee6e1fdeaa93e79a763feb24ed8d9c7fff7d5cbff6b98cdc` |
| 例句 | `examples_260830.gz` | 918,628 | `a98a458e24f1f20ce69862923a7d298e638f3fc4336fffd7d8d15ab63742ff83` |

## 处理方法

清理只作用于 Lexirus 的显示内容；包内仍保留来源记录的 `raw_dsl`、原词头和稳定键，便于追溯。

- 从显示正文中删除拼音（含声调和不带声调的片段）、拼音单独行和英文/拉丁片段。
- 俄语和重音保留。俄语单词中误混入的拉丁形似字母转换回西里尔字母，避免删掉俄语词或重音，例如 `Кóса` 修为 `Ко́са`。
- 清理 DSL 方括号标记、未配对括号符号、项目符号、首尾破折号、空括号和重复分隔符；保留括号内有意义的中文/俄语内容与义项结构。
- 对无法作为中文释义的俄语纯文本正文，只从产品显示层隔离，不伪写中文翻译；原始来源记录仍在包内。

快照清单记录的处理计数：

| 操作 | 次数 |
| --- | ---: |
| 移除拉丁/英文片段 | 5,140,203 |
| 移除拼音片段 | 130,058 |
| 移除独立拼音行 | 7,723 |
| 修复俄语重音/拉丁形似字符 | 1,501 |
| 规范中文括号 | 20,269 |
| 规范替代括号 | 26,874 |
| 移除项目符号 | 1,605 |
| 移除首尾破折号标记 | 5,438 |
| 移除未配对括号符号 | 4,359 |
| 从显示层隔离无中文释义的俄语正文 | 8,904 条记录 |

这些是清理操作计数，可能有重叠，不代表唯一受影响记录数，也不代表上游词条的语义和拼写错误已经全部校订。该处理针对显示层拼音、英文和标记残片；不宣称所有类型的编码错乱都已逐条人工修复。

## 第三方词典资料与许可

**BKRS。** Lexirus 包含来自 [bkrs.info](https://bkrs.info/p47) 的 BKRS 词典资料，本地来源记录标注为 2026 年 8 月 30 日导出。BKRS 数据库下载页说明其数据库可自由用于任何目的，并请使用者注明来源。Lexirus 对此处所述 BKRS 资料依据该公开说明使用。该说明适用于 BKRS 页面描述的资料和条款；原始词条的所有权并未因此转移给 Lexirus。

Lexirus 为本地索引、压缩存储和显示校订对这些资料进行处理。适用时，应用随附的第三方内容声明会列明来源、许可及修改信息。原始内容仍受各自来源及贡献者的权利和条款约束。开源组件和字体分别适用各自的许可声明。Lexirus 独立开发；提及来源不表示与其存在关联或获得其背书。

## 内容边界

这份文件是 Lexirus 的应用数据包。它包含原始 DSL 字段及经过清理的显示层，面向 Lexirus 应用使用；它不是不含原始来源内容的通用清理文本导出。
