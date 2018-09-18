---
title: angular开发问题汇总
date: 2018-04-27 17:36:16
tags: angular 前端
---

1. 在cli运行的情况下, 添加懒加载模块可能报错:
```
core.js:1448 ERROR Error: Uncaught (in promise): TypeError: undefined is not a function
TypeError: undefined is not a function
    at Array.map (<anonymous>)
    at webpackAsyncContext (eval at ./src/$$_lazy_route_resource lazy recursive (main.bundle.js:13), <anonymous>:19:34)
    at SystemJsNgModuleLoader.loadAndCompile (core.js:6558)
    at SystemJsNgModuleLoader.load (core.js:6542)
    at RouterConfigLoader.loadModuleFactory (router.js:4543)
    at RouterConfigLoader.load (router.js:4523)
    at MergeMapSubscriber.eval [as project] (router.js:2015)
    at MergeMapSubscriber._tryNext (mergeMap.js:128)
```
解决方案: 重新运行项目`npm start`

2. 通过第三方插件或方法异步改变组件变量的值时出现变量没有更新到模板

    <font color=red>问题根源</font>: </br>
    angular的检测机制是基于zone, 而第三方的异步调用运行在zone作用之外, 不会触发zone检测, 导致变量没有及时更新到模板

    <font color=red>解决方法: </font>
    1. 通过`ChangeDetectorRef.detectChanges()`手动进行变量检测;
    2. 通过`ngZone.run(() => {})`来将方法放在zone中进行.