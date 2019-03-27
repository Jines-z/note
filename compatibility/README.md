## 移动端兼容性处理

### Ios 滑动不流畅：
-webkit-overflow-scrolling: touch;

### Android 低端机 float 循环布局时，丢失下标：
使用display: inline-block;

### 图片加载出错（占位图）
javascript: onerror

vue: @error

注意：不要循环 error

### 文本溢出，显示省略号
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
    const $span = document.querySelector('span')
    const text = $span.innerHTML
    let line = 3 // 超出3行显示...
    let fontSize = 14
    let maxWidth = line * $span.offsetWidth // 3行占用总宽度
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
    $span.innerHTML = ellipsis(text)
</script>
```

### input 字母"y g"等显示不全
ios 中 form 内的 input 默认有圆角 50%，需修改。

左侧字母显示不全，布局时用text-indent解决。

### input 软键盘搜索
必须用form包裹
```
<form action="javascript:void(0)">
    <input type="search" />
</form>
```

### input 上传文件
必须用form包裹
```
<form encType="multipart/form-data" action="javascript:void(0)">
    <input multiple="multiple" type="file" />
</form>
```

### input android软键盘弹起时，窗口高度变小
可以通过 js 获取窗口高度，设置最外层高度为固定值非 100% 即可

### input、select 软键盘弹起时，有可滚动内容时，fixed失效
下面代码会失效：
```html
    <header style="position: fixed"></header>

    <!-- 可以滚动区域 -->
    <main style="height: 2000px">
        <!-- 内容... -->
    </main>

    <footer style="position: fixed"></footer>
```
用含有position: absolute属性的容器隔离开，不会失效：
```html
    <header style="position: fixed"></header>

    <!-- 可以滚动的区域 -->
    <main style="position: absolute; top: 0; left: 0;">
        <div class="content"></div>
    </main>

    <footer style="position: fixed"></footer>
```

### 文本换行包含英文单词
断开单词：word-break: break-all;

不断开：  word-break: break-word;

### iframe
ios8 中必须有初始高度，不然不加载

android 设备中有遮罩的情况下，会点击穿透，应做多重优化，iframe 和容器都设置 overflow: hidden; 并点击事件阻止冒泡，iframe 内部也应有遮罩。

同主域情况下，可以使用postMessage来设置动态高度

### Flex
左侧定宽，右侧自适应宽 100% 时，其内容超出宽度时，会撑大右侧的宽

### Pre
pre标签在 ios8、ios9 中不会保留格式，需设置 white-space: pre-wrap;

### 优化
对于小屏幕的适配

iphone X 适配

移动端为了优化用户体验，应 keep alive，并记住滚动条位置

ios中有默认滚动条，android中没有，需特殊处理

断网提示

[目录](https://github.com/jines-z/note)
