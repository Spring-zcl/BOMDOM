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
### 4. 添加节点
```
// 将一个节点添加到指点父节点的子节点列表末尾

node.appendChild(child)

// 将一个节点添加到父节点的指定子节点前面

node.insertBefore(child, 指定元素)
```
### 5. 删除节点
```
// 从父节点中删除一个子节点，返回删除的节点

node.removeChild(child)
```
### 6. 阻止连接跳转
```
<a herf='javascript:;'/>
<a herf='javascript:void(0);'/>
```
### 7. 复制节点（克隆节点）
```
// 返回调用该方法的节点的一个副本
// 括号里的可选择默认为false，是浅拷贝，只克隆节点本身，不包括节点里面的子节点，为true则相反

node.cloneNode()
```
### 8. 三种动态创建元素区别
```
document.write()
element.innerHTML
document.createElement()
```
#### 区别
1. docuemnt.write是直接将内容写入页面的内容流，但是文档流执行完毕，会导致页面全部重绘
2. innerHTML是将内容写入某个DOM节点，不会导致页面全部重绘
3. innerHTML创建多个元素效率更高（不要拼接字符串，采取数组形式拼接），结构稍微复杂
4. createElement（）创建多个元素效率稍微低一些，但是结构更清晰
## 事件
### 1. addEventListener事件监听
```
eventTarget.addEventListener(type, listener[, useCapture])

// type: 事件类型字符串，如click， mouseover
// listener: 事件处理函数，事件发生时，会调用该监听函数
// useCapture: 可选参数，默认false,为false时表示在事件冒泡阶段调用事件处理程序，为true时表示在事件捕获阶段调用事件处理程序
```
### 2. 删除事件
```
// 方式一
element.onclick = function() {
    alert(1)
    element.onclick = null
}

// 方式二
element.addEventListener('click', fn)
function fn() {
    alert(1)
    element.removeEventListener('click', fn)
}
```
### 3. 禁用右键菜单和禁止选中文字
```
// 禁用右键菜单
document.addEventListener('contextmenu', function(e){
    e.preventDefault()
})

// 禁止选中文字
document.addEventListener('selectstart', function(e){
    e.preventDefault()
})
```
### 4. 鼠标事件对象
|鼠标事件对象|说明|
|---|---|
|e.clientX|鼠标相对于浏览器窗口可视区的X坐标|
|e.clientY|鼠标相对于浏览器窗口可视区的Y坐标|
|e.pageX|鼠标相对于文档页面的X坐标|
|e.pageY|鼠标相对于文档页面的Y坐标|
|e.screenX|鼠标相对于电脑屏幕的X坐标|
|e.screenY|鼠标相对于电脑屏幕的Y坐标|
### 5. 常用键盘事件
|键盘事件|触发条件|
|---|---|
|onkeydown|某个键盘按键被按下时触发|
|onkeypress|某个键盘按键被按下时触发 但是它不能识别功能键 如Ctrl shitf 左右箭头|
|onkeyup|某个键盘按键被松开时触发|
### 6. 键盘事件对象
|键盘事件对象属性|说明|
|---|---|
|keyCode|返回该键的ASCII值|
#### 注意： 
onkeydown 和 onkeyup不区分字母大小写，onkeypress区分大小写
## 窗口加载事件
```
document.addEventListener('DOMContentLoaded',function(){})
// DOMContentLoaded事件出发时，仅当DOM加载完成，不包括样式表，图片，flash等等
```
## 调整窗口大小事件
```
window.onresize = function() {}
window.addEventListener('resize', function() {})

// window.onresize 是调整窗口大小加载事件，当触发时就调用的处理函数
// 注意：
// 1. 只要窗口大小发生像素变化，就会触发这个事件
// 2. window.innerWidth当前屏幕的宽度
```
## 定时器
### 1. setTimeout()定时器
```
window.setTimeout(调用函数，[延迟的毫秒数])

// setTimeout()方法用于设置一个定时器，该定时器在时间到期后执行调用函数
// 注意：
// 1. window可以省略
// 2. 这个调用函数可以直接写函数，或者写函数名或者采取字符串'函数名（）'三种方式
// 3. 延迟的毫秒数默认为0，单位是毫秒
// 4. 有多个定时器，可以给定时器赋值一个标识符
```
### 2. clearTimeout()清除定时器
```
window.clearTimeout(timeoutID)

// 参数timeoutID就是定时器标识符
```
### 3. setInterval()定时器
```
window.setInterval(回调函数，[间隔的毫秒数])

// setInterval()方法每隔间隔时间反复调用函数
// 注意：
// 1. window可以省略
// 2. 这个调用函数可以直接写函数，或者写函数名或者采取字符串'函数名（）'三种方式
// 3. 延迟的毫秒数默认为0，单位是毫秒
// 4. 有多个定时器，可以给定时器赋值一个标识符
```
### 4. clearInterval()清除定时器
```
window.clearInterval(intervalID)
// 参数intervalID就是定时器标识符
```
## location对象
### 1.URL
统一资源定位符（Uniform Resource Locator,URL）是互联网上标准资源的地址。互联网上的每个文件都会有一个唯一的URL，它包含的信息指出文件的位置以及浏览器应该怎么处理它。
URL的一版语法格式为：
    protocol://host[:port]/path/[?query]#fragment
