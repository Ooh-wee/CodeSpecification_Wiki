## 代码标准

### 项目结构解耦

以下项目名仅做示例理解，名字可以改

```
|----- pro
   |----- index(page)
      |----- component
         |----- header
         |----- body
         |----- footer
         ...
      |----- webapi.js (组件ajax)
      |----- index.js (主文件)
      |----- eFun.js (所有的事件方法)
      |----- public  
         |----- css
            |-----  animation.css
         |----- iamges
         |----- js
            |----- animation.js
            |----- anyOther.js
         ...
   |----- utils
      |----- eAlerts.js
   |----- public
      |----- css
         |----- public.css
      |----- images   
   ... balabala         
```

### 代码解耦

```
1. ajax 独立
2. 弹窗代码独立
3. e 事件独立
4. 公共样式独立
5. 动画样式独立
6. 组件样式独立
所有的代码能复用就复用
```

### 代码风格写法建议

1. 避免无默认值导致的报错，函数参数尽量使用以下写法

例如：

```
let httpServer = ({data, port} = {data : {test: 'Hello World !'}, port : 3000}) => { 
    let http = require('http');
    http.createServer((req, res) => {
      res.writeHead(200, {'Content-type': 'text/plain'});
      res.end(`${JSON.stringify(data)}`)
    }).listen((port), (err) => {
      if(!err){
          console.log(`Server start on port ${port}`);
      } else {
          throw `500 ---> ${err}`
      }
    });
}
```

### 函数尽量模块属性化

模块函数定义：

```
export let aFun = () => {}
export let bFun = () => {}
```

模块函数调用

```
import {aFun, bFun} = './fun.js'
```

### 理清生命周期

生命周期紊乱，可以参考vue或者react的生命周期示例：

1. 所有的打卡、埋点放到beforeCreate中

```
beforeCreate = () => {

}
```

2. window.onload dom加载之后的所有事件放在created中

```
created = () => {

}

```

### ajax调用

使用 promise + async + await
 
```
async() => {
    let resData = await ajaxFun();
}
```

### ```取代双引号

便于参数传递，
允许换行，代码整洁

```
let a = `
   Hello 
   ${window.state.name}!
   `;
```

### 尽量写原生

1. 原因

项目代码中常用到JQ/Zt的地方就是：

```
$(dom),
attr,
css,
```

使用场景不大，完全不用浪费一个import，
有利于提高代码构建能力

替代方案：

#### 获取dom 

仅作参考

```
let $ = (dom) => {
  let getDoms = document.querySelectAll(dom);
  switch(getDoms.length){
     case:
     return getDoms[0];
     default:
     return getDoms;
  }
}
```

#### attr

```
$(dom).getAttribute('name');
$(dom).setAttribute('name', 'test');
```

#### style

```
let color = `red`;
let style_ = `
  width: 100px;
  height: 100px;
  background: ${color};
`
$(dom).setAttribute('style', style_);
```

### use strict

可以不用lint，但是务必使用strict模式

### 用switch代替if

switch比if快



