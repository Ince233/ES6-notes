#### let: let的特点，与var的区别：

- 变量不能重复声明
- 存在块级作用域
- 不存在变量提升
- 不影响作用域链

#### const特点：

- 一定要赋初值
- 值不能修改
- 存在块级作用域
- 对于数组常量和对象常量的元素可以修改

#### 变量的解构赋值

- 数组的解构
- 对象的结构

#### 模板字符串

- 反引号字符串
- 可直接出现换行符
- 变量拼接${}

#### 对象的简化写法

- 对象属性键名和变量名一致时可以简化成一个

#### 箭头函数

- 箭头函数的this始终指向函数声明时作用域下的this，而普通函数的this指向函数调用时的作用域
- 不能作为构造实例化对象
- 不能使用arguments变量
- 箭头函数的简写
- 箭头函数适合与this无关的回调，例如计时器，数组的操作  

#### 函数参数的默认值设置

- 形参初始值，具有默认值的参数，一般位置要靠后
- 与解构赋值可结合使用

#### rest参数

- arguments放在形参列表，而...args放在实参列表

- 箭头函数的this始终指向声明时的作用域的this，而普通函数的this一般指向调用时作用域

- 不能作为构造实例化对象

- 不能使用arguments

- 箭头函数的简写

- 适合使用箭头函数的情景：与this无关的回调，例如定时器，数组的方法

  

