## 选择排序

1、双层循环；

2、每次选中外层特定下标的值，与内层该下标后边的值进行比较，若后边的值比该值小，则进行交换；

3、每次外循环可以找到内循环中最小值放到该次外循环下标处，直至排序完成。

```Javascript
function halfSearch(arr){
    for (let i = 0; i < arr.length; i++) {
        for (let j = i + 1; j < arr.length; j++) {
            if (arr[j] < arr[i]) {
                const temp = arr[j]
                arr[j] = arr[i]
                arr[i] = temp
            }
        }
    }
}
```
[目录](https://github.com/jines-z/note)
