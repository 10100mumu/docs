# Symbol

JavaScript 第七种数据类型，表示独一无二的值

* Symbol 值通过`Symbol()`生成，对象的属性可以是字符串类型，也可以是 Symbol 类型
* 调用`Symbol()`不能使用`new`命令，接受一个字符串作为函数的参数，主要是对 Symbol 值的描述，在控制台显示
* Symbol 值不能参与运算
* Symbol 值可以转化为布尔值，但是不能转化为数值
* Symbol 值不是私有属性

## 作为属性名的 Symbol 

每个 Symbol 值都是唯一的，意味着 Symbol 可以作为标识符

```javascript
let mySymbol = Symbol()
//第一种写法
let a = {};
a[mySymbol] = 'hello'
//第二种写法
let a = {
	[mySymbol]: 'hello'
}
//第三种写法
let a = {}
Object.defineProperty(a, mySymbol, {value: 'hello'})

```

Symbol 作为属性名时，不能用点运算符

## 实例：消除魔术字符串

魔术字符串：在代码中多次出现，与代码形成强耦合的某一具体的字符串或值。

在代码编写过程中，尽量用`Symbol`值来代替魔术字符串

## 属性名的遍历

* 通过`Object.getOwnPropertySymbols`和`Reflect.ownKeys()`可以获取对象的`Symbol`属性
* 可以利用`Symbol`属性的特性可以定义一些非私有，但又只希望用于内部的方法

## Symbol.for(), Symbol.keyFor()

* 可以通过`Symbol.for()`方法定义相同的`Symbol`值，以相同`key`生成的`Symbol`值为同一个`Symbol`值
* `Symbol.keyFor()`，参数为一个`Symbol`值，返回一个已经登记`Symbol`值的`key`，简单来说，利用`Symbol()`生成的值，`key`都不会相同

```javascript
var sy = Symbol.for('foo')
Symbol.keyFor(sy) // "foo"
```

## 内置的 Symbol 值

除了自定义的 Symbol 之外，JavaScript 还定义了一些内置的 Symbol 值

**Symbol.hasInstance**

指向对象的一个内部方法，当其他对象使用`instanceof`运算符的时候会调用该方法

```javascript
var str = new String('abc')
str instanceof String // true
// 等同于
String[Symbol.hasInstance](str) // true
```

**Symbol.isConcatSpreadable**

返回一个布尔值，表示对象是否可以使用`concat()`方法是否展开

```javascript
var arr = [1, 2]
var arr2 = [3, 4]
arr2.concat(arr) // [3, 4, 1, 2]
arr[Symbol.isConcatSpreadable] = false
arr2.concat(arr) // [3, 4, [1, 2]]
```

**Symbol.iterator**

对象的`Symbol.iterator`属性，指向改对象的遍历器，只要对象具有该属性，则表示该对象部署了 Iterator 接口，可以使用`for...of`进行遍历