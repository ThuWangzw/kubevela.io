---
title: 系统架构
---

KubeVela 的整体架构如下所示：

![kubevela-arch](../resources/system-arch.jpg)

## KubeVela 是一个控制平面系统

KubeVela 本身是一个的应用交付与管理控制平面，它架在 Kubernetes 集群、云平台等基础设施之上，通过开放应用模型来对组件、云服务、运维能力、交付工作流进行统一的编排和交付。KubeVela 这种与基础设施本身完全解耦的设计，很容易就能帮助你面向混合云/多云/多集群基础设施进行应用交付与管理。

而为了能够同任何 CI 流水线或者 GitOps 工具无缝集成，KubeVela 的 API（即开放应用模型）被设计为是声明式、完全以应用为中心的，它包括：

- 帮助用户定义应用交付计划的 `Application` 对象
- 帮助平台管理员通过 CUE 语言定义平台能力和抽象的 `X-Definition `对象
  - 比如 `ComponentDefinition`、`TraitDefinition` 等

在具体实现上，KubeVela 依赖一个独立的 Kubernetes 集群来运行。这其实是一个“有意为之”的设计：云原生社区中大量的实践已经证明“构建一个科学的、健壮的控制平面系统”，正是 Kubernetes 项目最擅长的工作。所以，依赖 Kubernetes 作为控制平面集群这个选择，虽然会增加一定的部署难度，却能够让我们以最原生的方式为大规模应用交付带来至关重要的“确定性”、“收敛性”和“自动化能力”。

具体来说，KubeVela 本身主要由如下几个部分组成:

- **核心控制器** 为整个系统提供核心控制逻辑，完成诸如编排应用和工作流、修订版本快照、垃圾回收等等基础逻辑
- **模块化能力控制器** 负责对 X-Definitions 对象进行注册和管理。
- **插件控制器** 负责注册和管理 KubeVela 运行所需要的第三方插件，比如 VelaUX、 Flux、Terraform 组件等等。
- **UI 控制台和 CLI** UI 控制台服务于希望开箱即用的开发者用户，CLI 适用于集成 KubeVela 和终端管理的用户。

### 运行时基础设施

运行时基础设施是应用实际运行的地方。KubeVela 本身是完全与这些基础设施无关的，因此它允许你面向任何环境（包括 Kubernetes 环境，也包括非 Kubernetes 环境比如云平台和边缘设备等）去交付和管理任何类型的应用。

## KubeVela 是可编程的

现实世界中的应用交付，往往是一个比较复杂的过程。哪怕是一个比较通用的交付流程，也会因为场景、环境、用户甚至团队的不同而千差万别。所以 KubeVela 从第一天起就采用了一种“可编程”式的方法来实现它的交付模型，这使得 KubeVela 可以以前所未有的灵活度适配到你的应用交付场景中。

![kernel](../resources/kernel.png)

如果要详细学习 KubeVela 的可编程文档，欢迎查看文档网站中 [自定义扩展](../platform-engineers/oam/oam-model) 部分。

## 下一步

- 查看 [实践教程](../tutorials/webservice)，了解更多使用场景和最佳实践。
- 查看 [操作手册](../how-to/dashboard/application/create-application)，一步步了解更多的功能。