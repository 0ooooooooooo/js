# BroadcastChannel 通信示例

## 🎯 功能简介

这是一个使用 `BroadcastChannel` API 实现的页面间通信示例，展示了如何在主页面和 iframe 之间进行消息传递。

## 📁 项目结构

```
BroadcastChannel/
├── index.html   # 主页面
├── iframe.html  # iframe 页面
└── README.md    # 项目说明
```

## 💻 代码实现

### 主页面 (index.html)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>BroadcastChannel Demo</title>
</head>
<body>
    <div>
        <div>index</div>
        <input type="text" id="input">
        <button>postMessage</button>
        <button>close channel</button>
        <button>open channel</button>
        <div class="content"></div>
    </div>
    <div style="margin-top: 20px;">
        <div>iframe</div>
        <iframe src="./iframe.html" frameborder="0"></iframe>
    </div>
</body>
<script>
    let broadcastChannel = new BroadcastChannel('channel');
    // ...实现代码...
</script>
</html>
```

### iframe 页面 (iframe.html)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>BroadcastChannel iframe</title>
</head>
<body>
    <div>
        <input type="text" id="input">
        <button>postMessage</button>
        <button>close channel</button>
        <button>open channel</button>
        <div class="content"></div>
    </div>
</body>
<script>
    const broadcastChannel = new BroadcastChannel('channel');
    // ...实现代码...
</script>
</html>
```

## 📝 功能说明

### 1. 消息发送
- 通过输入框输入消息
- 点击 `postMessage` 按钮发送消息
- 消息会在不同页面间广播

### 2. 通道控制
- `close channel`: 关闭通信通道
- `open channel`: 重新打开通信通道
- 实时显示接收到的消息

## 🔧 使用方法

1. **环境准备**
   - 需要本地服务器环境（如 http-server）
   - 确保文件放置在同一目录下

2. **启动项目**
   ```bash
   npx http-server
   ```

3. **访问页面**
   - 打开浏览器访问 `http://localhost:8080/index.html`

## ⚙️ 核心功能实现

### 创建通道
```javascript
const broadcastChannel = new BroadcastChannel('channel');
```

### 消息监听
```javascript
broadcastChannel.onmessage = (event) => {
    content.innerHTML = 'received: ' + event.data;
};
```

### 消息发送
```javascript
broadcastChannel.postMessage(input.value);
```

## 🚀 特性

1. **实时通信**
   - 页面间即时消息传递
   - 支持多页面广播

2. **可控性**
   - 支持手动关闭通道
   - 可随时重新建立连接

3. **简单集成**
   - 无需复杂配置
   - 原生 API 支持

## ⚠️ 注意事项

- 仅支持同源页面间通信
- 需要现代浏览器支持
- 关闭通道后需要重新创建才能继续通信

## 📚 相关资源

- [BroadcastChannel API](https://developer.mozilla.org/docs/Web/API/BroadcastChannel)
- [Same-origin policy](https://developer.mozilla.org/docs/Web/Security/Same-origin_policy)
- [Web Workers API](https://developer.mozilla.org/docs/Web/API/Web_Workers_API)

## 📄 许可证

MIT License
