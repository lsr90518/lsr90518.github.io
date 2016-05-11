---
layout: post
title:  "使用Token的CSRF防御策略"
date:   2016-05-06 08:31:19 +0900
tags: [tech]
---

## 1) CSRF本质

概要之类的文章，网上一搜一大把这里不再赘述。[CSRF是个啥？](https://www.google.com.hk/?gws_rd=ssl#q=csrf)

这里主要讨论一下CSRF的本质
: CSRF攻击就是攻击者**盗用**被害者的身份，发送违背被害者意愿的请求。

这里的关键词是**盗用**，所以只要我们防御了攻击者的盗用方法，那么受害者就会得到保护。

## 2) 防御策略

### 2.1) REFERER

### 2.2) TOKEN

### 2.3) 另外，最重要

## 3) 总结

* 明白了CSRF的本质之后，其实并不需要过多的在网上搜索很多的资料，因为在防御者看来，他们上网搜索资料是为了找出防御策略。然后攻击者也为了找出大家防御策略的漏洞，而上网搜索。所以根据自己项目的特点来进行设计，才是最重要的。
* 对于最终编码实现，也许你可以选择spring security，也可以直接使用servlet的filter来实现，甚至可以直接开发一个专门用于防御的微服务作为框架，其实对于框架的选择，首先基于自己的设计，然后找出最适合项目开发与提供功能最全的框架就好。切忌基于框架设计防御策略。


[why-refresh-csrf-token-per-form-request]:http://security.stackexchange.com/questions/22903/why-refresh-csrf-token-per-form-request
