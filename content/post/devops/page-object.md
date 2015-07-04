+++
categories = ["devops"]
date = "2015-01-29T22:26:00+08:00"
description = ""
keywords = []
title = "Page Object Pattern"

+++

移动UI自动化，看起来美好，践行起来却难。做个目光短见的务实主义者。Page Objects Pattern是Selenium官方推崇的方式，最近研究写测试用例最佳实践之Page Objects，同时结合Appium的Java Client简单介绍下如何写出靠谱的Page Object。

## Page Objects

Page Object定义为抽象web app页面的一系列对象，通过对页面功能的封装，它得到了很多好处：

* 减少重复代码
* 提高测试代码的可读性和稳定性
* 测试代码易于维护

## 一个简单的例子

```java
public class BaiduSearchPage {

	protected WebDriver driver;
        @FindBy(id="kw")
	private WebElement kw;
	private WebElement su;

	public BaiduSearchPage(WebDriver driver) {
		super();
		this.driver = driver;
                PageFactory.initElements(driver, this);
	}

	public void load(String url) {
		driver.get(url);
	}

	public ResultPage search(String key) {
		kw.clear();
		kw.sendKeys(key);
		su.click();
		return new ResultPage(driver);
	}
}
```
## 推荐的做法

* public 方法暴露Page对象的服务
* WebElement,Driver相关页面UI细节尽可能隐藏
* 尽量减少Page对象中的Assertion
* 到达新的Page，在方法中返回其它Page,甚至同一页面也可以返回Page做链式操作
* 一个Page对象不需要关注所有细节，只关心需要的对象，需要时再补充
* 不同的结果，同一个操作可以用不同的方法。

## Appium 中使用Page Object Pattern

Appium的Java Client是基于WebDriver的，但有了一些改进。比如元素定位不到，Appium Java Client会将Locator详细信息抛出，而Selenium没有。

## Wait

移动自动化测试Wait是很关键的一个动作，既关乎正确性，也关乎效率，我们应该极力避免使用Thread.sleep()或Sleeper.sleepTight()。Appium的客户端提供了一个类AppiumFieldDecorator可以很方便的设置ImplicitlyWaitTimeOut。FieldDecorator顾名思义，是Page对象Field的Decorator，PageFactory主要就是在Feild上下功夫，将WebElement类型的Feild使用Proxy方法，创建一个增强的WebElement,这个成员在每次操作时，都会先使用注解的定位策略定位，然后再调用WebElement的方法，当然可以通过CacheLookup注解，来缓存定位结果（尽量不这么做)。

```java
PageFactory.initElements(new AppiumFieldDecorator(driver, 5, TimeUnit.SECONDS), pageObject);
```

如果等待某个页面元素是否可见，在PageObject中也更简单

```java
public static void untilElementVisable(final WebElement element,int timeoutInSeconds){
  new Wait() {
     @Override
     public boolean until() {
	return element.isDisplayed();
     }
   }.wait(String.format("Timed out waiting for %s. Waited %s",
		  element, timeoutInSeconds), timeoutInSeconds);
}

```

## FindBy

在Appium中你会遇到，Selendroid模式和UIAutomator定位差异，比如Selendroid的linkText在UIAutomator中用name,还有就是iOS脚本想和Android共用一份。这在Appium中有了很好的扩充，Appium客户端会在运行时决定使用哪个Annotation来装饰WebElement。

```java
    @FindBy(name="text")
    @SelendroidFindBy(name = "text1")
    @iOSFindBy(id="sth")
    private WebElement textSelendroid;
```

## ElementInterceptor

总是有这样或那样的原因，需要记录日志，如果方法的执行每一步都要手写是很痛苦的，自然我们想到了AOP。在Selenium中EventFiringWebDriver类可以方便的记录日志，但是在Appium客户端中，我们可以修改AppiumFieldDecorator中ElementInterceptor来加入自己的日志信息，不过暂时这个功能Appium Client没有暴露出来，需要自己fork个repo修改下。

## 参考

http://assertselenium.com/automation-design-practices/page-object-pattern/
https://code.google.com/p/selenium/wiki/LoadableComponent
https://code.google.com/p/selenium/wiki/PageObjects
https://code.google.com/p/selenium/wiki/PageFactory
https://github.com/FluentLenium/FluentLenium
https://github.com/countableSet/webdriver-demo
