# Event 对象

* 事件发生之后，会产生一个 `Event` 对象，作为参数传递给监听函数。所有的事件都是这个对象的实例，或者说是继承了 `Event.prototype`
* `Event` 对象是一个构造函数，可以通过 `new` 创建一个事件，接受两个参数，第一个是字符串 `type`，表示事件名，第二个是对象，表示事件的配置，该对象有下面两个属性
	1. `bubbles`: 布尔值，默认 `false` ，表示事件是否冒泡
	2. `cancelable`: 布尔值，默认 `false` ，表示事件是否可以被取消，即能否用 `Event.preventDefault()` 取消这个事件

## 实例属性

| attribute | desc |
| --- | --- |
| Event.bubbles </br> Event.eventPhase| 当前事件是否可以冒泡，只读 </br> 返回有四种可能 </br> - 0 事件未发生 </br> - 1 事件处于捕获阶段，从祖先向下传播的过程 </br> - 2 事件到达目标节点，即 `Event.target` 指向目标节点 <br> - 3 - 事件处于冒泡阶段，从目标节点向祖先反传播的过程 |
| Event.cancelable </br> Event.cancelbubble </br> Event.defaultPrevented | 事件是否可以取消，浏览器原生事件是可以取消的，只读 </br> 将 `Event.cancelBubble` 设置为 `true`，等于执行了 `Event.stoppropagation()` 阻止事件的传播 </br> 事件是否执行过 `preventDefault()` 方法，只读 |
| Event.currentTarget </br> Event.target | 事件当前所处节点对象 </br> 事件的目标对象 |
| Event.type | 返回事件的名称 |
| Event.timeStamp | 返回事件发生距离浏览器加载网页完成的时间 |
| Event.isTrusted | 表示时间是否由用户真实行为产生的，比如点击产生的 `click` 事件，手动调用 `click()` 方法触发的事件该属性返回 `false` ，通过 `new` 创建出来的时间的该属性返回为 `false` |
| Event.detail | 该属性只有浏览器的 UI 事件才具有，该属性返回一个数值，表示事件的某种信息，比如，对于点击事件，会返回 1, 2, 3 表示点击的次数，对于滚动事件，则返回滚轮滚动的距离 |

## 实例方法
| method | desc |
| --- | --- |
| Event.preventDefault() | 取消浏览器对当前事件的默认行为，如果事件的 `cancelalbe` 为 `false` ，调用该方法无效，不会阻止事件的传播 |
| Event.stopPropagation() </br> Event.stopImmediatePropagation() | 阻止事件的继续传播，不影响当前节点的其他监听函数 </br> 阻止事件的传播，当前节点的其他监听函数也不会执行 |
| Event.composedPath() | 返回一个数组，成员是事件在冒泡过程中一次经过的节点，一直到 `Window` |

## 参考

[网道（WangDoc.com）是一个文档网站，提供互联网开发文档](https://wangdoc.com/javascript/events/event.html)