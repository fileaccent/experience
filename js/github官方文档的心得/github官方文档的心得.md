#### 一元运算符 +
加号可把一个字符转化为数字例如:
``` javascript
+'2' // 2
```
#### 幂运算符 ** 
``` javascript
a**b // a的b次方
```
``` javascript
alert( null > 0 );  // (1) false
alert( null == 0 ); // (2) false
alert( null >= 0 ); // (3) true
```
null 在相等 == 型比较中不会被转换,在 >= 中会转换成 0
``` javascript
alert( undefined > 0 ); // false (1)
alert( undefined < 0 ); // false (2)
alert( undefined == 0 ); // false (3)
```
undefined 在比较时,会被转换成 NaN

* 数字 0、空字符串 ""、null、undefined 和 NaN 都会被转换成 false。因为他们被称为 “falsy” 值。
  其他值被转换为 true，所以它们被称为 “truthy”。

* 一个或 "||" 运算的链，将返回第一个真值，如果不存在真值，就返回该链的最后一个值。
``` javascript
alert( 1 || 0 ); // 1（1 是真值）
alert( true || 'no matter what' ); //（true 是真值）
alert( null || 1 ); // 1（1 是第一个真值）
alert( null || 0 || 1 ); // 1（第一个真值）
alert( undefined || null || 0 ); // 0（所有的转化结果都是 false，返回最后一个值）
```
* 与操作寻找第一个假值
* 两个非运算 !! 有时候用来将某个值转化为布尔类型：
* 注意: 
  禁止 break/continue 在 ‘?’ 的右边
  (i > 5) ? alert(i) : continue; // continue 不允许在这个位置
* break <labelName> 语句跳出循环至标签处：
``` javascript
  outer: for (let i = 0; i < 3; i++) {
    for (let j = 0; j < 3; j++) {
      let input = prompt(`Value at coords (${i},${j})`, '');
      // 如果是空字符串或被取消，则中断并跳出这两个循环。
      if (!input) break outer; // (*)
      // 用得到的值做些事……
    }
  }
  alert('Done!');
```
* switch中的相等是严格相等

  函数
  ``` javascript
    function showMessage(from, text = anotherFunction()) {
      // anotherFunction() 仅在没有给定 text 时执行
      // 其运行结果将成为 text 的值
    }
  ```

  不要在 return 与返回值之间添加新行,浏览器默认在 return 后加分号,若要跨行要加括号

