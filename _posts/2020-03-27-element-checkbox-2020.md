---
layout:     post
title:      el-checkbox 多级联动
subtitle:   element-ui checkbox 组件的树形联动
date:       2020-03-27
author:     SuperZhouDalu
header-img: img/post-bg-universe.jpg
catalog: true
tags:                              
    - 前端
---

### 前言

> 示例版本为 Element-ui 2.13.0 + Vue 2.6.11

最近想弄 **Element-ui checkbox** 的多级联动，网上相关的例子大多数为二级联动，自己研究了一下，弄了一个树形菜单的多级联动，常用于角色管理等业务。（仅供参考，未考虑性能问题）

### 数据模型

```
[
    {
      "menu": { 
        "id":14, 
        "menuName":"测试管理',
         "parentId":0
      } ，
      "menuOptionsList":[
            {
                "id":46,
                "optionsName":"列表",
                "checked":false
            },
            {
                "id":47,
                "optionsName":"新增",
                "checked":false
            }
        ],        
        "children":[],
        "checked":false
    }
]
```

这里展示的最顶级的数据结构，下级数据只需要在 **children** 中添加即可。**需要注意的是 checked 属性，本身数据库表中没有这个数据，需要后台建立一个 VO 映射实体将 checked 字段添加进去，默认值为 false.**

### 逻辑处理

html 使用 el-table + el-chekbox 展示：

![](http://ww1.sinaimg.cn/large/005yqb1Zly1gd8g6sxn2ej30nl0i4t9f.jpg)

```
    <el-table
      :data="menuList"
      border
      fit
      size="mini"
      highlight-current-row
      row-key="menu.id"
      :default-expand-all="true"
      :tree-props="{children: 'children', hasChildren: 'hasChildren'}"
     >
       <el-table-column label="菜单名称" width="180">
         <template slot-scope="scope">
            <el-checkbox 
                v-model="scope.row.checked" 
                :indeterminate="scope.row.indeterminate" 
                @change="handleCheckAllChange(scope.row, $event)">
                {{ scope.row.menu.menuName }}
            </el-checkbox>
          </template>
        </el-table-column>
        <el-table-column label="功能选项">
          <template v-if="scope.row.children.length === 0" slot-scope="scope">
           <el-checkbox
             v-for="options in scope.row.menuOptionsList"
             :key="options.id"
             v-model="options.checked"
             :label="options.optionsName"
             @change="handleCheckChange(scope.row)"
           />
          </template>
       </el-table-column>
     </el-table>
```

核心方法 `handleCheckAllChange`  和 `handleCheckChange` 这两个方法，`handleCheckAllChange`  是 `菜单选项` 列按钮被点击的事件，`handleCheckChange` 是 `选项列表` 列被点击的事件。 

#### handleCheckAllChange（菜单列改变事件）

```
handleCheckAllChange(val, checked) {
      // 有下级去处理下级
      if (val.children.length > 0) {
        // 递归设置子级选中状态
        this.findChildren(val.children, checked)
      } else {
        // 无下级处理本级
        val.menuOptionsList.forEach(options => { options.checked = checked })
      }
      // 处理上级
      if (val.menu.parentId !== 0) {
        递归设置上级选中状态
        this.findParent(this.menuList, val.menu.parentId)
      }
      // 设置全选的未全部选中的状态
      val.indeterminate = false
}
```

根据数据中 **children** 的长度来判断是否存在下级，如果存在就执行递归方法 `findChildren` 将子类的 checked 属性设置为 true，不存在处理本级的 checked 属性即可。**需要注意的是 parentId 等于 0 证明当前菜单父级为顶级菜单，不需要再向上寻找。以此为判断依据来进行父级菜单的判断条件。** 如果 parentId 不等于 0 说明当前全选的菜单存在父级，需要将父级的选项框进行状态设置。

#### handleCheckChange（选项列改变事件）

```
handleCheckChange(val) {
      const length = val.menuOptionsList.length
      let checkedLength = 0
      val.menuOptionsList.forEach(options => {
        if (options.checked) {
          checkedLength++
        }
      })
      val.checked = checkedLength === length
      val.indeterminate = checkedLength > 0 && checkedLength < length
      // 处理上级
      if (val.menu.parentId !== 0) {
        this.findParent(this.menuList, val.menu.parentId)
      }
}
```
这个方法对应着 `选项列表` 列选中的状态，需要对 `菜单名称` 列的全选状态进行控制。首先通过变量 length 获取到当前数据行选项列表的数量，遍历选项数组根据 checked 的状态获取到已选中的选项数量。val.checked 代表当前列是否全选，val.indeterminate 代表当前列是否有选项被选中。但是这只是处理了当前行的状态，当前行可能是某一菜单的子集，所以需要由下向上的去寻找菜单的父级并设置选中状态。这里同样用到了上面方法中的 `findParent`  函数。

##### findChildren（递归查询子集）

```
findChildren(list, checked) {
  list.forEach(children => {
    children.checked = checked
    children.indeterminate = false
    children.menuOptionsList.forEach(options => {
      options.checked = checked
      if (children.children.length > 0) {
        this.findChildren(children.children, checked)
      }
    })
  })
}
```
##### findParent（递归查询父集）

```
findParent(list, parentId) {
  list.forEach(result => {
    let parentCheckedLength = 0
    let parentIndeterminateLength = 0
    if (result.menu.id === parentId) {
      result.children.forEach(children => {
        if (children.indeterminate) {
          parentIndeterminateLength++
        } else if (children.checked) {
          parentCheckedLength++
        }
      })
      result.checked = parentCheckedLength === result.children.length
      result.indeterminate = (parentIndeterminateLength > 0 || parentCheckedLength > 0) && parentCheckedLength < result.children.length
      if (result.menu.parentId !== 0) {
        this.findParent(this.menuList, result.menu.parentId)
      }
    } else if (result.children.length > 0) {
      this.findParent(result.children, parentId)
    }
  })
}
```

### 完整示例

由于源码篇幅过长，暂时将源码放到 [GitHub](
https://github.com/superZhouDaLu/BlogExample/blob/master/Element_CheckBox/demo.vue) 了，希望可以帮助到你。
