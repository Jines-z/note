## 移动端兼容性处理

### 微信 wx-open-audio 开放标签兼容性
-   封装格式 wav + 编码格式 pcm_s32le无法播放。
-   兼容性最好的封装格式是 mp3。
-   暂停时设置 playbackRate 无效。开放标签初始化完成前设置 playbackRate 会将该属性的 setter 覆盖导致后续设置倍速失效。

### video requestFullscreen
IOS 中 requestFullscreen 只能使用 video 调用。Android 中其他元素可以调用 requestFullscreen 使该 dom 全屏。

### 视频全屏兼容性
当视频为横向视频时，某些安卓机全屏后会自动旋转至横屏，需要监听屏幕旋转做额外处理。

### 监听屏幕旋转
-   IOS 使用 orientationchange。
-   Android 使用 MediaQueryList。Android@4 及以下需使用 addListener。以上使用 addEventListener。

### Vue slot 兼容性
vue@2.5.16 中，单一组件内部不可使用多个同名 slot，会报 warning，需使用 this。$slots + component 的思想，将 slot 取出并增加 render 方法当做一个内部组件来复用。

### m3u8 格式视频播放
IOS 原生支持播放m3u8，Android 需要使用 hls.js 兼容。

### Ios overflow 滑动不流畅：
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
```html
<form encType="multipart/form-data" action="javascript:void(0)">
    <input multiple="multiple" type="file" />
</form>
```

### input 移动端 type="number" 只能输入非负数字
```html
<input pattern="[0-9]*" type="tel">
```
```javascript
value.replace(/\D/g, '')
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
pre 标签在 ios8、ios9 中不会保留格式，需设置 white-space: pre-wrap;

### 优化
对于小屏幕的适配

iphone X 适配

移动端为了优化用户体验，应 keep alive，并记住滚动条位置

ios中有默认滚动条，android中没有，需特殊处理

断网提示

[目录](https://github.com/jines-z/note)
