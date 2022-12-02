---
title: 部分开发规范
time: 2022-11-28
update: 2022-11-28
---

# 开发规范

> 2022-11-29
>
> [知乎相关链接](https://zhuanlan.zhihu.com/p/182553920)
>
> [掘金相关链接](https://juejin.cn/post/6844903972206018567)

## `git commit`规范

`commit message`格式

```shell
<type>(<scope>): <subject>
```

### \<type>修改类型 ( must )

- feat | 新功能
- fix/to | 修正BUG
- docs | 文档
- style | 样式，不影响代码运行

- refacto | 重构（即不是新增功能，也不是修改bug的代码变动）

- perf | 优化相关，比如提升性能、体验

- test | 增加测试

- chore | 构建过程或辅助工具的变动

- revert | 回滚到上一个版本

- merge | 代码合并

- sync | 同步主线或分支的Bug

### \<scope>影响范围 ( option )

如数据层、控制层、视图层等等，当涉及到不止一部分时用 ***** 。

但现阶段暂时用不上，可以暂时用 ***** 代替。

### \<subject>描述 ( option )

不超过50个字符，结尾不需要加标点符号。

## HTML规范

### 标签

- 自闭合标签无需闭合
- 可选闭合标签要闭合
- 减少标签数量，不要有冗余标签

### class 与 id

- class 应以功能或内容命名，不以表现形式命名
- 字母小写，多个单词组成时，采用中划线-分隔
- 使用唯一的 id 作为 Javascript hook, 同时避免创建无样式信息的 class

### 属性顺序

- id
- class
- name
- data-xxx
- src, for, type, href
- title, alt
- aria-xxx, role

### 嵌套约束

#### 严格嵌套约束

无论何时都不会被允许。

- inline-Level 元素，仅可以包含文本或其它 inline-Level 元素;
- \<a>里不可以嵌套交互式元素\<a>、\<button>、\<select>等;（经chrome测试\<a>包含\<button>可以正常运行）
- \<p>里不可以嵌套块级元素\<div>、\<h1>~\<h6>、\<p>、\<ul>、\<ol>、\<li>、\<dl>、\<dt>、\<dd>、\<form>

#### 语义嵌套约束

浏览器会容错处理，但生成的文档树可能会不一样

- \<li> 用于 \<ul> 或 \<ol> 下
- \<dd>, \<dt> 用于 \<dl> 下
- \<thead>, \<tbody>, \<tfoot>, \<tr>, \<td> 用于 \<table> 下

### 文本规范

- 使用 HTML5 doctype，不区分大小写。

```xml
<!DOCTYPE html>
复制代码
```

- 声明文档使用的字符编码

```ini
<meta charset="utf-8">
复制代码
```

- 优先使用 IE 最新版本和 Chrome

```ini
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
```

### 样式表、JS加载

css 样式表在head标签内引用，js 脚本引用在 body 结束标签之前引用

## CSS 规范

### 声明顺序

#### 属性顺序

```css
.declaration-order {
  /* Positioning定位 */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  /* Box-model盒子模型 */
  display: block;
  float: right;
  width: 100px;
  height: 100px;

  /* Typography排版 */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;

  /* Visual视觉效果 */
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  /* Misc杂项 */
  opacity: 1;
}
```

#### 链表顺序

```css
a:link -> a:visited -> a:hover -> a:active（LoVeHAte）
```

### 命名

#### 缩写规范

要保持原意，且约定俗成的优先

```css
navigation   =>  nav 
header       =>  hd
description  =>  desc
```

#### 前缀规范

| 前缀 | 说明                                                         | 示例        |
| ---- | ------------------------------------------------------------ | ----------- |
| g-   | 全局通用样式命名，前缀g全称为global，一旦修改将影响全站样式  | g-mod       |
| m-   | 模块命名方式                                                 | m-detail    |
| ui-  | 组件命名方式                                                 | ui-selector |
| js-  | 所有用于纯交互的命名，不涉及任何样式规则。JSer拥有全部定义权限 | js-switch   |

### 缩写

- 属性值要缩写

  ```css
  // recommend
  margin: 1rem 3rem;
  
  // unrecommend
  margin-top: 1rem;
  margin-bottom: 1rem;
  margin-left: 3rem;
  margin-right: 3rem;
  ```

- **0**的省略

  ```css
  // recommend
  margin: 0;
  paddingL: .8rem;
  
  // unrecommend
  margin: 0rem;
  paddingL: 0.8rem;
  ```

- 省略**url()**外的引号

  ```css
  // recommend
  @import url(//www.google.com/css/go.css); 
  ```

## 特别注意

- 减少高消耗样式的使用

  ```css
  box-shadows
  border-radius
  transparency
  transforms
  CSS filters（性能杀手）
  ```

- 正确使用css

  ```css
  display: inline后不应该再使用 width、height、margin、padding 以及 float；
  display: inline-block 后不应该再使用 float；
  display: block 后不应该再使用 vertical-align；
  display: table-* 后不应该再使用 margin 或者 float；
  ```

  