---
layout:     post
title:      Vue 表格自适应高度
subtitle:   为 el-table 添加自适应高度指令
date:       2020-05-11
author:     SuperZhouDalu
header-img: img/post-bg-universe.jpg
catalog: true
tags:                              
    - 前端
---

### 前言

> 示例版本为 Element-ui 2.13.1 + Vue 2.6.11

![demo.gif](http://ww1.sinaimg.cn/large/005yqb1Zly1geokm94qxtg31hc0t4qqz.gif)

本人是做后台开发的，由于公司业务要求需要将前后台模块进行分离，两年前选择使用 [vue-element-admin](https://github.com/PanJiaChen/vue-element-admin) 项目进行前台的开发，该框架集成了很多功能，特别适合对 Vue 很陌生的新手，公司项目组成员接受程度普遍较高。

在使用过程中 **表格** 是必不可少的一个控件，用于展示数据，单页数据量过多就会导致浏览器自动生成右侧滚动条。

![demo1.png](http://ww1.sinaimg.cn/large/005yqb1Zly1geok2ppdovj31hb0pudij.jpg)

如果页面有头部信息或查询按钮，移动滚动条后会遮挡住这些操作和信息内容。

![demo2.png](http://ww1.sinaimg.cn/large/005yqb1Zly1geok3qxzt5j31h90q2gob.jpg)

Element-UI 中的 el-table 提供了设置高度的选项，在代码中设置 height 属性就可以现在表格的高度，数据量过多也只会在表格内部生成滚动条，而不是整个页面生成滚动条。

![demo3.png](http://ww1.sinaimg.cn/large/005yqb1Zly1geok5sq3glj31ha0pz40y.jpg)

但是这个高度需要固定的数值，不同的分辨率或者缩放后的浏览器使用固定高度后，不能满足只在 el-table 内部生成滚动条的条件。

![demo4.png](http://ww1.sinaimg.cn/large/005yqb1Zly1geok76w3pcj31h50kztau.jpg)

想要满足上述条件就需要使用 `v-adaptive` 指令了。

### Vue 自定义指令

你可能会好奇 `v-adaptive`  是在哪里来的？它是自定义的指令，设置表格高度需要对普通 DOM 元素进行底层操作。Vue 除了核心功能默认内置的指令 (`v-model` 和 `v-show`)，也允许注册自定义指令，相关 Api 可以查看 [官方文档](https://cn.vuejs.org/v2/guide/custom-directive.html) 。

### v-adaptive

新建包名`src/directive/el-table`，创建 `adaptive.js` 。页面缩放的监听是使用的 `element-ui` 中的 `resize-event`，将 `addResizeListener`  和 `removeResizeListener`  引入进来。自定义指令要用到的钩子函数：

* `bind`：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。
* `inserted`：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)。
* `unbind`：只调用一次，指令与元素解绑时调用。

```
import { addResizeListener, removeResizeListener } from 'element-ui/src/utils/resize-event'

 // 设置表格高度
 const doResize = async(el, binding, vnode) => {
 // 获取表格Dom对象
 const { componentInstance: $table } = await vnode
 // 获取调用传递过来的数据 
 const { value } = binding

  if (!$table.height) {
    throw new Error(`el-$table must set the height. Such as height='100px'`)
  }
  // 获取距底部距离（用于展示页码等信息）
  const bottomOffset = (value && value.bottomOffset) || 30

  if (!$table) return

  // 计算列表高度并设置
  const height = window.innerHeight - el.getBoundingClientRect().top - bottomOffset
  $table.layout.setHeight(height)
  $table.doLayout()
}

export default {  
    // 初始化设置
    bind(el, binding, vnode) { 
        // 设置resize监听方法
        el.resizeListener = async() => { 
            await doResize(el, binding, vnode)
        }    
        // 绑定监听方法到addResizeListener
        addResizeListener(window.document.body, el.resizeListener)  
    },  
    // 绑定默认高度
    async inserted(el, binding, vnode) { 
        await doResize(el, binding, vnode)  
    },  
    // 销毁时设置
    unbind(el) { 
        // 移除resize监听
        removeResizeListener(el, el.resizeListener)  
    }
}
```

接下来，需要将写好的逻辑绑定到 Vue 中，在同一目录下新建 `index.js`：

```
import adaptive from './adaptive'

const install = function(Vue) {     
    // 绑定v-adaptive指令
    Vue.directive('adaptive', adaptive)
}

if (window.Vue) {
    window['adaptive'] = adaptive  
    // eslint-disable-next-line no-undef 
    Vue.use(install)
}

adaptive.install = install

export default adaptive
```

### 在单页面使用

指令相关代码已经写好了，接下来就是该如何使用了。找到想要设置表格自适应高度的 vue 文件，在 `script` 标签下引入自定义的指令并绑定。

```
import adaptive from '@/directive/el-table'
export default {  
    name：‘Test’
    directives: { adaptive }，
    ... ...
}
```
然后找到表格所在的标签添加指令相关的代码：
```
<el-table  
    ref="table"
    // 自定义指令，bottomOffset 代表距离底部的距离
    v-adaptive="{bottomOffset: 85}"
    // 高度属性，100无具体意义，仅为初始值，不可省略
    height="100px" 
 >
 ... ...
 </table>
```
### 全局使用

如果存在多个页面需要设置自适应高度，为了减少使用指令的复杂度，我们可以在 `main.js` 中全局引入自定义的指令，上述 `script`的内容就不需要在每个页面进行写入了。

```
import adaptive from './directive/el-table'

Vue.use(adaptive)
```

### 结尾

源码放在 [GitHub](https://github.com/superZhouDaLu/BlogExample/tree/master/Vue_Adaptive_Table) 上了，希望可以帮助到你。
