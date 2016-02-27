+++
categories = ["devops"]
date = "2015-05-09T00:00:00+08:00"
description = "尝试去描述现有Build系统架构，更好的去构建Ctrip Build平台，追求软件开发，交付的一致性体验，避免做Build工程师"
keywords = ["Build","CMS","Gulp","Maven","Gradle","CD"]
title = "Build系统介绍"

+++

>好的IDE做Build工具的Wrapper，Build平台也应只做Build工具的Wrapper，大量散乱的Build脚本应被组织起来，演变为Build工具

## 10000公里俯瞰Build

Build体系中包括Build平台，Build工具，Build脚本。大量散乱的Build脚本，只会导致各种Build工程师的产生，它应进化为一种Build工具。Build平台应该最大力度的发挥Build工具的能力，至于Build脚本，交给用户(开发者)吧，只有他们有责任和欲望演进构建脚本代码，我们应致力于Build平台体验和构建工具的引入与研发。

当代Build平台,它应该能提供规范统一，集中的构建分享舞台，加快构建的生产与消费。

Build工具本质上，是对文件的处理，加工，构建出目标容器可以运行的软件。构建的过程就是输入，输出，处理的有向无环图。Build工具的优化，就是对这个有向无环图的优化，单个节点处理，多个节点输入输出的缓存/增量处理，图流向的优化，并行处理等。

Build脚本，自然就是对输入，输出，处理的描述，从一开始用文本，xml，再到DSL，到代码，是工程师对Build脚本认知的成熟体现。


![](https://raw.githubusercontent.com/cosyman/cosyman-hugo/master/static/images/devops/deg.png)

## SCM
Build的原材料来自VCS，但它依赖的中间产物，产生的中间产物，不应该被上传至VCS。Build脚本应视作代码。

## Configuration Manager System

虽然仅仅是flavor，可以抽象为独立的服务，并且最好抽象为独立的服务

## Profile

1. 平台的独立性
2. 不同的调料,当发现api传递很多参数时，应该考虑这些参数是否需要暴露，然后分组，只暴露profile。

## Script/DSL
DSL是通用语言发展到一定阶段的必然产物，Build DSL的产生意味着Build工具的描述能力不再受限制

## Repository

提供了构建消费者和提供者的舞台，这也是一个平台繁荣的必要条件。它利于模块化的实践，在facebook专门开发工具，鼓励代码小模块的实践，加速构建速度。

仓库管理的中心化，布局的标准化，让开发者专注于构建的使用和集成

结合git的tag管理，充分利用scm和代码密切联系，可以减少二次存放

本地缓存，局域网代理，缓存，高可用。

生产构建的格式应该与行业标准可适配，否则就意味着自造车轮，至少是封闭的，不利于引入第三方构建，是与开源的对抗

## Artifact

### Version

具体参考sem。

通常在集成初期为了开发方便，可以设置一种Time Changing版本，每次构建都会获取最新的版本，显然它应该限制在生产环境，在maven中体现为Snapshot机制

在集成趋于稳定是，可以用Dynamic Changing版本，并最终到Final版本

版本应该直接体现在构建的文件名字当中，避免不必要的错误。

### 依赖
没有依赖的项目，通常是没什么用的，Martin Fowler如是说。

大型的互联网系统，依赖图也将非常复杂，它至少支持，依赖传递与中断或排除，以及版本冲突的选择策略定制。

## Lifecycle

生命周期的定义，意味着某种构建的抽象可能性，尤其对于DotNet，Java等平台，构建本身是一种标准，比如Java中war，ear等，它可以帮助把约定胜于配置的理念发挥到极致，同时Lifecycle也通常意味着不变，对于灵活性要求极高的构建，则需要更强大的DSL来帮忙。

## Task Graph/Goal

对于构建有向无环图的抽象，可以看成Gradle中的TaskGraph，在Maven中则对应为Lifecycle和Goal。

Build系统引擎的优化，则是这TaskGraph的优化。调度系统如此，试框架TestNG也是如此。

## Best Practices

1. Build Script 由开发维护，作为代码的一部分。
2. 一致性，本地，server端的构建行为要一致，可以方便验证。
3. 关注点分离，self-contained的完整的输入输出及处理周期。
4. 根本上关注构建体验，分而治之。
5. 引入构建仓库。


## Cbuilder's Anti Pattern

1. SCM项目源码依赖-->SCM目录依赖-->SCM文件依赖 中间仓库，源码依赖意味着依赖的交付为源码，JDK的开发中比如jshell，http2
2. BuildScript过重，没有转给开发，Build Engineer的出现


## Develop Build Tool

1. Build 是严肃的，稳定
2. Build 应该被合理的组织


## References

- https://en.wikipedia.org/wiki/List_of_software_package_management_systems
- [Overview of  Build](http://www.cs.virginia.edu/~dww4s/articles/build_systems.html)
- [淘宝Maven培训](http://www.open-open.com/doc/view/4058453cde4b429c82ff2807d8aa81f0)
- http://devops.com/2014/07/29/continuous-delivery-pipeline/
- [版本](http://semver.org)
- http://www.infoq.com/presentations/cd-gradle-jenkins
- [NuGet Package Name](http://blog.nuget.org/20150729/Introducing-nuget-uwp.html)
- [Dependency Design](https://dzone.com/refcardz/designing-quality-software)
- [Repository Management](https://dzone.com/refcardz/getting-started-repository)
