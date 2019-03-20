## Debounce And Throttle

优化窗口的`resize`、`scroll`、输入框内容校验等操作，减少浏览器的负担，提高用户体验。我们可以减少此类事件触发的频率。

#### Debounce 防抖
连续性的操作结束后执行。

```Javascript
/*
    操作结束后延时500ms执行
    @param fn function
    @param wait number
    @return function
*/
const debounce = (fn, wait) =>{
    let timeout = null
    return () => {
        if(timeout !== null) clearTimeout(timeout)
        timeout = setTimeout(fn, wait)
    }
}

// 处理函数
const handle = () =>{
    console.log(Math.random())
}

// 滚动事件
window.addEventListener('scroll', debounce(handle, 500))
```

#### Throttle 节流
持续性操作的中间，以相同时间间隔执行

```Javascript
/*
    每隔300ms触发一次，超过1000ms未触发视为第二次操作
    @param fn function
    @param wait number
    @param maxTimeLong number
    @return function
*/
const throttling = (fn, wait, maxTimeLong) =>{
    let timeout = null
    let startTime = Date.parse(new Date)
    return () =>{
        if(timeout !== null) clearTimeout(timeout)
        let curTime = Date.parse(new Date);
        if(curTime-startTime >= maxTimeLong) {
            fn()
            startTime = curTime
        } else {
            timeout = setTimeout(fn, wait)
        }
    }
}

const handle = () =>{
    console.log(Math.random());
}

window.addEventListener('scroll', throttling(handle, 300, 1000));
```
[目录](https://github.com/jines-z/note)