#### 函数表达式和函数声明的区别:
  函数声明:
  ``` javascript
    function sum(a, b) {
      return a + b;
    }
  ```

  函数表达式:
  ``` javascript
    let sum = function(a, b) {
      return a + b;
    };
  ```

  函数声明全局可用
  函数表达式只在声明后可用

  当一个函数声明在一个代码块内时，它在该代码块内的任何位置都是可见的。但在代码块外不可见。

  ### 代码调试

  #### Debugger 命令

    我们也可以使用 debugger 命令来暂停代码，像这样：
  ``` javascript
    function hello(name) {
      let phrase = `Hello, ${name}!`;

      debugger;  // <-- 调试器会在这停止

      say(phrase);
    }
  ```

  ### 注释

  #### 注释这些内容：

  * 整体架构，高层次的观点。

  * 函数的用法。

  * 重要的解决方案，特别是在不是很明显时。

  #### 避免注释：

  * 描述“代码如何工作”和“代码做了什么”。

  * 避免在代码已经足够简单或代码有很好的自描述性而不需要注释的情况下，还写些没必要的注释。

  ### 使用 Babel 提高兼容性

  ### 对象

  #### 通过方括号来访问对象,这时可以拼接字符串
  ``` javascript
    let i = 1;
    let person = {
      stu1: 'killy'
    }
    console.log(person[`stu${i}`]) // killy
  ```
  非常nice

  #### 计算属性

  可以动态改变键名

  ``` javascript
    let fruit = prompt('请输入水果', '苹果');
    let price = {
      [fruit]: 5
    };
    console.log(price[fruit]);
  ```

  #### 存在值检查

  两种方法:

  1. user.noSuchProperty === undefined (很好理解)

  2. "key" in object

  看看代码
  ``` javascript
    let user = { name: "John", age: 30 };
    console.log( "age" in user ); // true，user.age 存在
    console.log( "blabla" in user ); // false，user.blabla 不存在。
  ```

  for in 循环,遍历对象所有的属性
  ``` javascript
    let user = {
      name: "John",
      age: 30,
      isAdmin: true
    };
    for(let key in user) {
      // keys
      alert( key );  // name, age, isAdmin
      // 属性键的值
      alert( user[key] ); // John, 30, true
    }
  ```

  在对象中, 会对整数属性排序

  这里的“整数属性”术语指的是一个字符串，可以在不改变的情况下对整数进行转换。

  所以，“49” 是一个整数属性名，因为我们把它转换成整数，再转换回来，它还是一样。但是 “+49” 和 “1.2” 就不行了：
  ``` javascript
    // Math.trunc 是内置的去除小数部分的方法。
    alert( String(Math.trunc(Number("49"))) ); // "49"，同样，整数属性
    alert( String(Math.trunc(Number("+49"))) ); // "49"，不同于 "+49" ⇒ 不是整数属性
    alert( String(Math.trunc(Number("1.2"))) ); // "1"，不同于 "1.2" ⇒ 不是整数属性
  ```

  所以如果想用原来的顺序,需要使用 '+'
  ``` javascript
    let codes = {
      "+49": "Germany",
      "+41": "Switzerland",
      "+44": "Great Britain",
      // ..,
      "+1": "USA"
    };
    for(let code in codes) {
      alert( +code ); // 49, 41, 44, 1
    }
  ```

  对象赋值只是赋值了指向对象属性的指针, 所有如果一个指向的对象属性,发生改变所有的对象都会变化

  复制对象的方法

  object.assign(dest,[src1, src2, src3, src4...])
  尽量不要在对象里面写对象
  不然复制的时候,又要重复上面的情况

  检测数组为空的方法
  ``` javascript
  function isEmpty(obj) {
    for (let key in obj) {
      return false;
    }
    return true;
  }
  ```

  ### Symbol 类型

  声明

  ``` javascript
  let id = Symbol('id');
  let id1 = Symbol("id");
  let id2 = Symbol("id");

  console.log(id1 == id2); // false
  ```
   当输出时, Symbol 不会被隐性的转换为String.需要手动转化
  ``` javascript
    let id = Symbol("id");
    alert(id.toString()); // Symbol(id)，现在它起作用了
  ```
  1. Symbol 是唯一标识符的基本类型

  2. Symbol 使用 Symbol() 创建的，调用带有一个可选的描述。

  3. Symbol 总是不同的值，即使它们有相同的名称。如果我们希望同名 Symbol 相等，那么我们应该使用全局注册表：Symbol.for(key) 返回（如果需要的话创建）一个以 key 作为名称的全局 Symbol。Symbol.for 的多次调用完全返回相同的 Symbol。

  4. Symbol 有两个主要的使用场景：

  * “隐藏” 对象属性。如果需要将属性添加到 “属于” 另一个脚本或库的对象中，则可以创建 Symbol 并将其用作属性键。Symbol 属性不出现在 for..in中，因此不会无心列出。另外，它不会被直接访问，因为另一个脚本没有我们的符号，所以它不会不小心干预它的操作。

  * 因此我们可以使用 Symbol 属性“秘密地”将一些东西隐藏到我们需要的对象中，但其他人不会以对象属性的形式看到它。

  * JavaScript 使用了许多系统 Symbol，这些 Symbol 可以作为 Symbol.* 访问。我们可以使用它们来改变一些内置行为。例如，在本教程的后面部分，我们将使用 Symbol.iterator 来迭代，Symbol.toPrimitive 来设置对象原始值的转换等等。

  * 从技术上说，Symbol 不是 100% 隐藏的。有一个内置方法 Object.getOwnPropertySymbols(obj) 允许我们获取所有的 Symbol。还有一个名为 Reflect.ownKeys(obj) 返回所有键，包括 Symbol。所以它们不是真正的隐藏。但是大多数库、内置方法和语法结构都遵循一个共同的协议。而明确调用上述方法的人可能很清楚他在做什么。

  ### this
  this 一般指调用区域的上一级(箭头函数除外)
  ### 引用类型

  #### 不要将对象中的函数赋给其他变量或使用 = , || 等等

  调用函数的方法比较

  ``` javascript
    let obj, method;
    obj = {
      go: function() { alert(this); }
    };

    obj.go();               // (1) [object Object]

    (obj.go)();             // (2) [object Object]

    (method = obj.go)();    // (3) undefined

    (obj.go || obj.stop)(); // (4) undefined

  ```

  这里是解释。

  1. 它是一个常规的方法调用。

  2. 同样，括号没有改变执行的顺序，点总是首先执行。

  3. 这里我们有一个更复杂的 (expression).method() 调用。这个调用就像被分成了两行（代码）一样：

  f = obj.go; // calculate the expression
  f();        // call what we have
  这里的 f() 是作为一个没有（设定）this 的函数执行的。

  4. 与 (3) 相类似，在点 . 的左边也有一个表达式。

    要解释 (3) 和 (4) 的原因，我们需要回顾一下属性访问器（点或方括号）返回的值是引用类型的。

  5. 除了方法调用之外的任何操作（如赋值 = 或 || 等）把它变为了一个没有设定 this 信息的普通值。


  ### 对象的转化

  当对象在与其他变量类型进行操作时,会发生转换

  1. 调用 obj[Symbol.toPrimitive](hint) 如果这个方法存在的话，

  2. 否则如果暗示是 "string"

    尝试 obj.toString() 和 obj.valueOf()，无论哪个存在。

  3. 否则，如果暗示 "number" 或者 "default"

    尝试 obj.valueOf() 和 obj.toString()，无论哪个存在。

  ### 构造函数

  构造函数在技术上是常规函数。不过有两个约定：

  他们首先用大写字母命名。
  它们只能用 "new" 操作符来执行。
  例如：

  ``` javascript
    function User(name) {
      this.name = name;
      this.isAdmin = false;
    }

    let user = new User("Jack");

    alert(user.name); // Jack
    alert(user.isAdmin); // false
  ```

  ### 双语法构造函数：new.target
  在一个函数内部，我们可以使用 new.target 属性来检查它被调用时，是否使用了 new。

  常规调用为空，如果通过 new 调用，则等于函数：
  ``` javascript
    function User() {
      alert(new.target);
    }

    // 不带 new：
    User(); // undefined

    // 带 new：
    new User(); // function User { ... }
  ```
  这可以使 new 和常规语法的工作原理相同：
  ``` javascript
    function User(name) {
      if (!new.target) { // 如果你没有运行 new
        return new User(name); // ...会为你添加 new
      }
      this.name = name;
    }
    let john = User("John"); // 重新调用 new User
    alert(john.name); // John
  ```

  构造函数一般没有 return
  如果有 return 的话,
  两种情况:
  如果是对象默认返回对象,
  如果什么都没有返回this

