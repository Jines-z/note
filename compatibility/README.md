## Node Tools

#### Ios 滑动不流畅：
-webkit-overflow-scrolling: touch;

##### Android 低端机 float 循环布局时，丢失下标：
使用display: inline-block;

#### 图片加载出错（占位图）
javascript: onerror

vue: @error

注意：不要循环 error

#### 文本溢出，显示省略号
单行：
```css
.ellipsis {
    width: 100px;
    display: inline-block;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
```
多行:
```css
.ellipsis {
    width: 100px;
    overflow: hidden;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 3;
    text-overflow: ellipsis;
}
```
-webkit-line-clamp 是一个不规范的属性，某些 android 低端机不支持，此时应使用 js 处理：
```html
<style>
    span {
        width: 100px;
        font-size: 14px;
        display: inline-block;
        line-height: 16px;
        word-break: break-all;
    }
</style>

<span>爱上【A}】邓12—_-~`丽君aaaa卡了跨界石考虑到佳世客拉大锯啊打开了啊数据库拉三等奖拉斯肯德基阿卡丽大师级的卡拉加大款拉大锯啊了可多</span>

<script type="text/javascript">
    const $dom = document.querySelector('span')
    const text = $dom.innerHTML
    let line = 3 // 超出3行显示...
    let fontSize = 14
    let maxWidth = line * $dom.offsetWidth // 3行占用总宽度
    let maxAt = Math.floor(maxWidth / fontSize) * 2
    function ellipsis(str) {
        let realLength = 0
        for (let i = 0; i < str.length; i++) {
            if (realLength >= maxAt) {
                return str.substr(0, i - 3) + '...'
            }
            const charCode = str.charCodeAt(i)
            if (charCode >= 0 && charCode <= 128) {
                realLength += 1
            } else {
                realLength += 2
            }
        }
    }
    $dom.innerHTML = ellipsis(text)
</script>
```

#### 文本换行包含英文单词
断开单词：word-break: break-all;

不断开：  word-break: break-word;

#### iframe
ios8 中必须有初始高度，不然不加载

android 设备中有遮罩的情况下，会点击穿透，应做多重优化，iframe 和容器都设置 overflow: hidden; 并点击事件阻止冒泡，iframe 内部也应有遮罩。

同主域情况下，可以使用postMessage来设置动态高度

#### Flex
左侧定宽，右侧自适应宽 100% 时，其内容超出宽度时，会撑大右侧的宽

#### Pre
pre标签在 ios8、ios9 中不会保留格式，需设置 white-space: pre-wrap;

#### 优化
对于小屏幕的适配

iphone X 适配

移动端为了优化用户体验，应 keep alive，并记住滚动条位置

ios中有默认滚动条，android中没有，需特殊处理

[目录](https://github.com/beverle-y/note)
