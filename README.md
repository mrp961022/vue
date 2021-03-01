##  第一题 使用flex实现以下布局
###  html
```
<div class="outSide">
    <div class="avatar">
        头像
    </div>
    <div class="content">
        <div class="left_content">
            左侧内容
        </div>
        <div class="right_content">
            右侧内容
        </div>
    </div>
    <div class="button_content">
        查看详情
    </div>
</div>
```
###  css

```
.outSide {
    width: 100%;
    height: 100px;
    display: flex;
    padding: 5px;
    background: skyblue;
}
.avatar {
    height: 50px;
    width: 50px;
    border: 1px solid;
    border-radius: 50%;
    line-height: 50px;
    text-align: center;
    margin-right: 10px;
}
.content {
    height: 100%;
    width: calc(100% - 30px - 100px);
    display: flex;
    margin-right: 10px;
}
.left_content {
    width: 30%;
    height: 100%;
    border: 1px solid;
    margin-right: 10px;
}
.right_content {
    width: 70%;
    height: 100%;
    border: 1px solid;
}
.button_content {
    width: 100px;
    height: 100%;
    border: 1px solid;
    text-align: center;
    line-height: 100px;
}
```

## 第二题 获取url中的指定参数的值

```
function fn(url, name) {
    // 获取所有参数，将其按照&拆分为数组
    let allNames = url.split('?')[1].split('&')
    // 声明一个变量，用来将所有参数按照键值对存储
    let objNames = {}
    allNames.map((item)=>{
        // 遍历数组中元素，将其按等号分开，左边是key，右边是value
        let key = item.split('=')[0];
        let value = item.split('=')[1];
        // 将数据按照键值对存储到对象中
        objNames[key] = value;
    })
    // 返回传入的key对应的value
    return objNames[name]
}
```

## 第三题 const newObj = JSON.parse(JSON.stringify(oldObj)) 使用这种方式是在做什么，会有什么问题
```
const newObj = JSON.parse(JSON.stringify(oldObj))
这种方式可以将数组oldObj对象中的内容拷贝到newObj中，两个对象地址就不是用的同一个地址，不会互相影响
问题：如果oldObj中有时间对象，拷贝到newObj中会变成字符串
     如果oldObj中有正则表达式，拷贝过去后只能得到空对象
     函数，undefined拷贝过去会丢失
     null，Infinity和-Infinity（无穷大和无穷小）拷贝过去都会变成null
     如果是是构造器函数生成的oldObj，拷贝时会丢失构造器函数constructor
```

## 第四题 简述节流和防抖并实现这两个函数
```
// 节流函数，在指定时间内多次触发一个事件，只会到了那个时间后才会执行事件（频繁多次触发，按时间间隔执行）
const throttle = (fn, dealy=500) => {
    var timer = null;
    return () => {
        if (timer === null) {
            timer = setTimeout(() => {
                fn();
                timer = null;
            }, dealy)
        }
    }
}

// 防抖函数，在短时间内，多次触发一个事件，只会执行最后一次的事件（频繁多次触发只执行最后一次）
const debounce = (fn,dealy) => {
    var timer = null;
    return () => {
        if(timer !== null){
            clearTimeout(timer);
        }
        timer = setTimeout(fn,dealy);
    }
}
```
