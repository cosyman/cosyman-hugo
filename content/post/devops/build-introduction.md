+++
categories = ["devops"]
date = "2015-05-09T00:00:00+08:00"
description = "尝试去描述现有Build系统架构，更好的去构建Ctrip Build平台，追求软件开发，交付的一致性体验，避免做Build工程师"
keywords = ["Build","CMS","Gulp","Maven","Gradle","CD"]
title = "Build系统介绍"

+++

>好的IDE做Build工具的Wrapper，Build平台也应只做Build工具的Wrapper，大量散乱的Build脚本应被组织起来，演变为Build工具

## 10000公里俯瞰Build

Build体系中包括Build平台，Build工具，Build脚本，大量散乱多Build脚本，只会导致各种Build工程师的产生，它应进化为一种Build工具。而Build平台可以最大力度的发挥Build工具的能力，至于Build脚本，交给用户(开发者)吧，只有他们有责任和欲望演进构建的脚本代码，我们应致力于Build平台体验和构建工具的引入与研发。

现代Build系统,构建分享的舞台，中转站，生产与消费，依赖关系图，有向无环Task图。


![](https://raw.githubusercontent.com/cosyman/cosyman-hugo/master/static/images/devops/deg.png)

## SCM

## Configuration Manager System

虽然仅仅是flavor，可用抽象为独立的服务，并且最好抽象为独立的服务

## Profile

1. 平台的独立性
2. 不同的调料,当发现api传递很多参赛时，应该考虑这些参数是否需要暴露，是否是开放决定的，然后分组，暴露profile

## Script/DSL

## Repository

提供了消费者提供者的舞台，内部繁荣。利于模块化的实践，在facebook专门开发工具，鼓励代码小模块的实践，加速构建速度。

中心化，所有被依赖的产出注册

结合git的tag管理，充分利用scm和代码密切联系，减少二次存放

本地缓存，局域网代理，缓存，高可用。

## Artifact

### Version

具体参考sem。通常为了开发方便，可以设置一种time changing 版本，每次构建都会获取最新的版本，显然它应该限制在生产环境，在maven中体现为Snapshot机制

版本应该直接体现在构建的文件名字当中，避免不必要的错误。

### 依赖
大型的互联网的系统，依赖图也将非常复杂，它至少支持，依赖传递与中断或排除，以及版本冲突的选择策略定制。当然比如在Java中，可以通过ClassLoader的定义，避免版本冲突，尤其在Java9中有了更好的支持


## Lifecycle

生命周期的定义，意味着某种构建的抽象可能性，尤其对于DotNet，Java等平台，甚至每种构建都本身是一种标准，比如Java中war，ear等，它可以帮助吧约定胜于配置的理念发挥到极致，同时Lifecycle也通常意味着不变，对于灵活性

## Task Graph/Goal

同样对于Task也应是一种有向无环图，这在Gradle Gulp等工具中显得特别重要


## Best Practices

1. Build Script 由开发维护，作为代码的一部分
2. 一致性，本地，server端。
3. 关注点分离，self-contained的完整的输入输出及处理周期。
4. 根本上关注构建体验，分而治之。

## Cbuilder's Anti Pattern

1. SCM项目源码依赖-->SCM目录依赖-->SCM文件依赖 中间仓库，源码以来意味着依赖的交付为源码，JDK的开发中比如jshell，http2
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
