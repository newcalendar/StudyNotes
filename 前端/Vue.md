# Vue

## 概述

Vue是一套用于构建用户界面的渐进式框架，与其它框架不同，Vue被设计为可以自底向上逐层应用。Vue的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合

安装Vue

1、官网下载，标签引入

2、

```
cnpm install vue 
```

```
vue目录结构

build项目构建相关代码

config配置目录

node_modules npm加载的项目依赖模块

src 开发源码文件，里面一般包含asset\components\appvue\mainjs

static静态资源

test测试目录

index.html首页入口文件

package.json项目配置文件

README.md项目说明文档


```

## Vue语法

v-html，使用v-html指令用于输出HTML代码

v-bind指令

vue提供了完全的JavaScript表达式支持

v-on用于监听DOM事件

双向绑定

{{data}}，利用双大括号进行数据绑定

v-model也可以实现数据的双向绑定

v-if条件语句可配合v-else或v-else-if  