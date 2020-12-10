## 介绍

> zoe是一款用于构建Web Components的前端框架，它拥有和React一致的API

## Web Components

  随着前端的发展，各种框架层出不穷，让前端社区更加繁荣的同时也带了一些弊端，开发者正在被一个个框架所限制，各个框架之间如同孤岛，不同框架之前代码不能共享，导致组件无法跨框架复用，这与前端模块化发展是相违背的，而Web Components可以帮助我们解决这个问题。

  Web Components不是单一的技术，它是由一系列浏览器标准组成的，通过标准化非侵入的方式封装组件。
  
  做为浏览器所支持的标准，它可以突破前端框架的限制，开发具有更高通用性的web组件。

## 关于zoe
  Web Components作为基础API，在渲染及更新时都需要手动操作Dom，过程繁琐且容易出错，并且它的强隔离性导致组件之间样式无法复用。

  zoe基于JXS语法开发Web Components，并且保持和React一致的API，这样我们可以像写React组件一样来开发Web Components。
  
  zoe可以突破Web Components之间的边界，实现样式共享。

## 特性

- JSX语法开发Web Components
- 保持了和React一致的API
- 支持Hooks语法
- 支持局部/全局样式共享
- 轻量的体积 (7kb gzip)
- 高性能

## 兼容性：
  - ios9+
  - android4.4+
  - ie11+
