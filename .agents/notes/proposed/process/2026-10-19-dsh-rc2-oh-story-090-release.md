# Agent Note: DSH 0.2.1-rc.2 与 Oh Story 0.9.0 联合适配发布

Status: proposed

## Problem

0.1.16 发布后，`@deepseek-ai/dsh` 在 npm 上的 `latest` 从 `0.2.0-rc.2` 前进到 `0.2.1-rc.2`，alpha 线停在 `0.2.1-alpha.5`；README 的默认安装命令仍固定旧 rc，开发宿主还在 alpha.4。上游 Oh Story 发布 0.9.0（`agents_version` 35 → 36），按写书时刻重排 13 个 Skill 的参考资料并删除重复资料；NovelToGame 发布 0.6.0，加入预算复盘、视觉目标选择与白盒试玩代理。技能桥里写死的路径、步骤与模板需要逐条对照新版。

## Proposal

开发与打包浏览器验证宿主改为 `0.2.1-rc.2`，Cordis / Schemastery 及 Cordis 辅助包回到稳定版；README 默认安装命令改为 `0.2.1-rc.2`，`0.2.0-rc.2` 保留为旧版兼容线继续跑打包验证。`engines.dsh` 与 DSH peer 范围不变（已覆盖 0.2.1 预发布）。不再单独宣传 alpha 线：rc.2 在 semver 与发布时间上都新于 alpha.5。

通过既有同步命令更新 Oh Story 与 NovelToGame，上游源取自干净克隆的发布标签，不动本地开发中的 checkout。Drama 0.9.0 与 video-recap 0.6.2 已是最新，维持原固定点。逐条核对技能桥的上游契约，修正失效路径与原生替换 Skill 的流程描述。

发布前按 `new-user-product-audit` 方法以新用户身份从 README 安装打包候选版并完成创作任务，用真实 DeepSeek 运行；阻断级问题修复后再发版。

## Alternatives considered

- 保留 alpha.4 作为显式试用线、只把默认线改到 rc.2：多一条线能覆盖仍停在 alpha 的用户，但 rc.2 是同一 0.2.1 序列更新的版本，engines 范围已接受全部 0.2.1 预发布，继续为旧 alpha 跑完整浏览器验证收益很小。
- 默认线保持 `0.2.0-rc.2`：对已安装用户最稳，但 npm `latest` 已是 `0.2.1-rc.2`，新用户直接 `npx @deepseek-ai/dsh` 得到的就是新线，README 继续固定旧版会让说明与默认行为不一致。

## Risks

0.2.1-rc.2 首次作为默认宿主，依赖两轮打包 Chrome 验证与真实模型试用发现兼容问题。Oh Story 0.9.0 删除和合并了大量参考资料，技能桥如有遗漏的旧路径，只会在对应流程运行时暴露。
