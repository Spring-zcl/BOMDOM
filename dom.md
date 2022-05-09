## 获取DOM元素
1. 
```javascript
document.getElementById()
document.getElementsByTagName()
```
2. #### H5新增获取方法
```javascript
document.getElementsByClassName()
// 返回指定选择器的第一个元素对象，选择器需加符号
document.querySelector()
// 返回指定选择器的所有元素对象集合
document.querySelectorAll()
```
3. #### 获取body元素
```javascript
document.body
```
5. #### 获取html元素
```javascript
document.documentElement
```
## 事件
### 事件执行步骤
1. 获取事件源
```javascript
var ele = document.querySelector('div')
```
2. 绑定事件，注册事件
```javascript
ele.onclick
```
3. 添加事件处理程序
```javascript
ele.onclick = function() {}
```
### 常见鼠标事件
|鼠标事件|触发条件|
|---|---|
|onclick|鼠标点击左键触发|
|onmouseover|鼠标经过触发|
|onmouseout|鼠标离开触发|
|onfocus|获得鼠标焦点触发|
|onblur|失去鼠标焦点触发|
|onmousemove|鼠标移动触发|
|onmouseup|鼠标弹起触发|
|onmousedon|鼠标按下触发|
## 修改元素内容
1. innerText
```javaScript
// 去除HTML标签、空格、换行
element.innerText
```
2. innerHTML
```javaScript
// 包括HTML标签、空格、换行
element.innerHTML
```
## 样式属性修改
可以通过js修改元素的大小、颜色、位置等样式
1. element.style---------------行内样式操作
#### 注意
    1. js里面的样式采取驼峰命名法，比如 fontSize、backgroundColor
    2. js修改style样式操作，产生的是行内样式，css权重比较高
2. element.className-----------类名样式操作
#### 注意
    1. 如果样式修改较多，可以采取操作类名方式更改元素样式
    2. class因为是个保留字，因此使用className来操作元素类名属性
    3. className会直接更改元素的类名，会覆盖原先的类名
## 自定义属性的操作
### 获取属性值
    element.属性  获取内置属性值（元素本身自带的属性）
    element.getAttribute('属性')   可获取自定义的属性
### 设置属性值
    element.属性 = '值'  设置内置属性值
    element.setAttribute('属性','值')  可设置自定义的属性
### 移除属性
    element.removeAttribute('属性')
## 设置H5自定义属性
H5规定自定义属性‘data-’开头作为属性名并赋值
```
<div data-index='1'></div>
element.setAttribute('data-index',1)
```
获取H5自定义属性
1. element.getAttribute('data-index')
2. H5新增element.dataset.index 或者 element.dataset['index'] 
#### 注意：
1. dataset只能获取‘data-’开头的
2. dataset里面存放了所有‘data-’开头的自定义属性
3. 如果自定义属性里面有多个-连接的单词，获取的时候使用驼峰命名
    element.getAttribute('data-list-name')
    element.dataset['listName']
## 节点概述
1. 节点有nodeType（节点类型）、nodeName（节点名称）和nodeValue（节点值）三个属性
    - 元素节点nodeType为1
    - 属性节点nodeType为2
    - 文本节点nodeType为3（文本几点包含文字、空格、换行等）
## 节点层级
### 1. 父级节点
```
// parentNode属性返回某节点的最近一个父节点，如果指定的节点没有父节点则返回null

node.parentNode
```
### 2. 子节点
```
// 返回值里面包含了所有的子节点，包括元素节点，文本节点等

parentNode.childNodes // (标准)
```

```
// parentNode.children是个只读属性，返回所有的子元素节点。只返回子元素节点，其余节点不返回

parentNode.children // (非标准)
```

```
// 第一个子节点，不管是文本节点还是元素节点

element.firstChild

// 最后一个子节点，不管是文本节点还是元素节点

element.lastChild
```

```
// 第一个子元素节点

element.firstElementChild

最后一个子元素节点

element.lastElementChild
```

### 3. 兄弟节点
```
// 返回当前元素的下一个兄弟节点，找不到返回null,包含所有节点

node.nextSibling

// 返回当前元素的上一个兄弟节点，找不到返回null,包含所有节点

node.previousSibling
```

```
// 返回当前元素的下一个元素节点，找不到返回null

node.nextElementSibling

// 返回当前元素的上一个元素节点，找不到返回null

node.previousElementSibling
```
## 创建、插入和删除元素
1. #### 创建DOM元素
```javaScript
// 创建一个节点
createElement(标签名)
// 追加一个节点
appendChild(节点)
```
2. #### 插入元素
```javaScript
// 在已有元素前插入
insertBefore(节点, 原有节点)
```
3. #### 删除DOM元素
```javaScript
// 删除一个节点
removeChild(节点)
```
4. #### 文档碎片
    - 文档碎片可以提高DOM操作性能（理论上）
```javaScript
document.createDocumentFragment()
```
示例：
```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <script>
    window.onload = function () {
      var uls = document.getElementById('uls')
      var btn = document.getElementById('btn')
      btn.onclick = function () {
        var lis = document.createElement('li')
        var del = document.createElement('button')
        var text = document.getElementById('txt1')
        var oli = uls.getElementsByTagName('li')
        del.innerHTML = '删除'
        lis.innerHTML = text.value
        lis.appendChild(del)
        if (uls.children.length) {
          uls.insertBefore(lis, oli[0])
        } else {
          uls.appendChild(lis)
        }
        delEvent(uls)
      }
    }
    function delEvent(parent) {
      var btns = parent.getElementsByTagName('button')
      for (let i = 0; i < btns.length; i++) {
        btns[i].onclick = function () {
          parent.removeChild(this.parentNode)
        }
      }
    }
  </script>
</head>

<body>
  <input type="text" id="txt1">
  <input type="button" id="btn" value="add">
  <ul id="uls"></ul>
</body>

</html>
```
