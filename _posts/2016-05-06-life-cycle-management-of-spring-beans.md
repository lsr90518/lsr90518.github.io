---
layout: post
title:  "Spring Bean的生命周期（译）"
date:   2016-05-06 08:31:19 +0900
tags: [review]
---

原文地址:[Life Cycle Management of a Spring Bean][origin-link]

### 1) 前言

这篇文章将会简洁地说明一下，一个Spring Bean在Spring的IOC(Inversion of Control)容器中是怎么被管理的。一个Spring Bean只要他被Application需要，他就会被放入在容器中。各种各样的生命周期接口(ife-cycle interfaces)和方法都将会被IOC容器调用。读这篇文章的前提条件，是最好先看一下[Introduction to Spring Web Framework][prerequisite-link]。

也同样可以阅读一下以下4篇文章

1. [Introduction to Spring Framework][also-read-1-link]
2. [Spring Tutorials][also-read-2-link]
3. [Spring Framework Books (recommended)][also-read-3-link]
4. [Book Review : Spring in Action][also-read-4-link]

### 2) Bean的生命周期

一个Spring Bean代表一个带有有用操作的POJO组件，

[origin-link]:http://www.javabeat.net/life-cycle-management-of-a-spring-bean/
[prerequisite-link]:http://www.javabeat.net/introduction-to-spring-mvc-web-framework-web-tier/
[also-read-1-link]:http://www.javabeat.net/introduction-to-spring-mvc-web-framework-web-tier/
[also-read-2-link]:http://www.javabeat.net/spring-tutorials/
[also-read-3-link]:http://www.javabeat.net/spring-framework-books/
[also-read-4-link]:http://www.javabeat.net/book-review-spring-in-action/
