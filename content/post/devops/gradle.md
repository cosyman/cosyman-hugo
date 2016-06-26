# Gradle 实用指南（Draft)
Gradle 3.0 变化比较大

Android Studio

## Project
- settings.gradle
- 不超过3层

## Repository

- build repo
 - layout name version classifier
 - local remote http
- dependency reop

## Task

- 依赖，顺序，override,path,skip,ennabled,ignore execution exception
- 缓存，outputs inputs hash
- tasks rules
- custom task
- buildSrc

- dry-run
- damon
- paralize


## File

- copy,delete,filter filter on line,zip,tar,rename
- Exec

## Dependency

1. gradleApi
2. Project
3. lib

版本 alpha beta rc final,可见性
版本在构建文件明中
版本是开发，测试，产品交流的identity，而不是昨天，前天，或某一天的版本
每次代码提交都可能产生一个RC

configuration

## Plugin

apply from url/id
通常对应一种组件，android library，jar

## Variant
- jdk version/
- Market
- productFlavor+Build Type

## Configuration

- 依赖配置
- 运行时资源配置
- build 配置


## References
- [Android Plugin](http://developer.android.com/intl/ja/tools/building/plugin-for-gradle.html)
- [Next Generation Gradle](https://docs.gradle.org/current/userguide/software_model_concepts.html)
- [Tasks](https://docs.gradle.org/current/userguide/more_about_tasks.html)
- [Dispalay Convention](http://marxsoftware.blogspot.jp/2014/01/identifying-gradle-conventions.html)
- [Gradle Goodness Notebook](https://leanpub.com/gradle-goodness-notebook/read)
- [标准 plugin](https://docs.gradle.org/current/userguide/standard_plugins.html)
- [入门指南](http://www.cnblogs.com/gzdaijie/p/5285160.html)
