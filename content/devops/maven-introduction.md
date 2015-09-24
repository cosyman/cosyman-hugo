+++
categories = []
date = "2015-08-01T09:54:36+08:00"
description = ""
keywords = []
title = "Maven 介绍"
draft = true
+++

## 分享内容

* Build 简介
* Maven 核心概念
* M2Eclipse 使用


## Build 简介

有向无环图

Android Build Flow

Artifact Repository的构建

现实生活，基于Profile的构建

IDE，Jenkins 发挥到极致


## Maven的核心概念

### 坐标(Coordinates)

* groupId
* artifactId
* version
 + MajorVersion: 1.2.1
 + MinorVersion: 2.0
 + IncrementalVersion: 1.2-SNAPSHOT  Changing version
 + Qualifier: 1.2-beta-2 4.2.1-RC
 + 版本不脱离代码，可读性友好的
* classifier javadoc,jdk15,

### Dependency

* 依赖范围(Scope)
  * compile
  * provided 目标容器提供
  * runtime  编译不需要，运行容器需要
  * test  打包不会打进去
  * system  比如tools.jar
  * import 依赖做成可重用的
* optional 依赖不被传递
* type 默认jar

* 依赖管理
  * 依赖最小必要
  * 避免循环
  * parent pom 统一管理版本，配置插件

### Artifact 查找

http://search.maven.org/
http://mvnrepository.com/
https://bintray.com/bintray/jcenter
IDE  reindex


### Archetype
框架，快速开始（节约很多精力)，最佳实践

### Profile

不限于环境，如测试分层，分组。
配合filter处理


### Lifecycle

Phase and Goal


### Maven 项目目录结构

src/main/java	| Application/Library sources
--------------|---------------------------
src/main/resources |Application/Library resources
src/main/filters | Resource filter files
src/main/webapp	| Web application sources
src/test/java	| Test sources
src/test/resources | Test resources
src/test/filters	| Test resource filter files
src/assembly	| Assembly descriptors
LICENSE.txt	| Project's license
README.txt	| Project's readme

* 测试代码不是二等公民，是代码，配置属性是代码，资源文件是代码
* filer classpath/webapp classpath

### Maven 常用插件

* [maven-antrun-plugin](http://maven.apache.org/plugins/maven-assembly-plugin/)
* [maven-dependency-plugin](http://maven.apache.org/plugins/maven-dependency-plugin/)
* [maven-enforcer-plugin](http://maven.apache.org/plugins/maven-enforcer-plugin/)
* [maven-surefire-plugin](http://maven.apache.org/plugins/maven-surefire-plugin/)
* [exec-maven-plugin](http://mojo.codehaus.org/exec-maven-plugin/)
* [versions-maven-plugin](http://mojo.codehaus.org/versions-maven-plugin/)
* [jetty-maven-plugin](http://www.eclipse.org/jetty/documentation/current/jetty-maven-plugin.html)
* [tomcat7-maven-plugin](http://tomcat.apache.org/maven-plugin-2.2/index.html)

### SCM
 + pom.xml 顶层目录
 + readme
 + .gitignore  target/  .settings/

### 安装
 repository 配置

## M2Eclipse

* Preferences 配置
* New/Import Maven Project
* Project 右键菜单
* Build&Run&Debug
 + 尽量使用 IDE Project的Debug
 + 本质就是起jre的时候有个端口，但remote debug开发时稍麻烦
 + mvnDebug -DforkCount=0 test
* Pom Editor


## Maven.next

1. Maven 4.0  multimoduleproject .mvn 松散
  + [Maven's Inflexibility Is Its Best Feature](https://timboudreau.com/blog/maven/read)
  + polyglot atom,clojure,groovy,ruby,scala,yaml  translate existing pom
2. Gradle
 + DSL over xml
 + convention is good and so is flexibility
3. SBT    
4. Gulp
  + easy to use
  + code over configration
  + every thing is stream/pipelines


### References

[依赖策略](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html)

[标准目录布局](http://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html)

[Maven文章列表](http://maven.apache.org/articles.html)

[Maven官方文档索引](http://maven.apache.org/guides/index.html)

[NuGet Package Name](http://blog.nuget.org/20150729/Introducing-nuget-uwp.html)

[依赖设计](https://dzone.com/refcardz/designing-quality-software)

[Repository Management](https://dzone.com/refcardz/getting-started-repository)

[Android Build Flow](http://tools.android.com/tech-docs/new-build-system/build-workflow)

[M2e leader](http://takari.io/blog.html)

[M2e documentation](http://www.eclipse.org/m2e/documentation/m2e-documentation.html)

[M2e FAQ](http://www.eclipse.org/m2e/documentation/m2e-faq.html)

[Introduction-to-m2eclipse](http://www.theserverside.com/news/1363817/Introduction-to-m2eclipse)

[Maven for building Java applications - Tutorial](http://www.vogella.com/tutorials/ApacheMaven/article.html)

[国内总结的Maven Example](https://github.com/v5developer/maven-framework-project)

[mkyong's Maven tutorials](http://www.mkyong.com/tutorials/maven-tutorials/)

[淘宝Maven培训](http://www.open-open.com/doc/view/4058453cde4b429c82ff2807d8aa81f0)

[Maven reference book](http://books.sonatype.com/mvnref-book/reference/)

[徐晓斌InfoQ Maven 实战](http://www.infoq.com/cn/author/%E8%AE%B8%E6%99%93%E6%96%8C#全部)

[乔梁CD](http://www.continuousdelivery.info/)

[理解Maven依赖调解](http://guntherpopp.blogspot.com/2011/02/understanding-maven-dependency.html)

[比较好的Maven培训PPT](http://wenku.baidu.com/link?url=Xxvo2Zvgjh5HmsEajQv-rJbwE-hsNHXNQ06Zo0_nG7nMzS2ZsemR5Tvb48woSkHEaOgqw7x8sEQ8yom9iW5gCWKDNt6jbSpTki_cQbwcb0m
)
