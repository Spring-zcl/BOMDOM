### 创建、插入和删除元素
---
1. #### 创建DOM元素
    - **createElement(标签名)** -------------------创建一个节点
    - **appendChild(节点)** -----------------------追加一个节点
2. #### 插入元素
    - **insertBefore(节点, 原有节点)** ------------在已有元素前插入
3. #### 删除DOM元素
    - **removeChild(节点)** -----------------------删除一个节点
4. #### 文档碎片
    - 文档碎片可以提高DOM操作性能（理论上）
    - **document.createDocumentFragment()**
---
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
