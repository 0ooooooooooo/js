# JavaScript 数组方法对比指南

## 🎯 功能简介

本文详细介绍了 JavaScript 中 `[].map.call()` 和直接使用 `.map()` 的区别，帮助开发者在不同场景下选择合适的数组处理方法。

## 💻 使用方法对比

### 1. 直接使用 .map()
```javascript
// 适用于标准数组
const arr = [1, 2, 3];
const result = arr.map(x => x * 2); // [2, 4, 6]
```

### 2. [].map.call()
```javascript
// 适用于类数组对象
const nodeList = document.querySelectorAll("div");
const result = [].map.call(nodeList, node => node.className);
```

## 📝 实际应用示例

### DOM 元素处理
```javascript
// 传统方法
const scripts = document.querySelectorAll("script");
const scriptUrls = [].map.call(scripts, s => s.src);

// 现代方法
const modernUrls = Array.from(scripts).map(s => s.src);
// 或使用展开运算符
const spreadUrls = [...scripts].map(s => s.src);
```

### 函数参数处理
```javascript
function sumNumbers() {
    // 处理 arguments 对象
    return [].map.call(arguments, Number)
             .reduce((a, b) => a + b, 0);
}
```

## ⚙️ 性能考虑

1. **执行效率**
   - `[].map.call()` 略慢（需要额外函数调用）
   - 直接 `.map()` 性能更优

2. **内存使用**
   - `.map()` 内存效率高
   - `[].map.call()` 创建临时数组对象

## 🚀 最佳实践

### 现代项目
```javascript
// 推荐使用 Array.from
const elements = Array.from(document.querySelectorAll('.class'));
const results = elements.map(el => el.dataset.value);
```

### 兼容性考虑
```javascript
// 需要兼容旧浏览器时使用
const elements = document.querySelectorAll('.class');
const results = [].map.call(elements, el => el.dataset.value);
```

## ⚠️ 常见陷阱

### this 绑定问题
```javascript
const obj = {
    values: [1, 2, 3],
    multiply: function() {
        // ✅ 正确用法：使用箭头函数
        [].map.call(this.values, (item) => item * this.factor);
    },
    factor: 2
};
```

## 🔧 调试工具

### 类型检查
```javascript
// 检查数组类型
function checkArrayType(obj) {
    console.log({
        isArray: Array.isArray(obj),
        isIterable: typeof obj[Symbol.iterator] === 'function'
    });
}
```

### 安全调用包装
```javascript
function safeMap(arrayLike, callback) {
    try {
        return Array.from(arrayLike).map(callback);
    } catch (e) {
        return [].map.call(arrayLike, callback);
    }
}
```

## 📚 相关资源

- [Array.prototype.map()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
- [Array.from()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
- [展开运算符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

## 📄 许可证

MIT License

---

💡 **提示**: 在现代项目中优先使用 `Array.from()` 或展开运算符，仅在需要兼容旧浏览器时使用 `[].map.call()`。
