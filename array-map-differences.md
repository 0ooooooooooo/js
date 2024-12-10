# JavaScript 中 [].map.call 和 数组.map 的区别

## 主要区别

### 1. 使用场景

#### 直接使用 .map()
- 只能用在真正的数组对象上
- 语法更简洁直观
```javascript
const arr = [1, 2, 3];
const result = arr.map(x => x * 2);
```

#### [].map.call()
- 可以用在类数组对象（array-like objects）上，例如：
  - DOM 元素集合（如 `document.querySelectorAll()` 返回的 NodeList）
  - 函数的 `arguments` 对象
  - 字符串
```javascript
const nodeList = document.querySelectorAll("div");
const result = [].map.call(nodeList, node => node.className);
```

### 2. 工作原理
- `[].map.call()` 是借用数组原型上的 map 方法，通过 `call` 改变 `this` 指向，使其能够在类数组对象上工作
- 直接的 `.map()` 是在数组实例上直接调用方法

## 实际应用示例

### 处理 DOM 元素集合
```javascript
// 使用 [].map.call
const scripts = document.querySelectorAll("script");
const scriptUrls = [].map.call(scripts, s => s.src);

// 现代写法替代方案
const scriptUrls = Array.from(scripts).map(s => s.src);
// 或者使用展开运算符
const scriptUrls = [...scripts].map(s => s.src);
```

### 处理函数参数
```javascript
function example() {
    // 将 arguments 转换为数组并处理
    const args = [].map.call(arguments, arg => arg * 2);
    
    // 现代写法
    const args = Array.from(arguments).map(arg => arg * 2);
    // 或者
    const args = [...arguments].map(arg => arg * 2);
}
```

## 最佳实践建议

1. 在现代 JavaScript 中，优先使用以下方法：
   - `Array.from().map()`
   - 展开运算符 `[...].map()`

2. 使用 `[].map.call()` 的场景：
   - 需要考虑旧版浏览器兼容性时
   - 处理特殊的类数组对象时

3. 直接使用 `.map()` 的场景：
   - 处理标准数组时
   - 代码需要保持简洁时
