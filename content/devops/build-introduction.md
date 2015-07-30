+++
categories = ["devops"]
date = "2015-05-09T00:00:00+08:00"
description = "尝试去描述现有Build系统架构，更好的去构建Ctrip Build平台，追求软件开发，交付的一致性体验，避免做Build工程师"
keywords = ["Build","CMS","Gulp","Maven","Gradle","CD"]
title = "Build系统介绍"
draft = true

+++

>好的IDE做Build工具的Wrapper，Build平台也应做Build工具的Wrapper，大量散乱的Build脚步应被组织起来，进而进化为Build工具

## 简介

现代Build系统，repo 分享的舞台，中转站，生产与消费，依赖关系图，有向无环图。

大量散乱的脚步，Build工具，而能发挥最大能力的Build平台。至于Build脚本，交给开发人员吧。

![](/images/devops/deg.png)

## SCM

## Configuration Manager System

虽然仅仅是flavor，可用抽象为独立的服务，并且最好抽象为独立的服务

## Profile

1. 平台的独立性
2. 不同的调料

## Script/DSL

## Repository

提供了消费者提供者的舞台，内部繁荣。利于模块化的实践，在facebook专门开发工具，鼓励代码小模块的实践，加速构建速度。

中心化，所有被依赖的产出注册

结合git的tag管理，充分利用scm和代码密切联系，减少二次存放

本地缓存，局域网代理，缓存，高可用。

## Lifecycle

## Task/Goal



Compiling[compiling] computer Source_code[source code] into Binary_code[binary code]

Software_package_(installation)[packaging] Binary_code[binary code]

Test_automation[automated tests]

Software_deployment[deploying] to production systemcreating documentation and/or Release_notes[release notes]

## Best Practices

1. Build Script 由开发维护，作为代码的一部分
2. 一致性，本地，server端。
3. 关注点分离，自包容的完整的输入输出及处理周期。
4. 根本上关注构建体验，分而治之。

## References

[Overview of  Build](http://www.cs.virginia.edu/~dww4s/articles/build_systems.html)

http://devops.com/2014/07/29/continuous-delivery-pipeline/

[版本](http://semver.org)

http://www.infoq.com/presentations/cd-gradle-jenkins