## 数据类型:

### 数字:

#### 使用 e 表示很大或很小的数

#### toString(<进制>)转化为字符串,括号里面可以填需转化的进制

```
Math.floor
```

向下舍入：`3.1` 变成 `3`，`-1.1` 变成 `-2`。

```
Math.ceil
```

向上舍入：`3.1` 变成 `4`，`-1.1` 变成 `-1`。

```
Math.round
```

向最近的整数舍入：`3.1` 变成 `3`, 3.6`变成`4`，`-1.1`变成`-1`。

`Math.trunc`（IE 浏览器不支持这个方法）

删除小数点后的所有内容而不舍入：`3.1` 变成 `3`，`-1.1` 变成 `-1`。

toFixed(n) 保留 n 位小数四舍五入,注意结果是字符串

如果要精确的四舍五入,需要将数字转化为整数
``` javascript
  alert( 1.35.toFixed(1) ); // 1.4
  alert( 6.35.toFixed(1) ); // 6.3
```
isNaN 检测是否为有效有限数字类型, NaN和infinity会返回false

ParseInt 和 ParseFloat 从字符串中抽取一个数字,要读取数字,数字必须在第一位
``` javascript
  alert( parseInt('a123') ); // NaN, the first symbol stops the process
```
其实他们有第二个参数,可以规定读取数字的进制

其他数学函数

Math.random() 随机函数
Math.max()
Math.pow(n, power)

### 字符串

#### 访问:

* str.charAt(序号) 访问字符串的第几个字母,没找到返回 ''
  str[序号]没找到返回 undefined

* 用 for of 遍历字符
``` javascript
  for (let char of "Hello") {
    alert(char); // H,e,l,l,o （char 变为“H”，然后是“e”，然后是“l”等）
  }
```

#### 改变大小写

toLowerCase() 和 toUpperCase() 可以改变大小写

#### 查找字符串

str.indexOf(substr, pos)
substr 需查找的字符串
pos 开始查找的位置
返回找到位置的序号,没找到返回 -1 
``` javascript
let str = "Widget with id";

if (str.indexOf("Widget") != -1) {
    alert("We found it"); // 现在运行了！
}
if (~str.indexOf("Widget")) { // 自己别这么写,知道有就行了
    alert("We found it"); // 现在运行了！
}
```
str.includes(substr, pos)
与上相同,找到返回 true, 没找到返回 false

startsWith 和 endsWith 在开头和结尾查找

#### 截取字符串
* slice(start, end); 
start 开始截取的位置包含
end 结束截取的位置不包含
* substring(start, end);
返回之前的字符串(不支持负参数)
* substr(start, length)
返回length长度的字符串
str.localeCompare(str2) 通过该国的规范来排序字符

### 数组

声明:
``` javascript
  let arr = []; // 推荐使用
  let arr = new Array() 最好不要使用
