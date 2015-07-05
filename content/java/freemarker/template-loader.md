+++
categories = ["java"]
date = "2015-01-09T00:00:00+08:00"
description = ""
keywords = ["Build","CMS","Gulp","Maven","Gradle","CD"]
title = "Freemarker Template"
draft = true

+++

Java中不乏优秀的模板引擎，Velocity,[mvel](https://github.com/mvel/mvel),FreeMarker等。在构建框架的时候，通常可以拿来即用，但我们需要控制它。最近需要一个数据准备的框架，便选择了FreeMarker，FreeMarker使用起来很简单，data+template=out.今天主要写一下其中template加载组件TemplateLoader

## TemplateLoader的实现

作为一个模板文件加载的抽象，自然不能限制模板来自何方，在FreeMarker中由几个主要的实现类来体现，这些TemplateLoader是可以独立使用的，Webapp需要Servlet环境。当然你可以实现自己的TemplateLoader.

* StringTemplateLoader 直接将内存中的String对象放入并使用
* FileTemplateLoader 本地文件目录
* ClassTemplateLoader ClassPath 加载
* WebappTemplateLoader  ServletContext
* MultiTemplateLoader 多个TemplateLoader的叠加，顺序按照数组的顺序优先加载

### StringTemplateLoader
刚开始总觉得StringTemplateLoader简单，其实挺麻烦，而且也无大用。

```java
@Test
public void testStringTL() throws IOException {
	StringTemplateLoader stl = new StringTemplateLoader();
	String template = "${key}";
	stl.putTemplate("hello", template);
	Object source = stl.findTemplateSource("hello");
	Reader reader = stl.getReader(source, "utf-8");
	String dest = IOUtils.toString(reader);
	Assert.assertEquals(template, dest);

}
```

### MultiTemplateLoader
TemplateLoader是可以多种类型，同种类型组合起来使用的，查询顺序按照数组的顺序优先。
```java
@Test
public void testMultiTL() throws IOException {
	TemplateLoader ctl = new ClassTemplateLoader(TemplateLoaderTest.class,
			"/");
	TemplateLoader ftl1 = new FileTemplateLoader(new File(
			System.getProperty("user.dir")));
	MultiTemplateLoader mtl = new MultiTemplateLoader(new TemplateLoader[] {
			ftl1,ctl  });

	Object source = mtl.findTemplateSource("test.ftl");
	Reader reader = mtl.getReader(source, "utf-8");
	String dest = IOUtils.toString(reader);
	Assert.assertEquals("${hello}", dest);
}
```

## 通常在Configuration中使用，才能方便的处理FreeMarker的表达式
```java
@Test
public void testInConfiguration() throws IOException {
	Configuration configuration = new Configuration(
			Configuration.VERSION_2_3_21);
	configuration.setDefaultEncoding("utf-8");
	TemplateLoader ctl = new ClassTemplateLoader(TemplateLoaderTest.class,
			"/");
	TemplateLoader ftl1 = new FileTemplateLoader(new File(
			System.getProperty("user.dir")));
	MultiTemplateLoader mtl = new MultiTemplateLoader(new TemplateLoader[] {
			ftl1,ctl });
	configuration.setTemplateLoader(mtl);
	//configuration.getTemplate("test.ftl").process(data, out);
}

```
## 其它

### 缓存
模板加载通常是耗费资源的，默认是开启缓存的，缓存的实现，是否使用缓存取决于你

```java
configuration.setCacheStorage(new freemarker.cache.NullCacheStorage());

configuration.clearTemplateCache();
```
