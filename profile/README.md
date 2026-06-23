# WDL

> Chinese version: [README.zh.md](README.zh.md)

Open infrastructure for running Workers-style applications on infrastructure you
operate.

WDL is a self-hosted, multi-tenant Workers platform built on stock Cloudflare
workerd. It keeps the Workers programming model and Wrangler-shaped workflow,
then adds the platform layer around workerd: tenant routing, control APIs, auth,
KV, R2, D1, Durable Objects, Queues, Cron, Workflows, static assets, bindings,
secrets, logs, metrics, and deployment lifecycle tooling.

The platform targets single-region production operation rather than a demo-only stack.
D1 and Durable Objects have explicit failover semantics, while runtime, scheduler, and
Workflows dispatch paths are designed to be multi-replica safe. Operators still own
capacity planning, Redis/Valkey and storage durability, ingress protection, and regional
disaster recovery.

## Repositories

| Repository | What it is |
| --- | --- |
| [`wdl-dev/wdl`](https://github.com/wdl-dev/wdl) | The WDL platform runtime and control plane. Start here for architecture, HA/failover, operations, compatibility, security, and deployment paths. |
| [`wdl-dev/cli`](https://github.com/wdl-dev/cli) | The tenant CLI, published as [`@wdl-dev/cli`](https://www.npmjs.com/package/@wdl-dev/cli). Use it to initialize projects, bundle with Wrangler dry-run, deploy immutable worker versions, manage resources, and tail logs. |

More first-party repositories will live here as the project opens up. The public
WDL site at [wdl.dev](https://wdl.dev/) is a normal Worker deployed to the WDL
hosted preview: a first-party application deployed by WDL onto WDL.

## Start Points

Application developers use `wdl` to deploy Workers-shaped projects to an
operator-run WDL platform. The CLI never sends code to Cloudflare; `wdl deploy`
uses Wrangler only for local bundling.

Operators run WDL on their own infrastructure. Start with the platform
[architecture](https://github.com/wdl-dev/wdl/blob/main/docs/architecture.md),
[security model](https://github.com/wdl-dev/wdl/blob/main/docs/security.md), and
[compatibility matrix](https://github.com/wdl-dev/wdl/blob/main/docs/compatibility.md).

WDL developers work across the platform, CLI, docs, examples, and first-party
Workers. First-party apps should deploy through the same CLI and control plane
as ordinary tenant workloads.

## Dogfooding

WDL is developed by running real applications on it. The public site is a
first-party Worker on the hosted preview. WDL Chat is the larger internal
dogfooding workload: an AI-assisted Worker development app that runs on WDL,
generates WDL Worker code, deploys it to test namespaces, and calls the preview
URL.

## Cloudflare

WDL builds around stock workerd instead of forking it. WDL is independent of
Cloudflare, Inc.; Cloudflare, Cloudflare Workers, Wrangler, and workerd are
trademarks or registered trademarks of Cloudflare, Inc.

## Links

Docs live with each repository. Docker images are published as
[`getwdl/wdl-workerd`](https://hub.docker.com/r/getwdl/wdl-workerd) and
[`getwdl/wdl-rust`](https://hub.docker.com/r/getwdl/wdl-rust). Contact:
<hi@wdl.dev>.

Unless stated otherwise, WDL projects in this organization are released under
the Apache License 2.0.