```
pop,push 栈结构方法
shift, push 队列结构方法

pop 取出并返回数组的最后一个元素
push 在末尾添加一个元素
shift 取出并返回数组的第一个元素
unshift 添加数组的第一个元素

#### 遍历
* 通过 for 循环遍历
``` javascript
let arr = ["Apple", "Orange", "Pear"];

for (let i = 0; i < arr.length; i++) {
  alert( arr[i] );
}

```
* 通过 for of 循环遍历(不能获取序号)
```javascript
  let fruits = ["Apple", "Orange", "Plum"];
  // 迭代数组元素
  for (let fruit of fruits) {
    alert( fruit );
  }
```

* 不要使用 for in 循环

数组拷贝不要用等号
使用 object.assign(arr, arr1); 拷贝数组

通过 arr.length = 0; 置零数组(最好方法)
最大子数组的问题

数组方法

* splice(index, length, arr1, arr2); 会改变原数组,返回改变后的数组
从 index 开始, 删除length个数字, 添加 arr1, arr2

* slice(start, end)
截取start,end之间的元素(包括start,不包括end)

* concat(arr1, arr2)
连接数组

* indexOf/lastIndexOf/includes 查询数组,和字符串相同

* find/findIndex
``` javascript
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"}
];

let user = users.find(item => item.id == 1);

alert(user.name); // John
```
* filter 过滤函数
* map 批量修改函数,返回修改后的数组,原数组不改变非常强大
* sort() 排序函数
* reverse() 反转函数
* split,join 分割连接函数
* reduce() 递归函数
``` javascript
let value = arr.reduce(function(previousValue, item, index, arr) {
  // ...
}, initial);
```
previousValue 为当前遍历前一个值, 若在第一个元素,则等于 initial
其他参数与上面的遍历情况相同
 ``` javascript
  let arr = [1, 2, 3, 4, 5];

  let result = arr.reduce((sum, current) => sum + current, 0);// 求和

  alert(result); // 15
 ```
 * isArray
 ``` javascript
  alert(Array.isArray({})); // false

  alert(Array.isArray([])); // true
 ```
 * 其实 find, filter, map, sort 等 还有另一个参数 thisArg,用于设置,前面函数的 this 的指代
 ``` javascript
  arr.find(func, thisArg);
  arr.filter(func, thisArg);
  arr.map(func, thisArg);
  // ...
  // thisArg 是可选的最后一个参数
 ```
 还有其他方法:
 some / every
 fill
 copyWithin
 等等
 * [array[i], array[j]] = [array[j], array[i]]; // 交换元素
 #### Iterables (可迭代对象)
 ``` javascript
  let range = {
    from: 1,
    to: 5
  };

  // 1. 使用 for..of 将会首先调用它：
  range[Symbol.iterator] = function() {
    // 2. ...它返回一个迭代器：
    return {
      current: this.from,
      last: this.to,

      // 3. next() 将在 for..of 的每一轮循环迭代中被调用
      next() {
        // 4. 它将会返回 {done:.., value :...} 格式的对象
        if (this.current <= this.last) {
          return { done: false, value: this.current++ };
        } else {
          return { done: true };
        }
      }
    };
  };

  // 现在它可以运行了！
  for (let num of range) {
    alert(num); // 1, 然后 2, 3, 4, 5
  }
 ```

  ### map 

  new Map() – 创建一个空集合。
  map.set(key, value) – 存储含有值的键。
  map.get(key) – 根据键来返回值, 如果 key 不在 map里将会返回 undefined。
  map.has(key) – 如果 key 存在则返回 true, 否则返回 false。
  map.delete(key) – 根据键来删除值。
  map.clear() – 清空集合。
  map.size – 返回当前全部元素的数量。

  Map 迭代

  map.keys() – returns an iterable for keys,
  map.values() – returns an iterable for values,
  map.entries() – returns an iterable for entries [key, value], it’s used by default in for..of.
  ``` javascript
    let recipeMap = new Map([
      ['cucumber', 500],
      ['tomatoes', 350],
      ['onion',    50]
    ]);

    // 迭代键(vegetables)
    for (let vegetable of recipeMap.keys()) {
      alert(vegetable); // cucumber, tomatoes, onion
    }

    // 迭代值 (amounts)
    for (let amount of recipeMap.values()) {
      alert(amount); // 500, 350, 50
    }

    // 迭代 [key, value] 对
    for (let entry of recipeMap) { // 效果跟 recipeMap.entries() 相同
      alert(entry); // cucumber,500 (and so on)
    }
  ```
  也可以使用 forEach 方法
  ``` javascript
    // 对每个 (key, value) 对运行 forEach 函数
    recipeMap.forEach( (value, key, map) => {
      alert(`${key}: ${value}`); // cucumber: 500 etc
    });
  ```