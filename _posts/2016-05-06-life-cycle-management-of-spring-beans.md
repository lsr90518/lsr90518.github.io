---
layout: post
title:  "Spring Bean的生命周期"
date:   2016-05-06 08:31:19 +0900
tags: [review]
---

参考地址:

* [Life Cycle Management of a Spring Bean][origin-link]
* [Implementing BeanNameAware][implementing-beanNameAware-link]

## 1) 前言

这篇文章将会简洁地说明一下，一个Spring Bean在Spring的IOC(Inversion of Control)容器中是怎么被管理的。一个Spring Bean只要他被Application需要，他就会被放入在容器中。各种各样的生命周期接口(ife-cycle interfaces)和方法都将会被IOC容器调用。读这篇文章的前提条件，是最好先看一下[Introduction to Spring Web Framework][prerequisite-link]。

也同样可以阅读一下以下4篇文章

1. [Introduction to Spring Framework][also-read-1-link]
2. [Spring Tutorials][also-read-2-link]
3. [Spring Framework Books (recommended)][also-read-3-link]
4. [Book Review : Spring in Action][also-read-4-link]

## 2) Bean的生命周期

一个Spring Bean代表一个带有有用操作的POJO组件，所有的Spring Beans都存在于Spring容器中，也就是所谓的IOC容器(IOC Container)。Spring Framework是透明的，也因此隐藏了大部分复杂的结构与Spring容器与Spring Bean之间的通信。这一节列举出了发生在Bean开始实例化到交给Application之间发生的行为的序列。

![Spring Bean的生命周期](/public/img/spring-bean-life-cycle.png "生命周期")

1. Bean容器在配置文件中找到Bean的定义。
2. Bean容器创建一个使用Java反射API(Java Reflection API)创建一个实例。
3. 如果某一个属性被提及到，被提及到的属性也会被创建。如果被提到的属性是一个Bean的话，容器会生成并且set。
4. 如果Bean类实现了`BeanNameAware`接口，那么在传递Bean名字的时候，`setBeanName()`方法将会被调用。
5. 如果Bean类实现了`BeanClassLoaderAware`接口的话，那么在加载时传递实例的时候，将会调用`setBeanClassLoader()`方法。
6. 如果Bean类实现了`BeanFactoryAware`接口的话，那么在传递`BeanFactory`的时候`setBeanFactory()`就会被调用。
7. 如果任何一个`BeanPostProcessors`被加载过Bean的`BeanFactory`所生成的话，`postProcessBeforeInitialization()`将会被在Bean的属性被set之前调用。
8. 如果Bean类实现了`InitializingBean`接口的话，一旦所有配置文件中的Bean属性都被set之后，`afterPropertiesSet()`将会被调用。
9. 如果在配置文件时，Bean定义中包含`init-method`属性的话，那么这个属性的值就会被赋予该方法的方法名，然后被调用。
10. 如果有任何一个`Bean Post Processors`被创建的话，`postProcessAfterInitialization()`都将会被调用。
11. 如果Bean类实现了`DisposableBean`接口的话，那么在Application不再需要参照bean的时候，`destory()`方法就会被调用。
12. 如果在配置文件时，Bean定义中包含`destory-method`属性的话，那么Bean里定义的相应的方法就会被调用。

## 3) 生命周期的各个阶段

### 3.1) Bean Name Aware Interface

如果Bean的实现类想知道Bean的名字并且想被Bean Factory管理的话，Bea应该实现`BeanNameAware`接口，并且重写`setBeanName()`方法。这样的话，Bean Factory在读取了Bean的定义之后，也会知道Bean的名字，然后把Bean的名字作为参数传入`setBeanName()`方法之中。

* [BookReview:Spring in Action][also-read-4-link]

NameBean.java

~~~java
import org.springframework.beans.factory.BeanNameAware;
import org.springframework.stereotype.Component;

@Component
public class NameBean implements BeanNameAware {
  @Override
  public void setBeanName(String s) {
    System.out.println("Hello, my bean name is -" + s);
  }
}
~~~

### 3.2) BeanClassLoaderAware Interface

TestBeanWithClassLoaderAware.java

~~~java
import org.springframework.beans.factory.BeanClassLoaderAware;

public class TestBeanWithClassLoaderAware implements BeanClassLoaderAware
{
  private ClassLoader classLoader;

  @Override
  public void setBeanClassLoader(ClassLoader classLoader)
  {
    this.classLoader = classLoader;
  }

  public ClassLoader getBeanClassLoader()
  {
    return classLoader;
  }
}
~~~

每一次，客户端Application可以通过被加载的Bean来获得Class Loader的内容。在上面的例子中，TestBeanWithClassLoaderAware类实现了`BeanClassLoaderAware`并且重写了`setBeanClassLoader()`方法。这样的话Bean Factory就会传递一个`ClassLoader`对象，作为参数到`setBeanClassLoader()`方法中去。

[origin-link]:http://www.javabeat.net/life-cycle-management-of-a-spring-bean/
[prerequisite-link]:http://www.javabeat.net/introduction-to-spring-mvc-web-framework-web-tier/
[also-read-1-link]:http://www.javabeat.net/introduction-to-spring-mvc-web-framework-web-tier/
[also-read-2-link]:http://www.javabeat.net/spring-tutorials/
[also-read-3-link]:http://www.javabeat.net/spring-framework-books/
[also-read-4-link]:http://www.javabeat.net/book-review-spring-in-action/
[implementing-beanNameAware-link]:https://springframework.guru/spring-beannameaware-interface/
