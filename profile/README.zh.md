# WDL

> English version: [README.md](README.md)

WDL 是一套开放基础设施，用于在你自己运维的基础设施上运行 Workers 形态的应用。

WDL 是基于 stock Cloudflare workerd 的自托管多租户 Workers 平台。它保留 Workers programming model 和 Wrangler-shaped workflow，并在 workerd 外侧补齐 platform layer：租户路由、control API、auth、KV、R2、D1、Durable Objects、Queues、Cron、Workflows、静态资源、bindings、secrets、logs、metrics，以及部署生命周期工具。

这个 platform 面向单区域生产运行，不只是 demo stack。D1 和 Durable Objects 具备明确 failover 语义，runtime、scheduler 和 Workflows 具备多副本安全的 dispatch 路径。Operator 仍然负责容量规划、Redis/Valkey 和 storage durability、ingress protection，以及区域级灾备。

## 仓库

| 仓库 | 内容 |
| --- | --- |
| [`wdl-dev/wdl`](https://github.com/wdl-dev/wdl) | WDL platform runtime 和 control plane。架构、HA/failover、运维、兼容性、安全模型和交付路径从这里开始。 |
| [`wdl-dev/cli`](https://github.com/wdl-dev/cli) | 租户 CLI，发布为 [`@wdl-dev/cli`](https://www.npmjs.com/package/@wdl-dev/cli)。用于初始化项目、通过 Wrangler dry-run 本地 bundle、部署不可变 worker version、管理资源和 tail 日志。 |
| [`wdl-dev/site`](https://github.com/wdl-dev/site) | 公开 [wdl.dev](https://wdl.dev/) site。它是一方 WDL Worker，并通过和普通 tenant application 相同的 CLI 路径部署。 |
| [`wdl-dev/chat`](https://github.com/wdl-dev/chat) | [chat.wdl.dev](https://chat.wdl.dev/)，一个构建 WDL Workers 的参考 demo WDL Worker：AI agent、MicroVM sandbox、临时 namespace 部署和 preview URL。 |
| [`wdl-dev/aws-sigv4`](https://github.com/wdl-dev/aws-sigv4) | 面向 web-standard runtimes 和 S3-compatible object storage 的小型零依赖 AWS SigV4 signer，发布为 [`@wdl-dev/aws-sigv4`](https://www.npmjs.com/package/@wdl-dev/aws-sigv4)。 |

一方仓库也会放在这里。公开 WDL site 和 WDL Chat 都是部署到 WDL 上的普通 Workers：用 WDL 把一方应用部署到 WDL。

## 入口

应用开发者用 `wdl` 把 Workers-shaped projects 部署到平台运维方运行的 WDL platform。CLI 不会把代码发到 Cloudflare；`wdl deploy` 只使用 Wrangler 做本地 bundling。

平台运维方在自己的 infrastructure 上运行 WDL。先读平台的[架构](https://github.com/wdl-dev/wdl/blob/main/docs/architecture.zh.md)、[安全模型](https://github.com/wdl-dev/wdl/blob/main/docs/security.zh.md)和[兼容矩阵](https://github.com/wdl-dev/wdl/blob/main/docs/compatibility.zh.md)。

WDL 开发者的工作分布在 platform、CLI、support packages、docs、examples 和一方 Workers 之间。一方应用应通过和普通 tenant workload 相同的 CLI 和 control plane 部署。

## Dogfooding

WDL 通过运行真实应用来开发。公开 site 是 hosted preview 上的一方 Worker。WDL Chat 是更大的参考 demo：一个运行在 WDL 上的 AI-assisted Worker 开发应用，可以生成 WDL Worker 代码、部署到临时 namespaces，并调用 preview URL。

## Cloudflare

WDL 围绕 stock workerd 构建，不 fork workerd。WDL 独立于 Cloudflare, Inc.；Cloudflare、Cloudflare Workers、Wrangler 和 workerd 是 Cloudflare, Inc. 的商标或注册商标。

## 链接

文档放在各自仓库中。Docker images 发布为 [`getwdl/wdl-workerd`](https://hub.docker.com/r/getwdl/wdl-workerd) 和 [`getwdl/wdl-rust`](https://hub.docker.com/r/getwdl/wdl-rust)。npm packages 发布在 [`@wdl-dev`](https://www.npmjs.com/org/wdl-dev) 下。联系：<hi@wdl.dev>。

除非另有说明，这个组织里的 WDL 项目以 Apache License 2.0 发布。
