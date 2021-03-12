---
title: 抽象方法
tags: 设计模式
abbrlink: 1332211608
date: 2020-08-22 21:02:04
categories: 
  - 设计模式
  - 创建型模式
---


##### 概述

> ​提供一个创建一系列相关或相互依赖对象的接口，而无需指定它们具体的类。

<!-- more -->

##### 适用性

1. 一个系统要独立于它的产品的创建、组合喝表示时
2. 一个系统要由多个产品系列中的一个来配置时
3. 当你要强调一系列相关的产品对象的设计以便进行联合使用时
4. 当你提供一个产品类库，而只想显示它们的接口而不是实现时

##### 参与者

1. AbstractFactory 声明一个创建抽象产品对象的操作接口
2. ConcreateFactory 实现创建具体产品对象的操作
3. AbstractProduct 为一类产品对象声明一个接口
4. ConcreateProduct 定义一个将被相应的具体工厂创建的产品对象。实现AbstraceProduct接口
5. ClientTest 仅使用由AbstractFactory和AbstractProduct类声明的接口

##### 类图

![](http://book.codedq.net/design-pattern/img/AbstractFactory.jpg)
