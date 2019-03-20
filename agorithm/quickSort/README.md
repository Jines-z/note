## 快速排序

1、找基准；

2、遍历数组，小于基准的放left，大于基准的放right；

3、分别递归左右两边子集，将数组合并返回。

```Javascript
function quickSort(arr){
    // 若只有一个，则返回
    if (arr.length <= 1) {
        return arr
    } else {
        // 找基准，并把基准从原数组删除
        var pivotIndex = Math.floor(arr.length / 2)
        var pivot = arr.splice(pivotIndex, 1)[0]

        // 定义左右数组
        var left=[]
        var right=[]
        for(var i=0;i<arr.length;i++){
            if(arr[i]<=pivot){
                // 小于基准放置左侧
                left.push(arr[i])
            }
            else{
                // 大于基准放置右侧
                right.push(arr[i])
            }
        }
        //递归
        return quickSort(left).concat([pivot], quickSort(right))
    }
}
```
[目录](https://github.com/jines-z/note)
