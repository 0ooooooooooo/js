# BroadcastChannel Demo

这是一个使用 `BroadcastChannel` API 的示例项目，展示了如何在主页面和 iframe 之间进行消息通信。

## 项目结构

```
BroadcastChannel/
├── index.html   # 主页面
├── iframe.html  # iframe 页面
└── README.md    # 项目说明
```

## 功能说明

1. **消息发送**：主页面和 iframe 页面可以通过 `BroadcastChannel` 相互发送消息。
2. **关闭通道**：可以手动关闭 `BroadcastChannel` 通道。
3. **重新打开通道**：关闭后可以重新打开 `BroadcastChannel` 通道。

## 使用方法

### 运行项目

1. 将项目文件放置在本地服务器环境中（如 `http-server` 或其他静态服务器工具）。
2. 打开 `index.html` 文件，页面会自动加载 iframe。

### 主页面功能

- 输入框用于输入消息。
- **PostMessage 按钮**：将输入框中的消息发送到 iframe 页面。
- **Close Channel 按钮**：关闭当前的 `BroadcastChannel` 通道。
- **Open Channel 按钮**：重新打开一个新的 `BroadcastChannel` 通道。

### iframe 页面功能

- 输入框用于输入消息。
- **PostMessage 按钮**：将输入框中的消息发送到主页面。
- **Close Channel 按钮**：关闭当前的 `BroadcastChannel` 通道。

## 示例代码

### 主页面 (`index.html`)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
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
</html>
<script>
    // 创建一个 BroadcastChannel 实例
    let broadcastChannel = new BroadcastChannel('channel');
    const input = document.getElementById('input');
    const postMessageButton = document.querySelector('button');
    const closeChannelButton = document.querySelectorAll('button')[1];
    const openChannelButton = document.querySelectorAll('button')[2];
    const content = document.querySelector('.content');

    // 监听来自 iframe 的消息
    broadcastChannel.onmessage = (event) => {
        content.innerHTML = 'iframe' + event.data;
    };

    // 发送消息到 iframe
    postMessageButton.addEventListener('click', () => {
        broadcastChannel.postMessage(input.value);
    });

    // 关闭 BroadcastChannel
    closeChannelButton.addEventListener('click', () => {
        broadcastChannel.close();
    });

    // 重新打开 BroadcastChannel
    openChannelButton.addEventListener('click', () => {
        broadcastChannel = new BroadcastChannel('channel');
        broadcastChannel.onmessage = (event) => {
            content.innerHTML = 'iframe' + event.data;
        };
    });
</script>
```

### iframe 页面 (`iframe.html`)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
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
</html>
<script>
    // 创建一个 BroadcastChannel 实例
    const broadcastChannel = new BroadcastChannel('channel');
    const input = document.getElementById('input');
    const postMessageButton = document.querySelector('button');
    const closeChannelButton = document.querySelectorAll('button')[1];
    const openChannelButton = document.querySelectorAll('button')[2];
    const content = document.querySelector('.content');

    // 监听来自主页面的消息
    broadcastChannel.onmessage = (event) => {
        content.innerHTML = 'index' + event.data;
    };

    // 发送消息到主页面
    postMessageButton.addEventListener('click', () => {
        broadcastChannel.postMessage(input.value);
    });

    // 关闭 BroadcastChannel
    closeChannelButton.addEventListener('click', () => {
        broadcastChannel.close();
    });
</script>
```

## 注意事项

- `BroadcastChannel` API 仅在同源的页面之间工作。
- 如果关闭了 `BroadcastChannel`，需要重新打开才能继续通信。
- 浏览器兼容性请参考 [MDN 文档](https://developer.mozilla.org/en-US/docs/Web/API/BroadcastChannel).

## 参考资料

- [BroadcastChannel API - MDN](https://developer.mozilla.org/en-US/docs/Web/API/BroadcastChannel)
