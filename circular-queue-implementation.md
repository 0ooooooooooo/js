# JavaScript 循环队列实现指南

## 🎯 功能简介

这是一个基于 JavaScript 实现的循环队列数据结构。循环队列是一种线性数据结构，它使用固定大小的数组和两个指针来实现队列。这种实现方式能够有效地重用存储空间。

## 💻 完整代码实现

````javascript
/**
 * 循环队列构造函数
 * @param {number} k - 队列的长度
 */
var MyCircularQueue = function(k) {
    this.length = k;        // 队列长度
    this.queue = new Array(k); // 存储队列的数组
    this.front = -1;        // 队首指针，-1表示队列为空
    this.tail = -1;         // 队尾指针，-1表示队列为空
};

/**
 * 向循环队列插入一个元素
 * @param {number} value - 要插入的值
 * @return {boolean} - 插入是否成功
 */
MyCircularQueue.prototype.enQueue = function(value) {
    if (this.isFull()) {
        return false;
    }
    if (this.front === -1) {
        this.front = 0;
    }
    this.tail = (this.tail + 1) % this.length;
    this.queue[this.tail] = value;
    return true;
};

/**
 * 从循环队列中删除一个元素
 * @return {boolean} - 删除是否成功
 */
MyCircularQueue.prototype.deQueue = function() {
    if (this.isEmpty()) {
        return false;
    }
    if (this.front === this.tail) {
        this.front = -1;
        this.tail = -1;
        return true;
    }
    this.front = (this.front + 1) % this.length;
    return true;
};

/**
 * 获取队首元素
 * @return {number} - 队首元素，队列为空时返回-1
 */
MyCircularQueue.prototype.Front = function() {
    return this.isEmpty() ? -1 : this.queue[this.front];
};

/**
 * 获取队尾元素
 * @return {number} - 队尾元素，队列为空时返回-1
 */
MyCircularQueue.prototype.Rear = function() {
    return this.isEmpty() ? -1 : this.queue[this.tail];
};

/**
 * 检查队列是否为空
 * @return {boolean} - 队列是否为空
 */
MyCircularQueue.prototype.isEmpty = function() {
    return this.front === -1;
};

/**
 * 检查队列是否已满
 * @return {boolean} - 队列是否已满
 */
MyCircularQueue.prototype.isFull = function() {
    return (this.tail + 1) % this.length === this.front;
};
````

## 📝 使用示例

````javascript
// 创建大小为3的循环队列
const circularQueue = new MyCircularQueue(3);

// 插入元素
console.log(circularQueue.enQueue(1)); // 返回 true
console.log(circularQueue.enQueue(2)); // 返回 true
console.log(circularQueue.enQueue(3)); // 返回 true
console.log(circularQueue.enQueue(4)); // 返回 false，队列已满

// 查看队首和队尾元素
console.log(circularQueue.Front()); // 返回 1
console.log(circularQueue.Rear());  // 返回 3

// 删除元素
console.log(circularQueue.deQueue()); // 返回 true
console.log(circularQueue.enQueue(4)); // 返回 true

// 查看队列状态
console.log(circularQueue.isEmpty()); // 返回 false
console.log(circularQueue.isFull());  // 返回 true
````

## ⚙️ 核心概念解释

1. **循环队列结构**
   - 使用固定大小数组存储元素
   - 通过取模运算实现循环
   - 使用两个指针追踪队首和队尾

2. **指针说明**
   - front：指向队首元素
   - tail：指向队尾元素
   - -1：表示队列为空

3. **关键操作**
   - 入队：tail = (tail + 1) % length
   - 出队：front = (front + 1) % length
   - 判满：(tail + 1) % length === front

## 🔧 性能分析

- 时间复杂度：
  - 入队/出队：O(1)
  - 查看队首/队尾：O(1)
  - 判空/判满：O(1)

- 空间复杂度：O(n)，n为队列大小

## 📚 应用场景

1. **缓冲区管理**
   - 数据流处理
   - 音视频播放器

2. **任务队列**
   - 打印任务管理
   - 请求处理队列

3. **生产者消费者问题**
   - 多线程数据交换
   - 异步任务处理

## ⚠️ 注意事项

1. 初始化时需要正确设置队列大小
2. 入队前需要检查队列是否已满
3. 出队前需要检查队列是否为空
4. 注意处理队列为空和只有一个元素的边界情况

## 📄 许可证

MIT License

找到具有 1 个许可证类型的类似代码
