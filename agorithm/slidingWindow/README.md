## 滑动窗口

*   双指针确定一个窗口

*   遍历的时候，两个指针一前一后夹着的子串（子数组）类似一个窗口，这个窗口大小和范围会随着前后指针的移动发生变化

![滑动窗口](https://jines-z.github.io/images/window.png)

```Javascript
// 找到一个字符串中，无重复长度的最长子串
const str = 'pwwkewaaaasdfg'
let maxLength = 0
let winStart = 0 // 窗口的起点
let map = new Map()
for (let i = 0; i < str.length; i++) { // i 是窗口的终点
    if (map.has(str[i])) {
        maxLength = maxLength > map.size ? maxLength : map.size
        map.clear()
        winStart += 1 // 改变窗口的起点
        i = winStart // 回滚
    } else {
        map.set(str[i], 1)
        if (i === str.length - 1) {
            console.log(maxLength > map.size ? maxLength : map.size)
        }
    }
}
```
[目录](https://github.com/jines-z/note)
