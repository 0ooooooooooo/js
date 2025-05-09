# 异步字符串替换示例

## 🎯 功能简介

这个示例展示了如何在 JavaScript 中使用 async/await 和 Promise 实现异步字符串替换功能，将数字转换为带前缀的字符串。

## 💻 代码实现

````javascript
// 原始字符串
const temp = "11-14-1431211313~~~141————123";

// 定义异步函数
const getName = (name1) => {
    return new Promise((resolve, reject) => {
        resolve('name' + name1);
    })
};

// 匹配数字并处理
const res = temp.match(/\d+/g);
const b = res.map(getName);
const c = await Promise.all(b);

// 替换原字符串
const d = temp.replace(/\d+/g, () => {
    return c.shift();
});

console.log(d);
````

## 📝 代码解析

### 1. 初始化数据
```javascript
const temp = "11-14-1431211313~~~141————123";
```
定义了一个包含数字和特殊字符的原始字符串。

### 2. 异步处理函数
```javascript
const getName = (name1) => {
    return new Promise((resolve, reject) => {
        resolve('name' + name1);
    })
};
```
- 创建一个返回 Promise 的异步函数
- 将输入的数字转换为 "name + 数字" 的格式
- 使用 resolve 返回处理结果

### 3. 数字提取与转换
```javascript
const res = temp.match(/\d+/g);
const b = res.map(getName);
const c = await Promise.all(b);
```
1. 使用正则表达式 `/\d+/g` 匹配所有数字
2. 对每个数字调用 `getName` 函数
3. 使用 `Promise.all` 等待所有异步操作完成

### 4. 字符串替换
```javascript
const d = temp.replace(/\d+/g, () => {
    return c.shift();
});
```
- 使用 `replace` 方法替换原字符串中的数字
- `shift()` 方法依次取出转换后的值

## 🎨 示例输出

**输入：**
```
11-14-1431211313~~~141————123
```

**输出：**
```
name11-name14-name1431211313~~~name141————name123
```

## 🔧 使用场景

1. **API 数据转换**
   - 需要从远程 API 获取替换内容
   - 数据需要异步处理

2. **数据库操作**
   - 替换内容需要从数据库查询
   - 涉及异步数据读取

3. **复杂字符串处理**
   - 需要批量处理大量数据
   - 包含多个异步操作

## 📚 相关资源

- [Promise MDN 文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [Async/Await MDN 文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/async_function)
- [JavaScript 正则表达式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions)

## 📄 许可证

MIT License
