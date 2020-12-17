# [```await```](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/await)
Web 开发技术 > JavaScript > JavaScript 参考 > 表达式和运算符 > await

await  操作符用于等待一个```Promise``` 对象。它只能在异步函数 ```async function``` 中使用。

## 语法
```js
[返回值] = await 表达式;
```
### 表达式
一个 ```Promise``` 对象或者任何要等待的值。
### 返回值
返回 ```Promise``` 对象的处理结果。如果等待的不是 ```Promise``` 对象，则返回该值本身。

## 描述
```await``` 表达式会暂停当前 ```async function``` 的执行，等待 ```Promise``` 处理完成。若 ```Promise``` 正常处理(```fulfilled```)，其回调的```resolve```函数参数作为 ```await``` 表达式的值，继续执行 ```async function```。

若 ```Promise``` 处理异常(```rejected```)，```await``` 表达式会把 ```Promise``` 的异常原因抛出。

另外，如果 ```await``` 操作符后的表达式的值不是一个 ```Promise```，则返回该值本身。

## 例子
如果一个 ```Promise``` 被传递给一个 ```await``` 操作符，```await``` 将等待 ```Promise``` 正常处理完成并返回其处理结果。
```js
function resolveAfter2Seconds(x) {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve(x);
    }, 2000);
  });
}

async function f1() {
  var x = await resolveAfter2Seconds(10);
  console.log(x); // 10
}
f1();
```
如果该值不是一个 ```Promise```，```await``` 会把该值转换为已正常处理的```Promise```，然后等待其处理结果。
```js
async function f2() {
  var y = await 20;
  console.log(y); // 20
}
f2();
```
如果 ```Promise``` 处理异常，则异常值被抛出。
```js
async function f3() {
  try {
    var z = await Promise.reject(30);
  } catch (e) {
    console.log(e); // 30
  }
}
f3();
```
## 规范
| Specification | Status | Comment |
|-|-|-|
| ECMAScript Async Functions(async function) | Draft | 提案 |
## 浏览器兼容性
> We're converting our compatibility data into a machine-readable JSON format. This compatibility table still uses the old format, because we haven't yet converted the data it contains. Find out how you can help!
- Desktop
- Mobile

| Feature	Chrome | Firefox (Gecko) | Internet Explorer | Edge | Opera | Safari (WebKit) |
|-|-|-|-|-|-|
| 基本支持 | 55 | 52.0 (52.0) | ? | ? | 42 | ? |
| Feature | Android | Android Webview | Firefox Mobile (Gecko) | IE Mobile | Opera Mobile | Safari Mobile | Chrome for Android |
|-|-|-|-|-|-|-|-|
|  基本支持 | 未实现 | 未实现 | 52.0 (52.0) | ? | 42 | ?	55 |

## 查看更多
- [async 函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/async_function)
- [async 函数表达式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/async_function)
- [AsyncFunction object](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/AsyncFunction)