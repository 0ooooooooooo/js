# DOM 元素全屏状态监测指南

## 🎯 功能简介

本指南介绍了如何使用 JavaScript 的全屏 API 来监测和控制 DOM 元素的全屏状态，提供更好的用户交互体验。

## 💻 核心 API

### 1. 主要方法和属性
```javascript
// 请求全屏
Element.requestFullscreen()
// 退出全屏
document.exitFullscreen()
// 获取当前全屏元素
document.fullscreenElement
```

## 📝 代码实现

```javascript
// 获取目标元素
const element = document.getElementById('yourElementId');

// 全屏状态检测
function isElementFullScreen() {
    return document.fullscreenElement === element;
}

// 监听全屏变化
document.addEventListener("fullscreenchange", () => {
    if (isElementFullScreen()) {
        console.log("指定的元素处于全屏模式");
    } else {
        console.log("指定的元素不在全屏模式");
    }
});

// 进入全屏
function enterFullScreen() {
    if (element.requestFullscreen) {
        element.requestFullscreen();
    } else if (element.webkitRequestFullscreen) { // Safari
        element.webkitRequestFullscreen();
    } else if (element.msRequestFullscreen) { // IE11
        element.msRequestFullscreen();
    }
}

// 退出全屏
function exitFullScreen() {
    if (document.exitFullscreen) {
        document.exitFullscreen();
    } else if (document.webkitExitFullscreen) {
        document.webkitExitFullscreen();
    } else if (document.msExitFullscreen) {
        document.msExitFullscreen();
    }
}
```

## 🚀 使用方法

### 1. HTML 结构
```html
<div id="fullscreenElement">
    <button onclick="enterFullScreen()">进入全屏</button>
    <button onclick="exitFullScreen()">退出全屏</button>
    <div class="content">
        <!-- 全屏内容 -->
    </div>
</div>
```

### 2. 调用示例
```javascript
// 进入全屏
document.querySelector('#fullscreenBtn').addEventListener('click', enterFullScreen);

// 退出全屏
document.querySelector('#exitBtn').addEventListener('click', exitFullScreen);
```

## ⚙️ 功能特性

1. **全屏控制**
   - 支持元素进入全屏
   - 支持退出全屏模式
   - 状态实时监测

2. **兼容处理**
   - 支持主流浏览器
   - 优雅降级处理

## ⚠️ 注意事项

1. **DOM 要求**
   - 确保元素已在 DOM 中
   - 元素 ID 正确设置

2. **浏览器限制**
   - 需要用户交互触发
   - 不同浏览器兼容性处理

3. **安全考虑**
   - 仅在用户操作时触发
   - 提供退出全屏选项

## 📚 相关资源

- [Fullscreen API MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Fullscreen_API)
- [浏览器兼容性](https://caniuse.com/?search=fullscreen)
- [W3C 规范](https://w3c.github.io/fullscreen/)

## 🔧 调试技巧

1. **检查全屏状态**
```javascript
console.log(document.fullscreenElement ? '全屏中' : '非全屏');
```

2. **监听错误**
```javascript
document.addEventListener('fullscreenerror', (e) => {
    console.error('全屏操作失败:', e);
});
```

## 📄 许可证

MIT License

---

💡 **提示**: 建议在实际使用时添加适当的错误处理和用户反馈机制。
