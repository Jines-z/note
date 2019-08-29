## 二分查找

1、先排序；

2、确定该区间的left、right、middle位置；

3、将目标值与 Array[middle] 对比

* 若相等，返回该位置
* 若不等，重新确定区间，循环进行比较

```Javascript
function halfSearch(arr, target){
    let left = 0
    let right = arr.length - 1
    while (left <= right) {
        const middle = Math.floor((left + right) / 2)
        if (target == arr[middle]) {
            return middle
        } else if (target < arr[middle]) {
            right = middle - 1
        } else if (target > arr[middle]) {
            left = middle + 1
        }
    }
}
```
[目录](https://github.com/jines-z/note)
