
# 闭包closure

[toc]
## 摘要

## 关键字
执行环境 活动对象
## 前置知识点

[变量对象]()，每个执行环境都有一个表示变量都的对象。
- 全局[变量对象]()始终存在；
- 函数等局部环境的[变量对象]()在执行中存在；

### 函数作用域链
- 函数创建时
    - 创建一个预先包含[全局变量对象]()的[作用域链]()，这个[作用域链]()被保存在内部的[&#91;&#91;scope&#93;&#93;]()属性中。
- 函数执行时
    - 首先，创建一个[执行环境]()。
    - 然后，创建作用域链。
        - 将函数的[&#91;&#91;scope&#93;&#93;]()属性推入[执行环境]()的[作用域链]()。
        - 本地[活动对象]()被创建，并推入执行环境的最前端（栈顶）。
        - 注：此时，作用域链中包含两个[变量对象]()。
    - 使用[arguments]()和其他[命名参数]()的值来初始化函数的[活动对象]()。
- 函数执行完毕
    - 局部[活动对象]()被销毁；
> 作用域链本质上是一个指向变量对象的指针列表，引用但不包含变量的对象。



## 2.闭包
闭包，有权访问另一个函数作用域中的变量的函数

### 闭包的作用域链

```js
function outFnFactory(args){
    return innerFnFactory(arg1, arg2){
        var val1 = arg1[args];
        var val2 = arg2[args];
        if(val1 < val2){
            return -1
        } else if(val1 > val2){
            return 1;
        } else {
            return 0;
        }
    }
}
var outFn = outFnFactory('name');
var result = outFn({name: 'sxw'}, {name: 'wizard});
```

对于outFnFactory,
- 创建时
    - 作用域链 -> &#91;全局变量对象&#93;
- 执行时
    - 作用域链 -> &#91;outFnFactory活动对象, 全局变量对象&#93;
- 销毁时
    - outFnFactory活动对象活动对象不会被销毁，因为返回的innerFnFactory将继续引用这个活动对象





对于innerFnFactory,

- 创建时 
    - 作用域链 -> &#91;outFnFactory活动对象, 全局变量对象&#93;
- 执行时 
    - 作用域链 -> &#91;innerFnFactory活动对象, outFnFactory活动对象, 全局变量对象&#93;

## 函数调用