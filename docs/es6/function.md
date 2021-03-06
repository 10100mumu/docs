# 函数的扩展

## 函数参数的默认值 

* ES6 允许直接为函数参数指定默认值
* 与解构赋值默认值结合使用
* 建议将带有默认值的参数放在尾部，因为如果放在前面或者中间，在调用函数的时候就必须传该参数，否则会报错
* 函数的`length`属性返回函数不带默认值参数的个数
* 一旦设置了参数的默认值，参数会形成一个单独的作用域，等初始化完成，这个作用域消失

**应用：指定一个参数不得省略，省略则抛出错误**

```javascript
function throwIfMissing() {
  throw new Error('Missing parameter');
}

function foo(mustBeProvided = throwIfMissing()) {
  return mustBeProvided;
}

foo()
// Error: Missing parameter
```

## rest 参数
* 可以理解为`arguments`的替代品，`arguments`为类数组对象，`rest参数`则是真正的数组

```javascript
// 求和函数
function add(...values){
  return values.reduce((a, b) => {
    return a + b;
  })
}
```

## 严格模式

函数参数使用了默认值、解构赋值、扩展运算符，那么在函数内部不能显示设定为严格模式，否则会报错

## name 属性

返回函数的函数名

## 箭头函数

ES6 允许使用箭头`=>`定义函数

```javascript
var f = v => v;
// 等同于
var f = function(v){
  return v;
}
```

* 使用圆括号代替参数部分
* 如果函数代码块不止一条语句，则用大括号括起来，如果只有一行语句，则可省去大括号
* 如果要返回一个对象，则用圆括号将对象包裹起来

```javascipt
var f = (v) => ({result: v + 1});
f(5)  // {result: 6}
```

使用注意点

1. 函数体的`this`对象，不是使用时所在的对象，而是始终指向声明箭头函数所在的作用域，固定了`this`的指向，极大解决了`this`对象指向不明确的问题
2. 不可以作为构造函数
3. 不可以使用`arguments`对象，可以使用`rest参数`代替
4. 不可以使用`yield命令`，因此箭头函数不能用做`Generator函数`

## 双冒号运算符

`apply`、`call`、`bind` 的替代方案，显示指定函数的上下文对象

```javascript
foo::bar
//	等同于
bar.bind(foo);
foo::bar(...arguments)
//	等同于
bar.apply(foo, arguments)
```

## 尾调用优化

> 尾调用：函数的最后一步调用其他函数

在不再用到外部函数内部变量的情况下，会去掉外层函数的调用帧，只保留最后一个执行函数的调用帧，大大减少内存的使用量

* 尾递归优化

```javascript
//	计算阶乘
function factorial(n){
  if(n == 1) return 1
  return n * factorial(n - 1)
}
//	上面这种方法会一直保留上一调用帧的变量，非常耗费内存，进过尾递归优化之后变成：

function f(n, total){
  if(n == 1) return total;
  return f(n - 1, n * total)
}
//	把变量放到下一调用帧，删除上一调用帧，节省内存开销
// 练习：使用尾递归优化计算斐波拉切竖列前n项和
```
* 递归函数的改写

确保最后一步调用自身，把中间变量改写成函数的参数，就像上面例子中的 total

* 尾调用优化只在严格模式下起作用，是因为正常模式通过`func.arguments``func.caller` 跟踪函数的调用栈，在严格模式下，这两个变量会失真，自然就减少了函数的调用栈，也就实现不了函数的尾调用优化

## 函数参数的尾逗号

为了在参数写成多行的时候，增加参数在上一行多加一个逗号，那么上一行也会被视为版本发生了变动，这看上去有点冗余，所以 ES6 允许在函数最后一个参数后面可以加上逗号，保持一致性
