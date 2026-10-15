# Agent Note: 同步已审阅的上游技能文档

Status: implemented

## Problem

四套固定知识资产仍指向本轮精修前的提交。只修改上游仓库和 DSH 自有指南，会让插件继续加载旧指令；手改 knowledge 副本又会破坏固定来源与哈希约定。

## Decision

按现有专用 assets:sync 命令，从已审阅且经 PR 合入的四个上游提交同步技能、所需参考和角色真源；不手改固定目录。对应 manifest 记录真实提交与逐文件摘要，当前 README 只更新所含 Drama Skills 的版本事实，CHANGELOG 逐一记录四套版本和提交。源技能已保护的 badcase 和配对随原文继承，不新增兼容读取或插件运行时逻辑。

## Alternatives considered

- 手改副本的文字最容易控制单次差异，但副本会偏离上游且后续同步覆盖修改，故维持专用同步。
- 固定旧提交可缩小本 PR，但会继续向插件使用者提供已纠正的旧指令，故跟随已审主线。

## Consequences

同步会带入已由上游审阅的文档契约调整，需要完整 parity、边界、单测与构建验证；源码版本仍沿用当前版本，不因此声称产生新的 release 或真实 provider 结果。

## Verification

四套资源由现有同步命令从已合并提交复制，887 文件及 7 Roles 与实际来源逐字一致。Drama 五份示例与登记摘要、字节数和新提交中的原文完全一致，仅将 sources.json 的 drama commit 更新为新固定来源；不宣称重新生成，不改样例、日期、历史输出或守卫。最终 pnpm verify 全部通过（lint、typecheck、四套 parity、DSH 边界、16 release tests、3 upstream-update tests、173 unit tests 与 build）；此前来源字段未同步的失败日志保留。插件版本、TypeScript 运行时与付费调用不变。收益是插件加载已审文档，代价是同步差异必须逐来源核对。

固定来源：

- oh-story：`747b8e30d1e5993dbfb04f38593e1bf36847cab4`
- drama：`dafe80ee390ec8be5a7ec8dd156a84d511f8e7dd`
- novel-to-game：`25e264dc32a82ee2e481b21d22d40874ea84ab27`
- video-recap：`5785c33d8b5172cfa2837a8a0d57eb4b87837475`
