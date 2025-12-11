---
layout: post
title: "LinkedIn如何构建企业级AI Agent平台及使用MCP"
description: "LinkedIn工程团队分享如何将AI agents从零散试验推向大规模生产级部署，以及如何使用Model Context Protocol统一agent与工具的交互"
category: 
tags: [AI, LinkedIn, MCP, Platform Engineering, Agents]
---
{% include JB/setup %}

## 概览

本文是 LinkedIn 的两位工程负责人 Karthik Ramgopal 和 Prince Valluri 与主持人 Wesley Reisz 的Podcast对话，讨论了 LinkedIn 如何构建面向企业级的 AI agent 平台，将 AI agents 从零散的试验 (proof-of-concept) 推向大规模、生产级 (production-grade) 的部署，以及在这个过程中，他们如何使用 Model Context Protocol (MCP) 来统一 agent 与工具 (tools) 的交互方式。

(本文基于ChatGPT做了机翻微调，原文链接：[Platform Engineering for AI: Scaling Agents and MCP at LinkedIn](https://www.thakurcoder.com/blog/2025-06-16-scaling-ai-agents-at-linkedin-from-framework-to-production)）

## 为什么要从 "零散 PoC" 走向 "统一平台"

在 LinkedIn，很多团队最初各自为战，自己写脚本、使用局部工具 (local tools)、做一些实验 — 虽然有价值，但方式不一致，每个团队都在重复造轮子 (plumbing、prompt orchestration、数据访问、安全评估、部署等都各行其是)。

同时，现代软件开发远不只是"打开 IDE 写几行代码然后搞定"。工程师们越来越多地参与跨系统协调 — 拉取来自多个服务的数据、综合洞见、触发工作流、然后写代码、最后走完整个 code lifecycle。很多任务是 "多步骤、有状态 (stateful)" 的。对这种任务，AI agents 特别合适。

因此，LinkedIn 认识到：与其让每个团队各自构建自己的"迷你 agent 平台"，不如 **提供一个统一、开放、可扩展 (open-ended) 的平台基础设施**。这样团队只需聚焦它们自己的领域问题 (domain problems)，而把系统性的问题 (infrastructure) 留给平台团队处理。

用更直白的话来说：AI agents 不应只是几个团队的炫技项目 (bling-bling)，而是要成为生产 (production) 级基础设施 — 和微服务 (microservices)、计算基础设施 (compute infrastructure) 同等级别来看待。

## Agent = 新的 "执行模型 (Execution Model)"

LinkedIn 把 AI agents 当作一种新的"执行模型 (execution model)"，就像微服务、容器、Kubernetes 那样，需要严肃对待、构建专业基础设施 (shared infrastructure)、确保可扩展性、可靠性、合规性、可观测 (observability) — 不能把它当成一个 feature 来搞。

为此，他们组建了专门的 "agentic 平台团队 (agentic platform team)" —— 就像负责存储基础设施 (storage infrastructure)、机器学习基础设施 (ML infrastructure) 的团队一样，专门负责整个 agent 平台的架构、流程、工具链、监控与治理。

## 用规范 (Specs) + 沙箱 (Sandbox) 保持安全 & 可控

为了让 agents 能安全、可靠、可审计地执行任务，同时又不剥夺开发者对流程的掌控，LinkedIn 设计了如下机制：

1. **开发者通过 规范 (spec / spec-driven) 来描述他们的"意图 (intent)"** —— 想进行什么更改、如何拆分任务、允许 agent 使用哪些工具 (tools)、最终结果 (acceptance criteria) 应该是什么样子。这样可以让 agent 输出相对确定 (deterministic)，让 reviewer 清楚上下文，也方便自动化验证 (automated validations) 执行。

2. **agent 执行是在 沙箱 (sandboxed) 环境 中进行**。这个环境对系统访问有严格限制 (不能随意调用所有系统)、agent 有明确定义的权限 (authentication/authorization)，agent 的身份 (identity) 可审计 (auditable)，所有调用 (tool calls) 和动作 (actions) 都可观察 (observable)。

3. **agent 做出的更改最终被封装为标准的 Pull Request (PR)** —— 就像正常人类开发者提交代码那样。PR 会经过原有的 CI/CD 流程 + 人类 review。agent 不是直接"替你写完"提交，而是"提出建议 / draft changes" + human-in-the-loop review。

这种设计既让 agent 自动化重复枯燥 (toil) 的任务，也保留了工程质量、安全性、人类判断 (engineering judgment) 的保障。

## 前台 (Foreground) Agents vs 后台 (Background) Agents

LinkedIn 把 agent 大致分为两类：

**Foreground agents** —— 开发者在 IDE 中直接与之互动 (例如使用类似 GitHub Copilot)，这些 agents 被增强 (augmented) —— 除了原有功能，还通过 MCP 工具 (MCP tools) 集成组织 / 企业上下文 (context)、语义索引 (semantic code indexes) 等，让编程体验更贴近公司实际代码库环境。

**Background agents** —— 在后台运行，负责较大的、跨系统、长期 (long-horizon) 的任务，比如大规模代码迁移 (code migrations)、依赖升级 (upgrades)、增加测试覆盖 (test coverage improvements)、清理过时 A/B 测试、重构 (refactoring)、以及生产环境的可观测性 (observability)、日志监控、自动化响应 (alert / outage response) 等 —— 这些往往是重复且容易被忽视 (low-priority but important) 的任务。

两类 agents 都很重要：foreground 适合那些开发者希望主动控制、交互频繁、需要快速试验或探索的任务；background 则适合那些结构化、可重复、规模大、可长期运行的维护任务。

## MCP 的角色 — "统一协议 + 共用工具 + 企业上下文"

为什么要用 Model Context Protocol (MCP)？LinkedIn 给出的理由是：

1. **在没有 MCP 之前，每个 AI 团队 / agent 框架 /工具 (tool) 都会用各自不同的 "function calling" 格式** — vendor-specific、service-specific，都不统一。这样虽然能用，但会造成高度碎片化 (fragmentation)，难以共享，也很难大规模推广。

2. **MCP 提供一种统一、vendor-neutral 的协议** —— 只要遵循 MCP，任何语言 (language)、任何 agent、任何工具、任何模型都能互操作 (interoperate)。这让 foreground agents 和 background agents 能够共用相同 MCP 工具 (MCP tools)、共享企业上下文 (organization context)，例如通过检索历史 PR、语义代码索引 (semantic indexes)、RAG (retrieval-augmented generation) 等获取上下文。

3. **同时，这种共享还方便治理 (governance)、合规 (compliance)、审计 (auditability)、可观察性 (observability)**，使得 agent-based workflows 达到生产级安全与可靠标准。

简而言之：MCP 是把 agent 平台从 "每个团队各自为政" 变成 "统一基础设施 + 共享工具 + 统一上下文 + 企业合规"的关键 —— 它让 AI agents 真正能够在大规模企业环境中落地 (production-ready)。

## 给做平台工程／AI 工程团队的建议

在访谈末尾，Karthik 和 Prince 给出了他们对其他组织 (做类似事情) 的建议，总结如下：

1. **投资 (invest) 于坚实的平台抽象 (platform abstractions)**：如果只是做炫技 demo，在小范围 PoC，那 AI agents 看起来好像很"神奇"。但若想推进到生产 (production)、可维护 (maintainable)、可扩展 (scalable) — 必须把基础设施 (infrastructure)、流程 (process)、工具 (tooling)、治理 (governance) 都认真建起来。

2. **理解 AI 的优势和局限 (strengths & limitations)**：AI 对某些任务 (如模式化重复任务、重构、自动化) 很擅长，但它不会取代人类判断 (human judgment)。不要把 agent 当成全能替代，而是当成协作工具 (structured collaborator) 来用。

3. **改变现有的工作方式 (work processes)**：如果公司现有流程高度依赖人工、不文档化、知识在少数人头脑中 (tribal knowledge)、缺少规范 (spec) —— 那么直接把 AI agents 插入进去，很难获得成效。必须先把流程标准化 (documented)、上下文明确、规范流程 (spec-driven)，这样 AI 才真正有用。

4. **重视 Evals (评估机制)**：不要把 evals 视为"第二阶段 (phase two)"才考虑。它们应当从一开始就设计为核心 (core) 一部分，用来衡量 agent 系统是否真正改进、是否有 regressions。

5. **聚焦于公司自己的上下文 (domain context / company-specific context)**：不要盲目试图重造 (recreate) 像 GitHub Copilot、Cursor、Replit 那样通用 agent。相反，先思考哪些是你公司 / 团队中重复率高、耗时费力、价值高 (high-impact) 的工程任务，然后针对这些任务构建 agent/workflow，会最划算、回报最高。

## 其他资料

- [Scaling AI Agents at LinkedIn: From Framework to Production](https://www.thakurcoder.com/blog/2025-06-16-scaling-ai-agents-at-linkedin-from-framework-to-production) - 被采访对象早期发文，感兴趣可以看下细节架构