|组成|说明|
|---|---|
|protocol|通信协议如http,ftp,maito等|
|host|主机（域名）|
|port|端口号可选|
|path|路径由零个或多个‘/’符号隔开的字符串，一般用来表示主机上的一个目录或文件地址|
|query|参数以键值对的形式，通过‘&’符号分隔|
|fragment|片段#后面的内容常见于链接锚点|
### 2.location对象的属性
|location对象属性|返回值|
|---|---|
|location.href|获取或者设置整个URL|
|location.host|返回主机（域名）|
|location.port|返回端口号|
|location.pathname|返回路径|
|location.search|返回参数|
|location.hash|返回片段#后面的内容常见于链接锚点|
### 3.location对象的方法
|location对象方法|返回值|
|---|---|
|location.assign()|跟href一样，可以跳转页面，可以返回上个页面|
|location.replace()|替换当前页面，因为不记录历史，所以不能后退页面|
|location.reload()|重新加载页面，相当于刷新按钮或者f5，如果参数为true强制刷新Ctrl+f5|
## history对象
|history对象方法|作用|
|---|---|
|back()|后退功能|
|forward()|前进功能|
|go()|前进后退功能参数如果是1前进一个页面如果是-1后退一个页面|
## 1. 元素偏移量offset系列
### 1. offset概述
 - 获得元素距离带有定位父元素的位置
 - 获得元素自身的大小（宽度高度）
 - 注意：返回的数值都不带单位
### 2. offset系列属性
|offset系列属性|作用|
|---|---|
|element.offsetParent|返回作为改元素带有定位的父级元素,如果父级元素没有定位则返回body|
|element.offsetTop|返回元素相对带有定位父元素上方的偏移|
|element.offsetLeft|返回元素相对带有定位父元素左边框的偏移|
|element.offsetWidth|返回自身包括padding、边框、内容区的宽度，返回数值不带单位|
|element.offsetHeight|返回自身包括padding、边框、内容区的高度，返回数值不带单位|
### 3. offset与style区别
|offset|style|
|---|---|
|offset可以得到任意样式表中的样式值|style只能得到行内样式表中的样式值|
|offset系列获得的数值是没有单位的|style.width获得的是带有单位的字符串|
|offsetWidth包含padding+border+width|style.width获得的不包含padding和border的值|
|offsetWidth等属性是只读属性，只能获取不能赋值|style.wisth是可读属性，可以获取也可以赋值|
|获取元素大小位置，用offset更合适|更改元素属性用style|
## 2. 元素可视区client系列
|client系列属性|作用|
|---|---|
|element.clientTop|返回元素上边框的大小|
|element.clientLeft|返回元素左边框的大小|
|element.clientWidth|返回自身包括padding、内容区的宽度，不含边框，返回的数值不带单位|
|element.clientHeight|返回自身包括padding、内容区的高度，不含边框，返回数值不带单位|
## 立即执行函数
```
(function(){}())
(function(){})()
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
