# ES6 部分
### 一元运算符 +
加号可把一个字符转化为数字例如:
``` javascript
+'2' // 2
```
#### 幂运算符 ** 
``` javascript
a**b // a的b次方
```
``` javascript
console.log( null > 0 );  // (1) false
console.log( null == 0 ); // (2) false
console.log( null >= 0 ); // (3) true
```
null 在相等 == 型比较中不会被转换,在 >= 中会转换成 0
``` javascript
console.log( undefined > 0 ); // false (1)
console.log( undefined < 0 ); // false (2)
console.log( undefined == 0 ); // false (3)
```
undefined 在比较时,会被转换成 NaN

* 数字 0、空字符串 ""、null、undefined 和 NaN 都会被转换成 false。因为他们被称为 “falsy” 值。
  其他值被转换为 true，所以它们被称为 “truthy”。

* 一个或 "||" 运算的链，将返回第一个真值，如果不存在真值，就返回该链的最后一个值。
``` javascript
console.log( 1 || 0 ); // 1（1 是真值）
console.log( true || 'no matter what' ); //（true 是真值）
console.log( null || 1 ); // 1（1 是第一个真值）
console.log( null || 0 || 1 ); // 1（第一个真值）
console.log( undefined || null || 0 ); // 0（所有的转化结果都是 false，返回最后一个值）
```
* 与操作寻找第一个假值
* 两个非运算 !! 有时候用来将某个值转化为布尔类型：
* 注意: 
  禁止 break/continue 在 ‘?’ 的右边
  (i > 5) ? console.log(i) : continue; // continue 不允许在这个位置
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
  console.log('Done!');
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
      console.log( key );  // name, age, isAdmin
      // 属性键的值
      console.log( user[key] ); // John, 30, true
    }
  ```

  在对象中, 会对整数属性排序

  这里的“整数属性”术语指的是一个字符串，可以在不改变的情况下对整数进行转换。

  所以，“49” 是一个整数属性名，因为我们把它转换成整数，再转换回来，它还是一样。但是 “+49” 和 “1.2” 就不行了：
  ``` javascript
    // Math.trunc 是内置的去除小数部分的方法。
    console.log( String(Math.trunc(Number("49"))) ); // "49"，同样，整数属性
    console.log( String(Math.trunc(Number("+49"))) ); // "49"，不同于 "+49" ⇒ 不是整数属性
    console.log( String(Math.trunc(Number("1.2"))) ); // "1"，不同于 "1.2" ⇒ 不是整数属性
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
      console.log( +code ); // 49, 41, 44, 1
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
    console.log(id.toString()); // Symbol(id)，现在它起作用了
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
      go: function() { console.log(this); }
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

    console.log(user.name); // Jack
    console.log(user.isAdmin); // false
  ```

  ### 双语法构造函数：new.target
  在一个函数内部，我们可以使用 new.target 属性来检查它被调用时，是否使用了 new。

  常规调用为空，如果通过 new 调用，则等于函数：
  ``` javascript
    function User() {
      console.log(new.target);
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
    console.log(john.name); // John
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
  console.log( 1.35.toFixed(1) ); // 1.4
  console.log( 6.35.toFixed(1) ); // 6.3
```
isNaN 检测是否为有效有限数字类型, NaN和infinity会返回false

ParseInt 和 ParseFloat 从字符串中抽取一个数字,要读取数字,数字必须在第一位
``` javascript
  console.log( parseInt('a123') ); // NaN, the first symbol stops the process
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
    console.log(char); // H,e,l,l,o （char 变为“H”，然后是“e”，然后是“l”等）
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
    console.log("We found it"); // 现在运行了！
}
if (~str.indexOf("Widget")) { // 自己别这么写,知道有就行了
    console.log("We found it"); // 现在运行了！
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
  console.log( arr[i] );
}

```
* 通过 for of 循环遍历(不能获取序号)
```javascript
  let fruits = ["Apple", "Orange", "Plum"];
  // 迭代数组元素
  for (let fruit of fruits) {
    console.log( fruit );
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

console.log(user.name); // John
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

  console.log(result); // 15
 ```
 * isArray
 ``` javascript
  console.log(Array.isArray({})); // false

  console.log(Array.isArray([])); // true
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
    console.log(num); // 1, 然后 2, 3, 4, 5
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
      console.log(vegetable); // cucumber, tomatoes, onion
    }

    // 迭代值 (amounts)
    for (let amount of recipeMap.values()) {
      console.log(amount); // 500, 350, 50
    }

    // 迭代 [key, value] 对
    for (let entry of recipeMap) { // 效果跟 recipeMap.entries() 相同
      console.log(entry); // cucumber,500 (and so on)
    }
  ```
  也可以使用 forEach 方法
  ``` javascript
    // 对每个 (key, value) 对运行 forEach 函数
    recipeMap.forEach( (value, key, map) => {
      console.log(`${key}: ${value}`); // cucumber: 500 etc
    });
  ```

  将一个对象或外部的属性,赋成 null 会把他从内存清除, 所以谨慎将数据赋值为 null 
  ``` javascript
    let john = { name: "John" };

    // 该对象能被访问, john 是它的引用

    // 覆盖引用
    john = null;
  ```

  #### weakMap 
  与 map 类似,但是键名必须是对象;
  ``` javascript
  let john = { name: "John" };

  let weakMap = new WeakMap();
  weakMap.set(john, "...");

  john = null; // 覆盖引用

  // john 从内存中被移除！
  ```
  weakMap 方法只有(不能遍历)
  weakMap.get(key)
  weakMap.set(key, value)
  weakMap.delete(key)
  weakMap.has(key)
  用途:
  1. 用于为对象附加数据,当对象消失时,数据也消失
  ``` javascript
  // 附加数据
  weakMap.set(john, "secret documents");
  // 如果 john 消失, secret documents 将会被自动删除
  ```
  2. 用作数据的缓存,可以迅速删除
  ``` javascript
    // 📁 cache.js
    let cache = new WeakMap();

    // 计算并记结果
    function process(obj) {
      if (!cache.has(obj)) {
        let result = /* 计算 obj 之后得出的结果 */ obj;

        cache.set(obj, result);
      }

      return cache.get(obj);
    }

    // 📁 main.js
    let obj = {/* some object */};

    let result1 = process(obj);
    let result2 = process(obj);

    // ...之后, 当该对象不再需要的时候:
    obj = null;

    // 不能使用 cache.size, 因为它是一个 WeakMap,
    // 要么是 0 或者 很快变成 0
    // 当 obj 被回收时, 缓存的数据也会被清除
  ```
  #### weakSet 
  它跟 Set 类似, 但是我们只能添加对象到 WeakSet (非原始值)中。
  某个对象只有在其它任何地方都能访问的时候才能留在 set 里。
  跟 Set 一样, WeakSet 支持 add, has and delete 等方法, 但不支持 size, keys() 并且没有迭代。 变 “弱” 的同时, 它也可以作为额外的存储空间，但并非任意数据，而是针对“是/否”的事实，在 WeakSet 里的成员代表着对象里的某个属性。 例如, 我们可以添加 users 到 WeakSet 里来追踪谁访问了我们的网站：
  ``` javascript
  let visitedSet = new WeakSet();

  let john = { name: "John" };
  let pete = { name: "Pete" };
  let mary = { name: "Mary" };

  visitedSet.add(john); // John visited us
  visitedSet.add(pete); // Then Pete
  visitedSet.add(john); // John again

  // 现在 visitedSet 有2个用户

  // 检查 John 是否访问过?
  console.log(visitedSet.has(john)); // true

  // 检查 Mary 是否访问过?
  console.log(visitedSet.has(mary)); // false

  john = null;

  // visitedSet 将被自动清理
  ```

  ### Object.keys/values/entries 忽略 Symbol 类型的属性
  就像 for..in 循环，这些方法会忽略使用 Symbol(...) 作为键的属性。

  通常这很方便。但是如果我们也想要获得 Symbol 类型的键，那么有另外不同的方法 Object.getOwnPropertySymbols， 它会返回一个只包含 Symbol 类型的键的数组。同样，Reflect.ownKeys(obj) 方法会返回「所有」键。

  ### 可以通过数组解构赋值

  ``` javascript
  // 有一个存放了名字和姓氏的数组
  let arr = ["Ilya", "Kantor"]

  // 解构赋值
  let [firstName, surname] = arr;

  console.log(firstName); // Ilya
  console.log(surname);  // Kantor
  ```
  通过 ... 将剩余元素收集起来
  ``` javascript
  let [name1, name2, ...rest] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];

  console.log(name1); // Julius
  console.log(name2); // Caesar

  console.log(rest[0]); // Consul
  console.log(rest[1]); // of the Roman Republic
  console.log(rest.length); // 2
  ```

  为值设置默认值
  ``` javascript
  // 默认值
  let [name = "Guest", surname = "Anonymous"] = ["Julius"];

  console.log(name);    // Julius (来自数组的值)
  console.log(surname); // Anonymous (默认值被使用了)
  ```

  通过向函数传递对象来作为函数参数,来实现使用默认值, 精简参数的效果
  ``` javascript
  let options = {
    title: "My menu",
    items: ["Item1", "Item2"]
  };

  function showMenu({
    title = "Untitled",
    width: w = 100,  // width 赋值给 w
    height: h = 200, // height 赋值给 h
    items: [item1, item2] // items 第一个元素赋值给 item1, 第二个元素赋值给 item2
  }) {
    console.log( `${title} ${w} ${h}` ); // My Menu 100 200
    console.log( item1 ); // Item1
    console.log( item2 ); // Item2
  }

  showMenu(options);
  ```

  ### js 日期对象
  #### 创建一个现在时间的日期对象
  new Date()
  ``` javascript
  let now = new Date();
  console.log( now ); // 显示当前的日期/时间
  ```
  #### 创建一个指定日期对象
  new Date(milliseconds)
  参数是从 1970-01-01 00:00:00 UTC+0 开始所经过的毫秒（一秒的千分之一）数。
  传入的参数是自 1970-01-01 00:00:00 开始计算的毫秒数，被称为时间戳。
  new Date(datestring)
  如果只有一个参数，并且是字符串，那么该参数会通过 Date.parse 算法解析（下面会提到）。
  new Date(year, month, date, hours, minutes, seconds, ms)
  创建一个 Date 对象，参数是当地时区的日期组合信息。只有前两个参数是必须的。
  #### 获取方法:
  * getFullYear() 获取年份（4 位数）(不要使用getYear())
  * getMonth() 获取月份从 0 到 11。
  * getDate() 获取当月的日期，从 1 到 31，这个方法名称可能看起来有些令人疑惑。
  * getHours(), getMinutes(), getSeconds(), getMilliseconds()
    获取相应的时间信息。
  * getDay()
    获取一周中的第几天，从 0（星期天）到 6 （星期六）。第一天始终是星期天，在某些国家可能不是这样的习惯，但是这不能被改变。
  * getTime() 返回时间戳
    getTimezoneOffset()
    返回时区偏移数，以分钟为单位：

  // 如果你在时区 UTC-1，输出 60
  // 如果你在时区 UTC+3，输出 -180
  console.log( new Date().getTimezoneOffset() );
  #### 设置方法:
  * setFullYear(year [, month, date])
  * setMonth(month [, date])
  * setDate(date)
  * setHours(hour [, min, sec, ms])
  * setMinutes(min [, sec, ms])
  * setSeconds(sec [, ms])
  * setMilliseconds(ms)
  * setTime(milliseconds) （使用自 1970-01-01 00:00:00 UTC+0 开始的毫秒数来设置整个日期对象）
    以上方法除了 setTime() 都有 UTC 版本，比如 setUTCHours()。
  #### 自动校准
  假设我们要在日期「2016 年 2 月 28 日」上再加 2 天。结果可能是「3 月 2 日」或者「3 月 1 日」，原因是闰年的存在。但是我们不需要去考虑这些，直接加两天，剩下的 Date 对象会帮我们处理：
  #### Date.now()
  如果我们仅仅想要度量时间间隔，我们不需要整个 Date 对象。

  有一个特殊的方法 Date.now()，它会返回当前的时间戳。
  Date.parse(str) 方法可以从一个字符串中读取日期。

  字符串的格式是：YYYY-MM-DDTHH:mm:ss.sssZ，其中：

  YYYY-MM-DD —— 日期：年-月-日。
  字符串 "T" 是一个分隔符。
  HH:mm:ss.sss —— 时间：小时，分钟，秒，毫秒。
  可选字符 'Z' 代表时区。单个字符 Z 代表 UTC+0。
  简短形式也是可以的，比如 YYYY-MM-DD 或者 YYYY-MM 又或者 YYYY。

  Date.parse(str) 方法会转化一个特定格式的字符串，返回一个时间戳（自 1970-01-01 00:00:00 起的毫秒数），如果格式不正确，返回 NaN。

  JSON.stringify 将对象转换为 JSON。
  JSON.parse 将 JSON 转换回对象。
  如果有日期对象必须使用下述方法,否则会报错
  ``` javascript
  let str = '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';

  let meetup = JSON.parse(str, function(key, value) {
    if (key == 'date') return new Date(value);
    return value;
  });

  console.log( meetup.date.getDate() ); // now works!
  ```

  通过 ... 传入多个参数
  我们也可以显式地定义和取用前面部分的参数，而把后面部分的参数收集起来。

  下面的例子即把前两个参数定义为变量，同时把剩余的参数收集到 titles 数组中：
  ``` javascript
  function showName(firstName, lastName, ...titles) {
    console.log( firstName + ' ' + lastName ); // Julius Caesar

    // titles 数组中包含了剩余的参数
    // 也就是有 titles = ["Consul", "Imperator"]
    console.log( titles[0] ); // Consul
    console.log( titles[1] ); // Imperator
    console.log( titles.length ); // 2
  }

  showName("Julius", "Caesar", "Consul", "Imperator");
  ```
  ... 的参数必须放在末尾

  展开操作符
  ``` javascript
  let arr = [3, 5, 1];

  console.log( Math.max(...arr) ); // 5（Spread 操作符把数组转为参数列表）
  ```
  可用于 splice 第三个参数的传入

  ### 闭包
  #### 闭包的结果与C语言的 static 的相似
   函数使用外部变量,并保存处理的结果以便下一次调用使用
   ``` javascript
   // 闭包
    function makeCounter () {
      let count = 0;
      return function () {
        return count++;
      }
    }
    let counter1 = makeCounter();
    let counter2 = makeCounter();
    console.log(counter1()); // 0
    console.log(counter1()); // 1
    console.log(counter2()); // 0
    // 闭包的结果与C语言的 static 的相似
   ```

   能产生闭包效果的结构(为了产生闭包效果,不要使用 var 定义变量)

   * if {}
   * for {}
   * { }

   ### IIFE (立即执行函数)
   ``` javascript
   // 方式一:
   (function () {
     let message = 'hello';
     console.log(message); // hello 
   })();
   // 方式二:
   (function () {
     let message = 'hello';
     console.log(message); // hello 
   }());
   // 方式三:
   !function () {
     let message = 'hello';
     console.log(message); // hello 
   }
   // 方式四:
   +function () {
     let message = 'hello';
     console.log(message); // hello 
   }
   ```

   注意: 闭包的变量 v8 引擎是无法追踪的
   #### 
   双括号函数
  ``` javascript
   sum(1)(2);
   function sum (a) {
     return function (b) {
       return a + b;
     }
   }
  ```

  for 循环 和 while 循环的区别

  for 循环每次循环时, 操作的是不同的变量
  while 循环操作的是相同的变量
  while 循环
  ``` javascript
  function makeArmy() {
    let shooters = [];

    let i = 0;
    while (i < 10) {
      let shooter = function() { // shooter 函数
        console.log( i ); // 应该显示它自己的数字
      };
      shooters.push(shooter);
      i++;
    }

    return shooters;
  }

  let army = makeArmy();

  army[0](); // 第 0 号 shooter 显示 10
  army[5](); // 第 5 号也输出 10...
  // ... 所有的 shooters 都显示 10 而不是它们的 0, 1, 2, 3...
  ```
  for 循环
  ``` javascript
    function makeArmy() {

      let shooters = [];

      for(let i = 0; i < 10; i++) {
        let shooter = function() { // shooter 函数
          console.log( i ); // 应该显示它自己的数字
        };
        shooters.push(shooter);
      }

      return shooters;
    }

    let army = makeArmy();

    army[0](); // 0
    army[5](); // 5
  ```

  旧时的 var 

  var 没有块级作用域

  var 穿透了 if、for 或其它块级代码。这是因为在早期的 JavaScript 里，块没有词法环境。而 var 就是对它的一个回忆。
  ``` javascript
  if (true) {
    var test = true; // 用 "var" 而不是 "let"
  }

  console.log(test); // true，变量在 if 结束后仍存在
  for (var i = 0; i < 10; i++) {
    // ...
  }

  console.log(i); // 10, "i" 在循环结束后仍然可见，它会成为一个全局变量
  ```
  如果 用 let 你是打死都不能访问的
  变量提升
  注意变量提升,只能提升声明,不能提升赋值
  ``` javascript
  function sayHi() {
    phrase = "Hello"; // (*)

    if (false) {
      var phrase;
    }

    console.log(phrase);
  }
  ```

  ### 全局对象

  window 对所有脚本可见,可以设置全局变量,不过肯定不标准.(可以使用)
  使用模块化引入
  所有的script的 最顶端的 this 就是 window , 可以通过设置
  type = 'module' 使代码块最顶端的 this 为 undefined 防止互相干扰

  ### 函数对象

  name
  ``` javascript
  function sayHi() {
    console.log("Hi");
  }

  console.log(sayHi.name); // sayHi
  ```
  length(不包含余参)
  ``` javascript
  function f1(a) {}
  function f2(a, b) {}
  function many(a, b, ...more) {}
  console.log(f1.length); // 1
  console.log(f2.length); // 2
  console.log(many.length); // 2
  ```

  自定义属性
  ``` javascript
  function sayHi() {
    sayHi.counter = 0; // 初始值
    console.log("Hi");
    // 我们记录一下运行次数
    sayHi.counter++;
  }
  sayHi();
  console.log('counter =' + sayHi.counter);
  ```
  可以用于实现和闭包完全相同的效果
  区别 闭包变量在外部完全不能访问,函数属性可以访问但是绝对不会有变量冲突

  命名函数表达式 (NFE)

  ``` javascript
    let sayHi = function (who) {
      console.log(`hello, ${who}`);
    }
    加名字
    let sayHi = function func (who) {
      console.log(`hello, ${who}`);
    }
  ```
  特点: 
  * func 在函数外不可见;
  * func 可用于函数内部调用,递归函数;(牛逼)

  通过 new Function () 创建函数
  特点: 
  在闭包中指向全局的语法,而不是函数内部的
  ``` javascript
  let sum = new Function('a', 'b', 'return a + b');

  console.log( sum(1, 2) ); // 3
  function getFunc() {
    let value = "test";

    let func = new Function('console.log(value)');

    return func;
  }

  getFunc()(); // error：value 未定义
  ```

  call() apply()
  call(context, arg1, arg2 ,arg3);
  context 是内部函数 this 的指向
  后面为参数
  apply(context, arg);
  后面的参数为一数组
  函数缓存:
  通过给一些难以计算并且重复性,很高的工作,提供缓存,当遇到该值时,先查看缓存有没有,若没有再计算,提高效率
  ``` javascript
  
  let worker = {
    slow(min, max) {
      console.log(`Called with ${min},${max}`);
      return min + max;
    }
  };

  function cachingDecorator(func, hash) {
    let cache = new Map();
    return function() {
      let key = hash(arguments); // (*)
      if (cache.has(key)) {
        return cache.get(key);
      }

      let result = func.apply(this, arguments); // (**)

      cache.set(key, result);
      return result;
    };
  }

  function hash(args) {
    return [].join.call(arguments);
  }

  worker.slow = cachingDecorator(worker.slow, hash);

  console.log( worker.slow(3, 5) ); // works
  console.log( "Again " + worker.slow(3, 5) ); // same (cached)
  ```
  ### 丢失 this 
  浏览器中的方法 setTimeout 有些特殊：它为函数的调用设定了 this=window
  好像是,上下文的 this 丢失
  解决方案 1: 包装层
  ``` javascript
  let user = {
    firstName: "John",
    sayHi() {
      console.log(`Hello, ${this.firstName}!`);
    }
  };

  setTimeout(function() {
    user.sayHi(); // Hello, John!
  }, 1000);
  ```
  解决方案 2: bind() 函数
  获取函数固定 this 的版本
  ``` javascript
  let user = {
    firstName: "John"
  };

  function func(phrase) {
    console.log(phrase + ', ' + this.firstName);
  }

  // 将 this 绑定给 user
  let funcUser = func.bind(user);

  funcUser("Hello"); // Hello, John（参数 "Hello" 被传递了，并且 this=user）
  ```
  ### 对象属性的标志

  对象属性有三个特殊的属性

  writable 可读性
  enumerable 可枚举性
  configurable 可删除性

  通过
  Object.getOwnPropertyDescriptor(obj, propertyName);
  获取属性的特殊属性
  通过
  Object.defineProperty(obj, propertyName, descriptor)
  修改属性
  将 user.name 设置为只读的
  ``` javascript
  let user = {
    name: "John"
  };

  Object.defineProperty(user, "name", {
    writable: false
  });

  user.name = "Pete"; // 错误：不能设置只读属性'name'...
  ```

  Object.defineProperties(obj, descriptors) 允许修改多个属性
  ``` javascript
  Object.defineProperties(user, {
    name: { value: "John", writable: false },
    surname: { value: "Smith", writable: false },
    // ...
  });
  ```
  还可以设置全局的封闭对象
  属性描述符可以在各个属性的级别上工作。
  还有一些限制访问整个对象的方法：
  Object.preventExtensions(obj)
  禁止向对象添加属性。
  Object.seal(obj)
  禁止添加/删除属性，为所有现有的属性设置 configurable: false。
  Object.freeze(obj)
  禁止添加/删除/更改属性，为所有现有属性设置 configurable: false, writable: false。
  还有对他们的测试：
  Object.isExtensible(obj)
  如果添加属性被禁止，则返回 false，否则返回 true。
  Object.isSealed(obj)
  如果禁止添加/删除属性，则返回 true，并且所有现有属性都具有 configurable: false。
  Object.isFrozen(obj)
  如果禁止添加/删除/更改属性，并且所有当前属性都是 configurable: false, writable: false，则返回 true。
  这些方法在实践中很少使用。

  ### 通过 _proto_ 继承
  ``` javascript
  let user = {
    name: "John",
    surname: "Smith",

    set fullName(value) {
      [this.name, this.surname] = value.split(" ");
    },

    get fullName() {
      return `${this.name} ${this.surname}`;
    }
  };

  let admin = {
    __proto__: user,
    isAdmin: true
  };

  console.log(admin.fullName); // John Smith (*)

  // setter triggers!
  admin.fullName = "Alice Cooper"; // (**)
  ```

  ### 函数原型 new Function()
  通过 prototype 继承
  ``` javascript
  let animal = {
    eats: true
  };

  function Rabbit(name) {
    this.name = name;
  }

  Rabbit.prototype = animal;

  let rabbit = new Rabbit("White Rabbit"); //  rabbit.__proto__ == animal

  console.log( rabbit.eats ); // true
  ```
  ### 对象
  #### 基本语法
  ``` javascript
    class MyClass {
      prop = value; // field

      constructor(...) { // 构造器
        // ...
      }

      method(...) {} // 方法

      get something(...) {} // getter 方法
      set something(...) {} // setter 方法

      [Symbol.iterator]() {} // 计算 name/symbol 名方法
      // ...
    }
    // 示例
    class User {
      constructor (name) {
        this.name = name;
        this.sex = sex;
      }
      sayHi () {
        console.log(`大家好, 我是 ${ this.name }`);
      }
    }
    let newUser = new User('小埋');
    newUser.sayHi(); // 大家好, 我是 小埋
    console.log(newUser.sex); // 妹子
  ```
  #### 本质
  ``` javascript
  console.log(typeof User); // function
  class User {
    constructor(name) { this.name = name; }
    sayHi() { console.log(this.name); }
  }
  // 类是函数
  console.log(typeof User); // function

  // ...或者，更确切地说是构造方法
  console.log(User === User.prototype.constructor); // true

  // User.prototype 中的方法，比如：
  console.log(User.prototype.sayHi); // console.log(this.name);

  // 实际上在原型中有两个方法
  console.log(Object.getOwnPropertyNames(User.prototype)); // constructor, sayHi
  ```
  #### 语法糖
  使用 构造函数重写 User 类
  ``` javascript
  // 1. 创建构造器函数
  function User(name) {
    this.name = name;
  }
  // 任何函数原型默认具有构造器属性，
  // 所以，我们不需要创建它

  // 2. 向原型中添加方法
  User.prototype.sayHi = function() {
    console.log(this.name);
  };

  // 使用方法：
  let user = new User("John");
  user.sayHi();
  ```

  类方法不可枚举

  #### 类方法 Getters/setters
  ``` javascript
  class User {

    constructor(name) {
      // 调用 setter
      this.name = name;
    }

    get name() {
      return this._name;
    }

    set name(value) {
      if (value.length < 4) {
        console.log("Name is too short.");
        return;
      }
      this._name = value;
    }

  }

  let user = new User("John");
  console.log(user.name); // John

  user = new User(""); // Name too short.
  ```
  ### 类继承
  ``` javascript
  class Animal {
    constructor(name) {
      this.speed = 0;
      this.name = name;
    }
    run(speed) {
      this.speed += speed;
      console.log(`${this.name} runs with speed ${this.speed}.`);
    }
    stop() {
      this.speed = 0;
      console.log(`${this.name} stopped.`);
    }
  }

  // 通过指定“extends Animal”让 Rabbit 继承自 Animal
  class Rabbit extends Animal {
    hide() {
      console.log(`${this.name} hides!`);
    }
  }

  let rabbit = new Rabbit("White Rabbit");

  rabbit.run(5); // White Rabbit runs with speed 5.
  rabbit.hide(); // White Rabbit hides!
  ```
  #### extends允许接任何表达式

  #### 增写方法
  但是通常来说，我们不希望完全替换父类的方法，而是希望基于它做一些调整或者功能性的扩展。我们在我们的方法中做一些事情，但是在它之前/之后或在执行过程中调用父类方法。

  为此，类提供了 "super" 关键字。

  执行 super.method(...) 调用父类方法。
  执行 super(...) 调用父类构造函数（只能在子类的构造函数中运行）。
  例如，让我们的兔子在停下来的时候自动隐藏：
  ``` javascript
  class Animal {

    constructor(name) {
      this.speed = 0;
      this.name = name;
    }

    run(speed) {
      this.speed += speed;
      console.log(`${this.name} runs with speed ${this.speed}.`);
    }

    stop() {
      this.speed = 0;
      console.log(`${this.name} stopped.`);
    }

  }

  class Rabbit extends Animal {
    hide() {
      console.log(`${this.name} hides!`);
    }

    stop() {
      super.stop(); // 调用父类的 stop 函数
      this.hide(); // 然后隐藏
    }
  }

  let rabbit = new Rabbit("White Rabbit");

  rabbit.run(5); // White Rabbit runs with speed 5.
  rabbit.stop(); // White Rabbit stopped. White rabbit hides!
  ```

  * 注意箭头函数没有 super
    继承 方法和 数据都要声明
  ``` javascript
  class Animal {

    constructor(name) {
      this.speed = 0;
      this.name = name;
    }

    // ...
  }

  class Rabbit extends Animal {

    constructor(name, earLength) {
      super(name);
      this.earLength = earLength;
    }

    // ...
  }

  // 现在可以了
  let rabbit = new Rabbit("White Rabbit", 10);
  console.log(rabbit.name); // White Rabbit
  console.log(rabbit.earLength); // 10
  ```

  静态声明 前面加 static ,且继承什么都不用做

  ### 受保护属性和私有属性
  通过设置 get,set 函数,控制数据的访问,比如只写get,不写set函数,让数据只能读.
  注意受保护数据默认前面加 _
  ``` javascript
  class CoffeeMachine {
    _waterAmount = 0;

    set waterAmount(value) {
      if (value < 0) throw new Error("Negative water");
      this._waterAmount = value;
    }

    get waterAmount() {
      return this._waterAmount;
    }

    constructor(power) {
      this._power = power;
    }

  }

  // 创建咖啡机
  let coffeeMachine = new CoffeeMachine(100);

  // 加入水
  coffeeMachine.waterAmount = -10; // Error: Negative water
  ```
  数据只读
  ``` javascript
  class CoffeeMachine {
    // ...

    constructor(power) {
      this._power = power;
    }

    get power() {
      return this._power;
    }

  }

  // 创建咖啡机
  let coffeeMachine = new CoffeeMachine(100);

  console.log(`Power is: ${coffeeMachine.power}W`); // 功率是：100W

  coffeeMachine.power = 25; // Error (no setter)
  ```
  私有字段 #开头
  ``` javascript
  class CoffeeMachine {

    #waterAmount = 0;

    get waterAmount() {
      return this.#waterAmount;
    }

    set waterAmount(value) {
      if (value < 0) throw new Error("Negative water");
      this.#waterAmount = value;
    }
  }

  let machine = new CoffeeMachine();

  machine.waterAmount = 100;
  console.log(machine.#waterAmount); // Error
  ```
  如果继承必须使用 get, set方法操作变量
  ### 继承内置类
  ``` javascript
  // 给 PowerArray 新增了一个方法（可以增加更多）
  class PowerArray extends Array {
    isEmpty() {
      return this.length === 0;
    }
  }

  let arr = new PowerArray(1, 2, 5, 10, 50);
  console.log(arr.isEmpty()); // false

  let filteredArr = arr.filter(item => item >= 10);
  console.log(filteredArr); // 10, 50
  console.log(filteredArr.isEmpty()); // false
  ```
  如果希望返回常规的数组,则需要
  ``` javascript
  class PowerArray extends Array {
    isEmpty() {
      return this.length === 0;
    }

    // 内置方法会使用这个作为构造函数 (constructor)
    static get [Symbol.species]() {
      return Array;
    }
  }

  let arr = new PowerArray(1, 2, 5, 10, 50);
  console.log(arr.isEmpty()); // false

  // filter 使用 arr.constructor[Symbol.species] 作为构造函数 (constructor) 创建新数组
  let filteredArr = arr.filter(item => item >= 10);

  // filteredArr 不是 PowerArray, 而是 Array
  console.log(filteredArr.isEmpty()); // Error: filteredArr.isEmpty is not a function
  ```
  instanceof
  用法：

  obj instanceof Class
  如果 obj 隶属于 Class 类（或者是 Class 类的衍生类），表达式将返回 true。
  * 在 JavaScript 中，我们只能继承单个对象。每个对象只能有一个 [[Prototype]] 原型。并且每个类只可以扩展另外一个类。

  js Mixin 模式

  例如，这个叫做 sayHiMixin 的 mixin 用于给 User 添加一些“言语”。
  ``` javascript
  // mixin
  let sayHiMixin = {
    sayHi() {
      console.log(`Hello ${this.name}`);
    },
    sayBye() {
      console.log(`Bye ${this.name}`);
    }
  };

  // 用法：
  class User {
    constructor(name) {
      this.name = name;
    }
  }

  // 拷贝方法
  Object.assign(User.prototype, sayHiMixin);

  // 现在 User 可以说　hi 了
  new User("Dude").sayHi(); // Hello Dude!
  ```
  ### 错误处理
  ``` javascript
  try {
    // 执行此处代码
  } catch(err) {
    // 如果发生异常，跳到这里
    // err 是一个异常对象
  } finally {
    // 不管 try/catch 怎样都会执行
  }
  ```

  err 的属性
  message
  name
  stack

  ### 回调
  js 有很多的异步函数
  ``` javascript
  function loadScript(src) {
    let script = document.createElement('script');
    script.src = src;
    document.head.append(script);
  }
  ```
  为了能在加载后,再调用里面的函数 需要有 callback 函数
  ``` javascript
  function loadScript(src, callback) {
    let script = document.createElement('script');
    script.src = src;

    script.onload = () => callback(script);

    document.head.append(script);
  }
  ```
  为了让函数执行,应该如此调用
  ``` javascript
  loadScript('/my/script.js', function() {
    // 在脚本被加载后，回调才会被运行
    newFunction(); // 现在起作用了
    ...
  });
  ```
  但是为了防止错误,需要加入错误处理
  ``` javascript
  function loadScript(src, callback) {
    let script = document.createElement('script');
    script.src = src;

    script.onload = () => callback(null, script);
    script.onerror = () => callback(new Error(`Script load error for ${src}`));

    document.head.append(script);
  }
  ```
  用法
  ``` javascript
  loadScript('/my/script.js', function(error, script) {
    if (error) {
      // handle error
    } else {
      // 成功加载脚本
    }
  });
  ```

  ### promise
  ``` javascript
  let promise = new Promise(function(resolve, reject) {
    // executor (生产者代码，"singer")
  });
  promise.then( // 成功后执行函数
    function(result) { /* handle a successful result */ },
    function(error) { /* handle an error */ }
  );
  promise.catch(console.log); // 失败后执行函数
  ```
  用 promise 重写 loadScript
  ``` javascript
  function loadScript(src) {
    return new Promise(function(resolve, reject) {
      let script = document.createElement('script');
      script.src = src;

      script.onload = () => resolve(script);
      script.onerror = () => reject(new Error("Script load error: " + src));

      document.head.append(script);
    });
  }
  // 用法
  let promise = loadScript("https://cdnjs.cloudflare.com/ajax/libs/lodash.js/3.2.0/lodash.js");

  promise.then(
    script => console.log(`${script.src} is loaded!`),
    error => console.log(`Error: ${error.message}`)
  );

  promise.then(script => console.log('One more handler to do something else!'));
  ```
  ### promise 链
  ``` javascript
  new Promise(function(resolve, reject) {

    setTimeout(() => resolve(1), 1000); // (*)

  }).then(function(result) { // (**)

    console.log(result); // 1
    return result * 2;

  }).then(function(result) { // (***)

    console.log(result); // 2
    return result * 2;

  }).then(function(result) {

    console.log(result); // 4
    return result * 2;

  });
  ```

  ### 继续 loadScript 按顺序加载脚本
  ``` javascript
  loadScript("/article/promise-chaining/one.js")
    .then(function(script) {
      return loadScript("/article/promise-chaining/two.js");
    })
    .then(function(script) {
      return loadScript("/article/promise-chaining/three.js");
    })
    .then(function(script) {
      // 使用脚本里声明的函数来表明它们的确被加载了

      one();
      two();
      three();
    });
  ```
  #### Promise.all
  假设我想要并行执行多个 promise，并等待所有 promise 准备就绪。

  例如，并行下载几个 URL 并等到所有内容都下载完毕后才开始处理它们。

  这就是 Promise.all 的用途：

  语法：
  ``` javascript
  let promise = Promise.all([...promises...]);
  Promise.all([
    new Promise(resolve => setTimeout(() => resolve(1), 3000)), // 1
    new Promise(resolve => setTimeout(() => resolve(2), 2000)), // 2
    new Promise(resolve => setTimeout(() => resolve(3), 1000))  // 3
  ]).then(console.log); // 1,2,3 当 promise 就绪：每一个 promise 即成为数组中的一员
  ```
  #### Promise.allSettled
  等待所有的 promise 都被处理：即使其中一个 reject，它仍然会等待其他的 promise。处理完成后
  ``` javascript
  Promise.all([
    fetch('/template.html'),
    fetch('/style.css'),
    fetch('/data.json')
  ]).then(render); // render 方法需要上面所有数据
  ```
  #### Promise.race
  与 Promise.all 类似，它接受一个可迭代的 promise 集合，但是它只等待第一个完成（或者 error）而不会等待所有都完成，然后继续执行。

  Promise 的 任务队列
  当一个 promise 准备就绪时，它的 .then/catch/finally 处理程序就被放入队列中。但是不会立即被执行。当 JavaScript 引擎执行完当前的代码，它会从队列中获取任务并执行它。
  ### Async 关键字
  ``` javascript
  async function f() {
    return 1;
  }

  f().then(console.log); // 1
  ```
  在函数前面的「async」这个单词表达了一个简单的事情：即这个函数总是返回一个 promise。即使这个函数实际上会返回一个非 promise 的值，函数定义前加上了「async」关键字会指示 JavaScript 引擎自动将返回值包装在一个已决议（resolved）的 promise 内。
  ### Await 关键字
  关键字 await 让 JavaScript 引擎等待直到 promise 完成并返回结果。
  ``` javascript
  async function f() {

    let promise = new Promise((resolve, reject) => {
      setTimeout(() => resolve("done!"), 1000)
    });

    let result = await promise; // 等待直到 promise 决议 (*)

    console.log(result); // "done!"
  }

  f();
  ```
  修改之前的 showAvatar()
  ``` javascript
  async function showAvatar() {

    // 读取 JSON
    let response = await fetch('/article/promise-chaining/user.json');
    let user = await response.json();

    // 读取 github 用户信息
    let githubResponse = await fetch(`https://api.github.com/users/${user.name}`);
    let githubUser = await githubResponse.json();

    // 显示头像
    let img = document.createElement('img');
    img.src = githubUser.avatar_url;
    img.className = "promise-avatar-example";
    document.body.append(img);

    // 等待 3 秒
    await new Promise((resolve, reject) => setTimeout(resolve, 3000));

    img.remove();

    return githubUser;
  }

  showAvatar();
  ```
  ### generator 构造函数
  ``` javascript
  function* gererateSequence() {
    yield 1;
    yield 2;
    yield 3;
    return 4;
  }
  
  let generator = generateSequence();

  let one = generator.next();

  console.log(JSON.stringify(one)); 
  // {value: 1, done: false}
  ```
  generator 函数通过 next() 执行到 yield ,再次 next() 执行到下一个 yield
  next(),会返回一个对象 有 value 和 done 属性
  value 是 yield 后面的值, done 是是否为最后一个部分,执行到最后一部分为 true,其他为 false
  可以通过 for of 循环逐项获取, 但是return不能获取,故最后一位为也应该为 yield
  ``` javascript
  function* generateSequence() {
    yield 1;
    yield 2;
    yield 3;
  }

  let generator = generateSequence();

  for(let value of generator) {
    console.log(value); // 1, then 2
  }
  ```
  生成可迭代序列
  ``` javascript
  function* generateSequence(start, end) {
    for (let i = start; i <= end; i++) {
      yield i;
    }
  }

  let sequence = [...generateSequence(1,5)];

  console.log(sequence); // 1, 2, 3, 4, 5
  ```
  #### Generator 组合(composition)
  ``` javascript
  function* generateSequence(start, end) {
    for (let i = start; i <= end; i++) yield i;
  }

  function* generatePasswordCodes() {

    // 0..9
    yield* generateSequence(48, 57);

    // A..Z
    yield* generateSequence(65, 90);

    // a..z
    yield* generateSequence(97, 122);

  }

  let str = '';

  for(let code of generatePasswordCodes()) {
    str += String.fromCharCode(code);
  }

  console.log(str); // 0..9A..Za..z
  ```
  #### 'yield' 双向路径
  ``` javascript
  function* gen() {
    // 向外部代码传递一个问题，然后等待答案
    let result = yield "2 + 2?"; // (*)

    console.log(result);
  }

  let generator = gen();

  let question = generator.next().value; // <-- yield 返回结果

  generator.next(4); // --> 向 generator 传入结果
  ```
  头大(用的时候再看)
  ### 模块化
  export 关键字表示在当前模块之外可以访问的变量和功能。
  import 关键字允许从其他模块中导入一些诸如函数之类的功能等等。
  ``` javascript
  // 📁 sayHi.js (导出模块)
  export function sayHi(user) {
    console.log(`Hello, ${user}!`);
  }
  // 📁 main.js (导入模块)
  import {sayHi} from './sayHi.js';

  console.log(sayHi); // function...
  sayHi('John'); // Hello, John!
  ```
  通过设置 <script> 标签的 type = module 来使该部分成为模块
  如果 导出模块的内容,发生改变,则其他导入模块的文件,获得的内容也会被修改
  内联脚本和外部脚本都允许使用 <script async type="module"> 属性，当导入的模块被处理时，异步脚本会立即运行，与其他的脚本或者 HTML 文档无关。
  注意:
  * 路径前必须有东西
  ``` javascript
  import {sayHi} from 'sayHi'
  错误 需要改为 './sayHi'
  ```
  #### 使用 import * as <obj> 来导入文件的所有内容
  ``` javascript
  / 📁 main.js
  import * as say from './say.js';

  say.sayHi('John');
  say.sayBye('John');
  ```
  #### import as 导入为
  ``` javascript
  // 📁 main.js
  import {sayHi as hi, sayBye as bye} from './say.js';

  hi('John'); // Hello, John!
  bye('John'); // Bye, John!
  ```
  #### export as 导出为
  ``` javascript
  // 📁 say.js
  ...
  export {sayHi as hi, sayBye as bye};
  ```
  #### 默认导入 export default
  ``` javascript
  // 📁 user.js
  export default class User { // 只要添加“default”即可
    constructor(name) {
      this.name = name;
    }
  }
  // 📁 main.js
  import User from './user.js'; // 不需要花括号 {User}, 仅仅是 User 就可以了

  new User('John');
  ```
  * 注意一个文件只能导出一次
    default 别名
  ``` javascript
  function sayHi(user) {
    console.log(`Hello, ${user}!`);
  }

  export {sayHi as default}; // 和我们在函数前添加“export default”一样
  ```
  重新导出
  ``` javascript
  // 📁 auth/index.js
  export {login, logout} from './helpers.js';
  // 或者，为了重新导出所有的 helpers 内容，我们可以使用：
  // export * from './helpers.js';

  export {default as User} from './user.js';

  export {default as Github} from './providers/github.js';
  ...
  ```
  ### 动态导入
  ``` javascript
  let modulePath = prompt("Module path?");

  import(modulePath)
    .then(obj => <module object>)
    .catch(err => <loading error, no such module?>)
  <script>
  async function load() {
    let say = await import('./say.js');
    say.hi(); // Hello!
    say.bye(); // Bye!
    say.default(); // Module loaded (export default)!
  }
</script>
<button onclick="load()">Click me</button>
  ```

  ### Proxy Reflect
  Proxy 包装器
  get 实例 制作一个翻译器,有翻译返回翻译,没有翻译返回原文字
  ``` javascript
  let dictionary = {
    'Hello': 'Hola',
    'Bye': 'Adiós'
  };

  dictionary = new Proxy(dictionary, {
    get(target, phrase) { // 拦截读取属性操作
      if (phrase in target) { //如果字典包含该短语
        return target[phrase]; // 返回译文
      } else {
        // 否则返回未翻译的短语
        return phrase;
      }
    }
  });

  // 在字典中查找任意短语！
  // 最坏的情况也只是它们没有被翻译。
  console.log( dictionary['Hello'] ); // Hola
  console.log( dictionary['Welcome to Proxy']); // Welcome to Proxy
  ```
  set 实例 数字数组
  ``` javascript
  let numbers = [];

  numbers = new Proxy(numbers, { // (*)
    set(target, prop, val) { // 拦截写入操作
      if (typeof val == 'number') {
        target[prop] = val;
        return true;
      } else {
        return false;
      }
    }
  });

  numbers.push(1); // 添加成功
  numbers.push(2); // 添加成功
  console.log("Length is: " + numbers.length); // 2

  numbers.push("test"); // TypeError （proxy 的 `set` 操作返回 false）

  console.log("This line is never reached (error in the line above)");
  ```
  如上所述，要保持不变式。

  对于 set操作, 它必须在成功写入时返回 true。

  如果我们忘记这样做或返回任何 falsy值，则该操作将触发 TypeError。
  同样还有其他操作,用时再查
  ###　eval() 执行函数( 现在不太用了)
  #### 偏函数(感觉像函数求偏导)
  bind的完整语法
  let bound = func.bind(context, arg1, arg2, ...);
  后面的都是参数
  ``` javascript
  let double = mul.bind(null, 2);

  console.log( double(3) ); // = mul(2, 3) = 6
  console.log( double(4) ); // = mul(2, 4) = 8
  console.log( double(5) ); // = mul(2, 5) = 10
  ```
  ### 柯里化
  将一个调用形式为 f(a, b, c) 的函数转化为调用形式为 f(a)(b)(c) 的技术。
  ### BigInt
  #### 创建
  const bigint = 
  1234567890123456789012345678901234567890n;

  const sameBigint = BigInt("1234567890123456789012345678901234567890");

  const bigintFromNumber = BigInt(10); // 等同于 10n
  注意:
  不可和其他数字对象混合;
  不能使用 + 转换
  其他与普通数字相同
  # DOM, BOM
  ## DOM
  ### 初始DOM树
  DOM 分为四种
  document—— DOM 中的“入口点”。
  元素节点 —— HTML 标签，树构建块。
  文本节点 —— 包含文本。
  注释 —— 有时我们可以将内容放入其中，它不会显示，但 JS 可以从 DOM 中读取它。
  ### 遍历DOM树
  最上面的树节点可以直接通过 document 属性来使用：

  <html> = document.documentElement
  最上面的 document 节点是 document.documentElement。这是对应 <html> 标签的 DOM 节点。
  <body> = document.body
  另一个被广泛使用的 DOM 节点是 <body> 元素 — document.body。
  <head> = document.head
  <head> 标签可以通过 document.head 访问。
  特别要注意的是，如果一个脚本是在 <head> 标签中，那么脚本中是访问不到 document.body 元素的，因为浏览器还没有读到其中的内容。

  childNodes 遍历所有子系元素
  firstChild 访问第一个子元素
  lastChild 访问最后一个子元素
  elem.hasChildNodes() 用于检测节点是否有子节点。
  parentNode 访问父节点
  在同一个父节点中一个节点的下一个节点（下一个兄弟节点）可以通过 nextSibling 访问，上一个节点可以通过 previousSibling 访问。
  上述方法可能找到文本空白的节点
  ``` javascript
  <html><head></head><body><script>
  //  HTML 代码是“密集”的用来避免额外的“空白”文本节点。
  HTML is "dense" to evade extra "blank" text nodes.

  // <body> 的父节点是 <html>
  console.log( document.body.parentNode === document.documentElement ); // true

  // <head> 的下一个兄弟节点是  <body>
  console.log( document.head.nextSibling ); // HTMLBodyElement

  // <body> 的上一个兄弟节点是  <head>
  console.log( document.body.previousSibling ); // HTMLHeadElement
</script></body></html>
  ```
  children —— 只获取类型为元素节点的子节点。
  firstElementChild，lastElementChild —— 第一个和最后一个子元素。
  previousElementSibling，nextElementSibling —— 兄弟元素。
  parentElement —— 父元素。
  <table>支持额外属性
  table.rows — 用于表示表中 <tr> 元素的集合。
  table.caption/tHead/tFoot — 用于访问元素 <caption>、<thead>、<tfoot>。
  table.tBodies — <tbody> 元素的集合（根据标准该元素数量可以很多）。
  <thead>、<tfoot>、<tbody> 元素提供了 rows 属性：

  tbody.rows — 表内部 <tr> 元素的集合。
  tr.cells — 在给定 <tr> 元素下 <td> 和 <th> 单元格的集合。
  tr.sectionRowIndex — 在封闭的 <thead>/<tbody> 中 <tr> 的编号。
  tr.rowIndex — 在表中 <tr> 元素的编号。
  <td> 和 <th>：
  td.cellIndex — 在封闭的 <tr> 中单元格的编号。
``` javascript
  <table id="table">
    <tr>
      <td>one</td><td>two</td>
    </tr>
    <tr>
      <td>three</td><td>four</td>
    </tr>
  </table>

  <script>
    // 获取第一行中第二个单元格的内容
    console.log( table.rows[0].cells[1].innerHTML ) // "two"
  </script>
```
  ### 搜索: getElement 和 querySelector

  #### document.getElementById(<id>)
    如果元素有 id 属性，那么该 id 也会有一个同名全局变量。
``` javascript
    <div id="elem">
      <div id="elem-content">Element</div>
    </div>

    <script>
      console.log(elem); // DOM-element with id="elem"
      console.log(window.elem); // accessing global variable like this also works

      // 对于 elem-content 会稍微有些复杂
      // 因为里面有破折号，所以不是一个变量名
      console.log(window['elem-content']); // ...但可以使用方括号 [...]
    </script>
```
  #### document.getElementsByTagName('div') 获取所有的div 标签
    elem.getElementsByClassName(className) 返回具有给定 CSS 类的元素。元素也可能含有其他的类。
  document.getElementsByName(name) 返回具有给定 name 属性的元素，文档范围。因为历史原因而很少使用。在这里提出，只是考虑到了完整性。
  #### querySelectorAll
  elem.querySelectorAll(css) 的调用将返回与给定 CSS 选择器匹配 elem 中的所有元素。这是最常用和最有力的方法。
  #### querySelector
  调用 elem.querySelector(css) 后，它会返回给定 CSS 选择器的第一个元素。

  换句话说，结果与 elem.querySelectorAll(css)[0] 相同，但是后者会从所有找到的元素中选取一个，而 elem.querySelector 只会查找一个。因此编写会更快更简洁。
  #### match 查找是否存在该节点,存在为 true, 不存在 false
  #### closest
  elem.closest(css) 方法会查找与 CSS 选择器匹配的最接近的祖先。elem 自己也会被搜索。

  换句话说，方法 closest 在元素中得到了提升，并检查每个父类。如果与选择器匹配，则停止搜索并返回祖先。
  ``` javascript
  <h1>Contents</h1>

  <div class="contents">
    <ul class="book">
      <li class="chapter">Chapter 1</li>
      <li class="chapter">Chapter 1</li>
    </ul>
  </div>

  <script>
    let chapter = document.querySelector('.chapter'); // LI

    console.log(chapter.closest('.book')); // UL
    console.log(chapter.closest('.contents')); // DIV

    console.log(chapter.closest('h1')); // null（因为 h1 不是祖先）
  </script>
  ```
  #### Live 集合
  所有的 "getElementsBy*" 方法都会返回 live 集合。这类集合总是可以反映出文档的当前状态而且在文档变化时，可以自动更新。
  下面的实例中，有两个脚本。
  1. 第一个方法创建了对集合 <div> 的引用。到目前为止，它的长度是 1。
  2. 第二个脚本在浏览器再遇到一个 <div> 时，它的长度会变成 2。
  ``` javascript
    <div>First div</div>
    <script>
      let divs = document.getElementsByTagName('div');
      console.log(divs.length); // 1
    </script>

    <div>Second div</div>

    <script>
      console.log(divs.length); // 2
    </script>
  ```
  相反，querySelectorAll 会返回一个static集合。就像一个固定的元素数字。

  如果我们使用它，那么两个脚本都会输出 1：
  ``` javascirpt
  <div>First div</div>

  <script>
    let divs = document.querySelectorAll('div');
    console.log(divs.length); // 1
  </script>

  <div>Second div</div>

  <script>
    console.log(divs.length); // 1
  </script>
  ```
  nodeType” 属性
  nodeType 属性提供了一个获取 DOM 节点类型的旧方法。

  它有一个数值：

  elem.nodeType == 1 是元素节点，
  elem.nodeType == 3 是文本节点，
  elem.nodeType == 9 是 document 对象，
  ``` javascript
  <body>
    <script>
    let elem = document.body;

    // 让我们检查一下它是什么？
    console.log(elem.nodeType); // 1 => element

    // 第一个子节点是
    console.log(elem.firstChild.nodeType); // 3 => text

    // 对于文档对象，类型是 9
    console.log( document.nodeType ); // 9
    </script>
  </body>
  ```
  标签：nodeName 和 tagName
  给定一个 DOM 节点，我们可以从 nodeName 或者 tagName 属性中读取它的标记名：

  例如：
  ``` javascript
  console.log( document.body.nodeName ); // BODY
  console.log( document.body.tagName ); // BODY
  ```
  #### innerHTML: the contents
  innerHTML 属性允许将元素中的 HTML 作为字符串来获取。

  我们也可以修改它。因此，这是改变页面最有效的方法之一。

  该示例显示了 document.body 的内容，然后完全替换它：
  #### outerHTML：元素的完整 HTML, 可以直接修改标签
  outerHTML 属性包含元素的完整 HTML。就像是 innerHTML 加上元素本身。

  下面是一个示例：
  ``` javascipt
  <div id="elem">Hello <b>World</b></div>

  <script>
    console.log(elem.outerHTML); // <div id="elem">Hello <b>World</b></div>
  </script>
  ```
  js 代码从上往下,执行 他会检测前面的html元素,而不会看后面的
  ``` javascript
  <div>hi</div> // hello
  <script>
  document.querySelector('div').innerHTML = 'hello';
  </script>
  <div>hi</div> // hi
  ```
  textContext 以文本插入不执行中间的html代码(防止用户注入)
  ``` javascript
  <div id="elem1"></div>
  <div id="elem2"></div>

  <script>
    let name = prompt("What's your name?", "<b>Winnie-the-pooh!</b>");

    elem1.innerHTML = name; // <b>标签里的会加粗
    elem2.textContent = name; // <b>标签里的不会加粗
  </script>
  ```
  #### hidden 属性 用于隐藏元素
  ``` javascript
  div>Both divs below are hidden</div>

  <div hidden>With the attribute "hidden"</div>

  <div id="elem">JavaScript assigned the property "hidden"</div>

  <script>
    elem.hidden = true;
  </script>
  ```
  #### 更多属性
  elem.hasAttribute(name) —— 检验是否拥这个特性。
  elem.getAttribute(name) —— 获取到这个特性值。
  elem.setAttribute(name, value) —— 设置这个特性值。
  elem.removeAttribute(name) —— 移除这个特性。
  elem.attributes 读取所有属性
  * 注意属性名大小写不敏感
  * 他们的值只能是字符串
  ``` javascript
  <body>
    <div id="elem" about="Elephant"></div>

    <script>
      console.log( elem.getAttribute('About') ); // (1) 'Elephant', reading

      elem.setAttribute('Test', 123); // (2), writing

      console.log( elem.outerHTML ); // (3), see it's there

      for (let attr of elem.attributes) { // (4) list all
        console.log( `${attr.name} = ${attr.value}` );
      }
    </script>
  </body>
  ```
  当一个标准化的特性被改变，相应的属性随之改变（有极个别除外），反之亦然。
  ``` javascript
  <input>
  <script>
    let input = document.querySelector('input');

    // 特性 => 属性
    input.setAttribute('id', 'id');
    console.log(input.id); // id（更新了）

    // 属性 => 特性
    input.id = 'newId';
    console.log(input.getAttribute('id')); // newId（更新了）
  </script>
  ```
  这里有一些特殊情况下的例子，input.value 只能从特性同步到属性，反过来则不行：
  ``` javascript
  <input>
  <script>
    let input = document.querySelector('input');

    // 特性 => 属性
    input.setAttribute('value', 'text');
    console.log(input.value); // text

    // 这操作无效 属性 => 特性
    input.value = 'newValue';
    console.log(input.getAttribute('value')); // text（没有更新！）
  </script>
  ```
  DOM 并不总是字符串。例如 input.checked 属性（多选框）是一个布尔类型的值。
  类似的例子还有，style 特性值是一个字符串，但 style 属性是一个对象：

  #### 自定义属性
  通常以data 开头
  ``` javascript
  <body data-about="Elephants">
  <script>
    console.log(document.body.dataset.about); // Elephants
  </script>
  ```
  ### 修改文档内容
  #### 生成元素
  * document.createElement(tag)
    用给定的标签创建一个新元素节点（element node);
  ``` javascript
  let div = document.createElement('div');
  ```
  * document.createTextNode(text)
    用给定的文本创建一个文本节点
  ``` javascript
  let textNode = document.createTextNode('Here I am');
  ```
  * 创建div的各种属性
  ``` javascript
  let div = document.createElement('div');
  div.className = "console.log console.log-success";
  div.innerHTML = "<strong>Hi there!</strong> You've read an important message.";
  ```
  #### 插值方法
  ``` javascript
  document.body.appendChild(div)。
  ```
  * parentElem.appendChild(node)
    将 node 作为 parentElem 最后一个子元素。
  ``` javascript
  <ol id="list">
    <li>0</li>
    <li>1</li>
    <li>2</li>
  </ol>

  <script>
    let newLi = document.createElement('li');
    newLi.innerHTML = 'Hello, world!';

    list.appendChild(newLi);
  </script>
  ```
  * parentElem.insertBefore(node, nextSibling)
    在 parentElem 的 nextSibling 插入 node。
  ``` javascript
  <ol id="list">
    <li>0</li>
    <li>1</li>
    <li>2</li>
  </ol>
  <script>
    let newLi = document.createElement('li');
    newLi.innerHTML = 'Hello, world!';

    list.insertBefore(newLi, list.children[1]);
  </script>
  ```
  * parentElem.replaceChild(node, oldChild)
    将 parentElem 的 oldChild 替换为 node。
    (基本不用上面三种但是要知道,不能看见不认识)
  * node.append(...nodes or strings) —— 在 node 末尾插入节点或者字符串，
  * node.prepend(...nodes or strings) —— 在 node 开头插入节点或者字符串，
  * node.before(...nodes or strings) —— 在 node 前面插入节点或者字符串，
  * node.after(...nodes or strings) —— 在 node 后面插入节点或者字符串，
  * node.replaceWith(...nodes or strings) —— 将 node 替换为节点或者字符串。
  ``` javascript
  <ol id="ol">
    <li>0</li>
    <li>1</li>
    <li>2</li>
  </ol>

  <script>
    ol.before('before');
    ol.after('after');

    let prepend = document.createElement('li');
    prepend.innerHTML = 'prepend';
    ol.prepend(prepend);

    let append = document.createElement('li');
    append.innerHTML = 'append';
    ol.append(append);
    // 结果
    before
    <ol id="ol">
      <li>prepend</li>
      <li>0</li>
      <li>1</li>
      <li>2</li>
      <li>append</li>
    </ol>
    after
  </script>
  ```
  #### 在相邻的 HTML 标签中插入/文本/元素
  elem.insertAdjacentHTML(where, html)。
  该方法第一个参数是代码字符串，指定相对于 elem 的插入位置，必须是以下四个值之一：
  "beforebegin" —— 在 elem 开头位置前插入 html，
  "afterbegin" —— 在 elem 开头位置后插入 html（译注：即 elem 元素内部的第一个子节点之前），
  "beforeend" —— 在 elem 结束位置前插入 html（译注：即 elem 元素内部的最后一个子节点之后），
  "afterend" —— 在 elem 结束位置后插入 html。
  第二个参数是 HTML 字符串，会以 HTML 的形式插入到页面中。
  ``` javascript
  <div id="div"></div>
  <script>
    div.insertAdjacentHTML('beforebegin', '<p>Hello</p>');
    div.insertAdjacentHTML('afterend', '<p>Bye</p>');
  </script>
  <p>Hello</p>
  <div id="div"></div>
  <p>Bye</p>
  ```
  #### 克隆节点
  elem.cloneNode(true) 方法用来对一个元素进行“深”克隆 —— 包括所有特性和子元素。

  elem.cloneNode(false) 方法只克隆该元素本身，不对子元素进行克隆。
  一个复制信息的例子：
  ``` javascript
  <style>
  .console.log {
    padding: 15px;
    border: 1px solid #d6e9c6;
    border-radius: 4px;
    color: #3c763d;
    background-color: #dff0d8;
  }
  </style>

  <div class="console.log" id="div">
    <strong>Hi there!</strong> You've read an important message.
  </div>

  <script>
    let div2 = div.cloneNode(true); // 克隆信息
    div2.querySelector('strong').innerHTML = 'Bye there!'; // 改变克隆信息

    div.after(div2); // 显示克隆信息在已经存在的 div 后
  </script>
  ```
  #### 文档片段（DocumentFragment）
  ``` javascript
  <ul id="ul"></ul>

  <script>
  function getListContent() {
    let result = [];

    for(let i=1; i<=3; i++) {
      let li = document.createElement('li');
      li.append(i);
      result.push(li);
    }

    return result;
  }

  ul.append(...getListContent()); // append + “...” 操作符 = 一对好朋友！
  </script>
  ```
  ### 移除
  node.remove()
  从当前位置移除 node。
  总结
  创建节点的方法：

  document.createElement(tag) —— 用给定标签创建一个节点，
  document.createTextNode(value) —— 创建一个文本节点（很少使用），
  elem.cloneNode(deep) —— 如果参数 deep==true 将元素及后代子元素进行克隆。
  插入和移除节点的方法：

  从 parent

  parent.appendChild(node)
  parent.insertBefore(node, nextSibling)
  parent.removeChild(node)
  parent.replaceChild(newElem, node)
  这些方法都返回 node。

  添加一些节点和字符串：

  node.append(...nodes or strings) —— 在 node 末尾位置增加，
  node.prepend(...nodes or strings) —— 在 node开头位置增加 ，
  node.before(...nodes or strings) —— 在 node 之前位置增加，
  node.after(...nodes or strings) —— 在 node 之后位置增加，
  node.replaceWith(...nodes or strings) —— 替换 node。
  node.remove() —— 移除 node。
  把字符串当成“文本”插入。

  在 HTML 中添加内容 elem.insertAdjacentHTML(where, html)，在 where 位置进行操作：

  "beforebegin" —— 将 html 插入 elem 到开头的前面位置，
  "afterbegin" —— 将 html 插入 elem 到开头的后面位置，
  "beforeend" —— 将 html 插入 elem 到结尾的前面位置，
  "afterend" —— 将 html 插入 elem 到结尾的后面位置。
  elem.insertAdjacentText 和 elem.insertAdjacentElement 跟 elem.insertAdjacentHTML 很相似，只不过他们一个用来插入字符串，一个用来插入元素，但是很少使用这两个方法。

  在页面加载完成之前添加 HTML 到页面中：

  document.write(html)
  如果是在页面加载完成以后调用会擦除加载完毕的内容。通常在很老的脚本才会使用这个方法了。
  通过 
  function parseDom(arg) {
　　 var objE = document.createElement("div");
　　 objE.innerHTML = arg;
    let obj = objE.children;
　　 return objE.children;
  };
  将字符串转为HTML元素
  ``` javascript
  document.body.append(...parseDom(`
  <div>开始</div><div>结束</div>
  `))
  ```
  完毕,暂时找到的最佳方法,肯定不止...
  ### 样式和类
  查看类名:
  console.log(document.body.className);
  修改样式的方法:
  1. elem.style.left = left;
    修改类的方法:
  1. elem.classList.add/remove("class") —— 添加/移除类。
  2. elem.classList.toggle("class") —— 如果类存在就移除，否则添加。
  3. elem.classList.contains("class") —— 返回 true/false，检查给定类。
    重置样式属性:
    document.body.style.display = ""
    style.cssText 重写样式
  #### 读取样式
  * 计算样式：getComputedStyle
  ``` javascript
  <head>
    <style> body { color: red; margin: 5px } </style>
  </head>
  <body>

    <script>
      let computedStyle = getComputedStyle(document.body);

      // 现在我们可以读出页边距和颜色了

      console.log( computedStyle.marginTop ); // 5px
      console.log( computedStyle.color ); // rgb(255, 0, 0)
    </script>
  </body>
  ```
  ### 元素的尺寸与滚动
  注意如果元素需要滚动条,滚动条,会挤压内部内容
  ![](.\images\元素位置与大小属性.PNG)
  以上属性的值,要熟记

  这些属性很少出现，但它们仍然是“最外层”的几何属性，所以我们将从它们开始。
  offsetParent, offsetLeft/Top
  offsetParent 是最近的祖先元素:

  CSS 定位（position 为 absolute、relative 或 fixed），
  或者 <td>、<th>、<table>，
  或者 <body>。
  offsetWidth/Height 元素对外的真实大小
  注意:被隐藏是读不出宽度和高度的大小的
  clientTop 和 clientLeft。边框宽度
  clientWidth/Height 文本加边框（不包含隐藏部分）
  scrollWidth/Height 文本加边框（包含隐藏部分）
  scrollLeft/scrollTop 是元素隐藏、滚动部分的宽度/高度。
  除了 scrollLeft/scrollTop 之外，所有属性都是只读的。如果更改，浏览器会使元素滚动。
  ### 窗口的宽度/高度
  * clientWidth/clientHeight(我们想要的)
  document.documentElement 的 clientWidth/clientHeight
  innerWidth/Height(去除滚动条的宽度)
  ``` javascript
  ```
  ### 文档的宽度/高度
  ``` javascript
  let scrollHeight = Math.max(
    document.body.scrollHeight, document.documentElement.scrollHeight,
    document.body.offsetHeight, document.documentElement.offsetHeight,
    document.body.clientHeight, document.documentElement.clientHeight
  );
  console.log('Full document height, with scrolled out part: ' + scrollHeight);
  ```
  ### 滚动
  #### 读取滚动
  * 读取当前的滚动：window.pageYOffset/pageXOffset
  * 可以通过更改 scrollTop/scrollLeft 来滚动常规元素。

  在 Chrome/Safari/Opera 外的所有浏览器：修改

  document.documentElement.scrollTop/Left。
  在 Chrome/Safari/Opera 浏览器：使用 

  document.body.scrollTop/Left。
  可是这样太繁琐了

  可以用后面的替换
  window.scrollBy(x,y) 和 window.scrollTo(pageX,pageY)
  一个是 向下向右滑动 y,x 一个是 滑动到 y, x 全部是数字,以px为单位(我真是个傻逼)
  #### 滚动到视图
  elem.scrollIntoView(top) 
  
  会使 elem 滚动到可视范围。它有一个结论：

  如果 top=true（默认值），页面滚动使 elem 会出现到窗口顶部。元素的上边缘与窗口顶部对齐。

  如果 top=false，则页面滚动使 elem 会出现在窗口底部。元素的下边缘与窗口底部对齐。
  注意:他有前提
  1. 元素不能在视图内,即看得见的位置(否则无效)
  ### 坐标
  1. 相对于窗口,窗口坐标
  窗口的坐标是从窗口的左上角开始计算的。

  elem.getBoundingClientRect() 方法返回一个 elem 的窗口坐标对象，这个对象有以下这些属性：

  top — 元素顶部边缘的 Y 坐标
  left — 元素左边边缘的 X 坐标
  right — 元素右边边缘的 X 坐标
  bottom — 元素底部边缘的 Y 坐标
  #### elementFromPoint(x, y)
  调用 document.elementFromPoint(x, y) 方法返回窗口坐标 (x, y) 中最顶层的元素。
  let centerX = document.documentElement.clientWidth / 2;
  let centerY = document.documentElement.clientHeight / 2;

  let elem = document.elementFromPoint(centerX, centerY);

  elem.style.background = "red";
  console.log(elem.tagName);
  相对窗口使用 fixed
  2. 相对于文档的坐标
  pageY = clientY + 文档垂直部分滚动的高度。
  pageX = clientX + 文档水平部分滚动的宽度。
  ``` javascript
  // 获取元素的文档坐标
  function getCoords(elem) {
    let box = elem.getBoundingClientRect();

    return {
      top: box.top + pageYOffset,
      left: box.left + pageXOffset
    };
  }
  ```
  #### 鼠标相对与窗口的位置
  event.clientX / event.clientY
  鼠标事件中光标相对于窗口的坐标。
  ``` javascript
  <input type="button" value="Click me" id="elem">

  <script>
    elem.onclick = function(event) {
      // 显示事件类型、元素和单击的坐标。
      console.log(event.type + " at " + event.currentTarget);
      console.log("Coordinates: " + event.clientX + ":" + event.clientY);
    };
  </script>
  ```
  ### 浏览器事件简介
  鼠标事件：

  * click —— 当鼠标点击一个元素时（触摸屏设备在 tap 时生成）。
  * contextmenu —— 当鼠标右击一个元素时。
  * mouseover / mouseout —— 当鼠标光标移入或移出一个元素时。
  * mousedown / mouseup —— 当鼠标按下/释放一个元素时。
  * mousemove —— 当鼠标移出时。
  表单元素事件：

  * submit —— 当访问者提交了一个 <form> 时。
  * focus —— 当访问者聚焦一个元素时，例如 <input>。
  键盘事件：

  * keydown and keyup —— 当访问者按下然后松开按钮时。
  Document 事件：

  * DOMContentLoaded —— 当加载和处理 HTML 时，DOM 将会被完整地构建。
  CSS 事件：

  * transitionend —— 当 CSS 动画完成时。
  还有许多其他事件。我们将在下一章中详细介绍具体事件。

  事件处理器
  为了响应事件，我们可以通过分发处理器 —— 在事件发生时运行的函数。


  #### HTML属性
  ``` javascript
  <input value="Click me" onclick="console.log('Click!')" type="button">
  ```
  #### DOM属性(推荐这种)
  ``` javascript
  <input id="elem" type="button" value="Click me">
  <script>// 如果要输入多个函数,用外部的一个function包裹他们就行了
    elem.onclick = function() {
      console.log('Thank you');
    };
  </script>
  ```
  * this  onclick中的 this 指代的是被操作的DOM元素

  #### addEventListener

  * 语法

  添加: element.addEventListener(event, handler[, phase]);

  移除:element.removeEventListener(event, handler[, phase]);
  
  * 多次调用 addEventListener 允许添加多个处理器，就像这样：如果要写建议写一起
  ``` javascript
  <input id="elem" type="button" value="Click me"/>

  <script>
    function handler1() {
      console.log('Thanks!');
    };

    function handler2() {
      console.log('Thanks again!');
    }

    elem.onclick = () => console.log("Hello");
    elem.addEventListener("click", handler1); // Thanks!
    elem.addEventListener("click", handler2); // Thanks again!
  </script>
  ```
  * 有些事件处理器只能通过 addEventListener 
  比如 trnansitionend (css动画完成)
  ``` javascript
  <style>
    input {
      transition: width 1s;
      width: 100px;
    }

    .wide {
      width: 300px;
    }
  </style>

  <input type="button" id="elem" onclick="this.classList.toggle('wide')" value="Click me">
  
  <script>
    elem.ontransitionend = function() {
      console.log("DOM property"); // doesn't work
    };

    elem.addEventListener("transitionend", function() {
      console.log("addEventListener"); // 动画完成时显示
    });
  </script>
  ```
  换句话说，当 addEventListener 接收一个对象作为处理器时候，就会调用 object.handleEvent(event) 来处理事件。

  我们也可以使用一个类：
  ``` javascript

  <button id="elem">Click me</button>

  <script>
    class Menu {
      handleEvent(event) {
        switch(event.type) {
          case 'mousedown':
            elem.innerHTML = "Mouse button pressed";
            break;
          case 'mouseup':
            elem.innerHTML += "...and released.";
            break;
        }
      }
    }

    let menu = new Menu();
    elem.addEventListener('mousedown', menu);
    elem.addEventListener('mouseup', menu);
  </script>
  ```
  ### 冒泡
  focus() 不冒泡
  其他大部分是冒泡的
  停止冒泡
  event.stopPropagation()。阻止向上冒泡,不能阻止本层的事件
  event.stopImmediatePropagation() 阻止向上冒泡,并阻止本层的事件
  #### DOM 事件标准描述了事件传播的 3 个阶段：

  * 捕获阶段 —— 事件（从 Window）向下到达元素上。
  * 目标阶段 —— 事件到达目标元素。
  * 冒泡阶段 —— 事件从元素上开始冒泡。
  ### 事件委托
  #### event.target 获取包含单击位置的最内层元素(核心)
  我们的想法是，如果我们有许多元素是以类似的方式处理的，那么我们就不需要给每个元素分配一个处理器 —— 而是在它们共同的祖先上面添加一个处理器。
  ``` javascript
  able.onclick = function(event) {
    let td = event.target.closest('td'); // (1)

    if (!td) return; // (2)

    if (!table.contains(td)) return; // (3)

    highlight(td); // (4)
  };
  ```
  #### 委托示例：标记中的操作
  例如，我们想要制作一个有“保存”、“加载”和“搜索”等功能的菜单。有一个拥有 save、load 和 search 等方法的对象。

  第一个想法可能是为每个按钮分配一个单独的处理器。但有一个更优雅的解决方案。我们可以为整个菜单添加一个处理器，并为有方法调用的按钮添加 data-action 属性：

  ``` javascript
  <div id="menu">
    <button data-action="save">Save</button>
    <button data-action="load">Load</button>
    <button data-action="search">Search</button>
  </div>

  <script>
    class Menu {
      constructor(elem) {
        this._elem = elem;
        elem.onclick = this.onClick.bind(this); // (*)
      }

      save() {
        console.log('saving');
      }

      load() {
        console.log('loading');
      }

      search() {
        console.log('searching');
      }

      onClick(event) {
        let action = event.target.dataset.action;
        if (action) {
          this[action]();
        }
      };
    }

    new Menu(menu);
  </script>
  ```
  ### 浏览器默认动作
  许多事件会自动触发浏览器动作。

  例如：

  * 单击一个链接 —— 触发到它的 URL。
  * 单击表单中的提交按钮 —— 触发提交到服务器的动作。
  * 在文本上按下鼠标按键并移动 —— 选中文本。
  阻止方法:
  ``` javascript
  <a href="/" onclick="return false">Click here</a> // return false 只实用与分发 on<event>的事件

  <a href="/" onclick="event.preventDefault()">here</a>
  ```
  阻止进一步的事件
  input 如果没有 mousedown ,则不会触发 focus()
  ``` javascript
  <input value="Focus works" onfocus="this.value=''">
  <input onmousedown="return false" onfocus="this.value=''" value="Click me">
  ```
  * event.preventDefault() 阻止默认行为

  ### 生成自定义事件

  #### 事件构造器

  ``` javascript
  let event = new Event(event type[, options]);

  ```
  event type —— 可以是任何字符串，比如 "click" 或者我们自己喜欢的 "hey-ho!"。

  options —— 具有两个可选属性的对象：

  bubbles: true/false —— 如果是 true，那么事件冒泡。
  cancelable: true/false —— 如果 true，那么“默认动作”就会被阻止。之后我们会看到对于自定义事件，这些意味着什么。
  默认情况下，它们都是 false：{bubbles: false, cancelable: false}。
  ``` javascript
  <button id="elem" onclick="console.log('Click!');">Autoclick</button>
  <script>
    let event = new Event("click");
    elem.dispatchEvent(event);
  </script>
  ```
  event.isTrusted
  有一个可以区分 “真实”用户事件和 script 生成事件的方法。

  event.isTrusted 属性为 true，则事件来自真实用户的动作，为 false ，则说明事件由脚本生成。
  ``` javascript
  <h1 id="elem">Hello from the script!</h1>

  <script>
    // catch on document...
    document.addEventListener("hello", function(event) { // (1)
      console.log("Hello from " + event.target.tagName); // Hello from H1
    });

    // ...dispatch on elem!
    let event = new Event("hello", {bubbles: true}); // (2)
    elem.dispatchEvent(event);
  </script>
  ```

  但是并没有事件去触发上面的 hello 函数
  #### event.preventDefault() 阻止自定义事件的发生
  
  ``` javascript
  <pre id="rabbit">
    |\   /|
     \|_|/
     /. .\
    =\_Y_/=
     {>o<} 
  </pre>

  <script>
    // hide() will be called automatically in 2 seconds
    function hide() {
      let event = new CustomEvent("hide", {
        cancelable: true // without that flag preventDefault doesn't work
      });
      if (!rabbit.dispatchEvent(event)) {
        console.log('the action was prevented by a handler');
      } else {
        rabbit.hidden = true;
      }
    }

    rabbit.addEventListener('hide', function(event) {
      if (confirm("Call preventDefault?")) {
        event.preventDefault();
      }
    });

    // hide in 2 seconds
    setTimeout(hide, 2000);

  </script>
  ```
  ### 鼠标事件类型
  * 我们可以将鼠标事件分成两类：“简单”和“复杂”

  #### 简单事件
  最常用的简单事件是：

  mousedown/mouseup
  在元素上单击/释放鼠标按钮。
  mouseover/mouseout
  鼠标指针从一个元素上移入/出。
  mousemove
  鼠标每次移动到元素上时都会触发事件。
  …还有其他几种事件类型，我们稍后会讨论它们。

  #### 复杂事件
  click
  如果使用鼠标左键，则在 mousedown 及 mouseup 相继触发后触发该事件。
  contextmenu
  如果使用鼠标右键，则在 mousedown 后触发。
  dblclick
  在对元素进行双击后触发。
  复杂事件是由简单事件组成的，因此理论上我们可以没有它们而运转。但它们的存在却给我们提供了极大的便利。

  事件顺序
  一个动作可能会触发多个事件。

  比如，在按下鼠标按钮时，单击会首先触发 mousedown，然后释放鼠标按钮时，会触发 mouseup 和 click。

  在单个动作触发多个事件时，它们的顺序是固定的。也就是说会遵循 mousedown → mouseup → click 的顺序。事件按照相同的顺序被处理：onmouseup 在 onclick 运行之前完成。
  #### 获取按钮：which(这是啥?)
  与单击相关的事件始终具有 which 属性，该属性允许获取准确的鼠标按钮。

  它不用于 click和 contextmenu 事件，因为前者只发生在左键，而后者只发生在右击。

  但如果我们跟踪 mousedown 和 mouseup，那么我们就需要它，因为这些事件在任意鼠标按钮按下时都会触发，所以 which 允许区分 “right-mousedown” 和 “left-mousedown”。

  有三个可能的值：

  event.which == 1 —— 左按钮
  event.which == 2 —— 中间按钮
  event.which == 3 —— 右按钮
  中间按钮现在有些特殊，所有很少被使用。

  ``` javascript
  注意：在 Mac 上我们通常使用 Cmd 而不是 Ctrl (看看就好>.<)
  在 Windows 和 Linux 上修改键是 Alt、Shift 和 Ctrl。在 Mac 上还有：Cmd，它对应于属性 metaKey。

  在大多数情况下，当 Windows/Linux 使用 Ctrl 时，Mac 的用户会使用 Cmd。因此当 Windows 用户按下 Ctrl+Enter 或 Ctrl+A 时，Mac 用户会按下 Cmd+Enter 或 Cmd+A 等，大多数 app 使用 Cmd 而不是 Ctrl。

  因此如果我们想支持 Ctrl+click，那么对于 Mac 用户来说，使用 Cmd+click 也是有意义的。这对于 Mac 用户来说非常舒服。

  即使我们想迫使 Mac 用户使用 Ctrl+click —— 也非常困难。问题在于：Mac 上左击 Ctrl 被解释为右击，它会生成 contextmenu 事件，而不是像 Windows/Linxu 的 click 事件。

  因此如果我们想让所有操作系统的用户感觉舒适，那么我们应该和 ctrlKey 一起使用 metaKey。

  对于 JS 代码，这意味着我们应该检查 if (event.ctrlKey || event.metaKey)。
  ```
  坐标：clientX/Y，pageX/Y
  所有的鼠标事件都有两种形式的坐标：

  对于窗口而言：clientX 和 clientY。
  对于文档而言：pageX 和 pageY。
  比如，如果我们有一个 500 x 500 的窗口，鼠标在左上方，那么 clientX 和 clientY 都是 0。如果鼠标在中间，那么 clientX 和 clientY 就是 250。和它在文档中的位置无关。它们类似于 position:fixed。

  将鼠标移动到输入字段上，可以看到 clientX/clientY（它在 iframe 中，因此坐标是相对于 iframe 而言的）

  还有 CSS 方法可以终止选择：CSS UI 草案 中的 user-select 属性。(但是这段文字无法复制!)

  大多数浏览器都支持它的前缀：  
  ``` javascript
    <style>
      b {
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
      }
    </style>

    Before...
    <b ondblclick="console.log('Test')">
      Unselectable
    </b>
    ...After
  ```
  好的方法为阻止 mousedown
  ``` javascript
    Before...
  <b ondblclick="console.log('Click!')" onmousedown="return false">
    Double-click me
  </b>
   ...After
  ```
  #### 取消选择(我感觉不可能用到 >.<)

  我们可以在事件处理器中用 “post-factum” 取消它，而不是阻止选择它。
  ``` javascript
  这是方法：

  Before...
  <b ondblclick="getSelection().removeAllRanges()">
    Double-click me
  </b>
  ...After
  ```
  #### 防止复制(这个可以)
  ``` javascript
  <div oncopy="console.log('Copying forbidden!');return false">
  Dear user,
  The copying is forbidden for you.
  If you know JS or HTML, then you can get everything from the page source though.
</div>
  ```
  ### 移动：mouseover/out，mouseenter/leave

  #### 这两个有额外属性 relatedTarget

  对于 mouseover：

  event.target —— 是鼠标经过的那个元素。

  event.relatedTarget —— 是鼠标上一次经过的元素。

  mouseout 则与之相反：

  event.target —— 是鼠标离开的元素。

  event.relatedTarget —— 是当前指针位置下的（鼠标进入的）元素。

  relatedTarget 可以为 null
  relatedTarget 属性可以为 null。

  这很正常，而且意味着鼠标不是来源于另一个元素，而是窗口以外。或者是离开了窗口。

  当我们在代码中使用 event.relatedTarget 时，我们应该记住这种可能性。如果我们访问 event.relatedTarget.tagName，那么就会出现错误。
  
  #### 缺点:
  进入子元素时的“额外” mouseout
  想象一下 —— 鼠标指针进入一个元素。mouseover 被触发。然后光标进入一个子元素。有趣的是，在这种情况下 mouseout 会被触发。光标仍然在元素中，但我们从它那儿接收到了 mouseout 事件！

  Mouseenter, mouseleave

  mouseenter/mouseleave 事件类似于 mouseover/mouseout。当鼠标指针移入/移出元素时，它们也会被触发。

  但有两个不同之处：

  1. 元素内部的转换不会有影响。
  2. mouseenter/mouseleave 事件不会冒泡。

  ### 拖放鼠标事件

  拖放算法
  拖放基础算法就像这样：

  在可拖动元素上捕获 mousedown 事件。
  准备要移动的元素（可能创建它的副本或其他任何东西）。
  然后在 mousemove 上，通过改变 left/top 和 position:absolute 来移动它。
  在 mouseup（释放按钮）中 —— 执行所有完成拖放相关的动作。

  ``` javascript
  ball.onmousedown = function(event) {

  let shiftX = event.clientX - ball.getBoundingClientRect().left;
  let shiftY = event.clientY - ball.getBoundingClientRect().top;

  ball.style.position = 'absolute';
  ball.style.zIndex = 1000;
  document.body.append(ball);

  moveAt(event.pageX, event.pageY);

  // 球中心在 (pageX, pageY) 坐标上
  function moveAt(pageX, pageY) {
    ball.style.left = pageX - shiftX + 'px';
    ball.style.top = pageY - shiftY + 'px';
  }

  function onMouseMove(event) {
    moveAt(event.pageX, event.pageY);
  }

  // (3) 用 mousemove 移动球
  document.addEventListener('mousemove', onMouseMove);

  // (4) 释放球，移除不需要的处理器
  ball.onmouseup = function() {
    document.removeEventListener('mousemove', onMouseMove);
    ball.onmouseup = null;
  };

};

ball.ondragstart = function() {
  return false;
};
```

 #### document.elementFromPoint(clientX, clientY)
 
 document.elementFromPoint(clientX, clientY) 的方法。它会根据给定的窗口相对坐标，返回该处嵌套最深的元素（如果坐标在窗口之外，则返回 null）。

### 键盘侠
#### Keydown 和 keyup
当键被按下时，keydown 事件会发生，而当键被释放时，keyup 事件会发生。
#### event.code 和 event.key
事件对象 key 属性允许获取字符，而事件对象的 code 属性允许获取“物理秘钥代码”。

例如，相同的键 Z 可以按下或者不按下 Shift。这给了我们两个不同的字符：小写的 z 和大写 Z。

event.key 正是这个字符，并且它将是不同的。但是，event.code 是相同的：
如果用户使用不同的语言，那么切换到另一种语言就会产生一个完全不同的字符，而不是 "Z"。这将成为 event.key 的值，而 event.code 则始终是一样的："KeyZ"。

字符键有代码 "Key<letter>"："KeyA" 和 "KeyB" 等。
数字键有代码："Digit<number>"："Digit0" 和 "Digit1" 等。
特殊秘钥按其名称编码："Enter"、"Backspace" 和 "Tab" 等。
如果键没有给出任何字符呢？例如，Shift 或 F1 或其他的。对于那些键的 event.key 则与 event.code 大致相同：

Key	             event.key	              event.code

F1	                F1	                       F1

Backspace	       Backspace	               Backspace

Shift	             Shift	             ShiftRight 或 ShiftLeft

``` javascript
document.addEventListener('keydown', function(event) {
  if (event.code == 'KeyZ' && (event.ctrlKey || event.metaKey)) {
    console.log('Undo!')
  }
});
```
#### 总结
按一个键总是会产生一个键盘事件，无论是符号键还是特殊键，比如 Shift 或 Ctrl 等。唯一的例外是 Fn，它有时会出现在笔记本电脑键盘上。它没有键盘事件，因为它通常在比 OS 低的级别上实现的。

键盘事件：

keydown —— 长久按键（如果按下长键则自动重复），

keyup —— 释放按键时。

主键盘事件属性：

code —— “按键代码”（"KeyA"、"ArrowLeft" 等），具体到键盘上键的物理位置。

key —— 非字符键的字符（"A"、"a" 等），通常具有和 code 一样的值。

过去，键盘事件有时用于跟踪用户在表单字段中的输入。这很不可靠，因为输入源可以不同。我们有 input 和 change 事件来处理任何输入（之后我们会在 事件：change、input、cut、copy 和 paste 章节中作进一步介绍）。它们在任何输入后触发，包括鼠标或语音识别。

当我们真正想要键盘时，我们应该使用键盘事件。比如，对热键或特殊键作出反应。

### 滚动 (显示当前的滚动)
``` javascript
window.addEventListener('scroll', function() {
  document.getElementById('showScroll').innerHTML = pageYOffset + 'px';
});
```
#### 防止滚动(建议用css)

### 表单属性和方法

文档中的表单是一个特殊集合 document.forms 中的成员。

document.forms 是一个命名集合：我们既可以使用名字也可以使用索引来获取表单。

document.forms.my - 包含了 name="my" 的表单
document.forms[0] - 文档中的第一个表单
当我们有了一个表单，其中任何的元素都可以通过命名集合 form.elements 来获取到。

比如说：
``` javascript
<form name="my">
  <input name="one" value="1">
  <input name="two" value="2">
</form>

<script>
  // 获取表单
  let form = document.forms.my; // <form name="my"> 元素

  // 获取表单中的元素
  let elem = form.elements.one; // <input name="one"> 元素

  console.log(elem.value); // 1
</script>
```

#### 表单元素

让我们来谈谈表单控件，主要关注于它们具体的特性。

input 和 textarea

通常来说，我们可以使用 input.value 或者 input.checked 来访问复选框的值。

就像下面这样： (绝对不要使用 innerHTML)
``` javascript
input.value = "New value";

textarea.value = "New text";

input.checked = true; // 用于复选框或者单选按钮
```

#### select 和 option

一个 <select> 元素有 3 个重要的属性：

select.options —— <option> 元素的集合，

select.value —— 所选选项的值，

select.selectedIndex —— 所选选项的索引。

所以我们会有三种方式来设置一个 <select> 元素的值：

* 找到所需要的 <option> 元素之后设置 option.selected 为 true。

* 设置 select.value 为对应的值。

* 设置 select.selectedIndex 为对应选项的索引。

第一个方式是最显而易见的，但是 (2) 和 (3) 通常来说会更简便。
``` javascript
<select id="select">
  <option value="apple">Apple</option>
  <option value="pear">Pear</option>
  <option value="banana">Banana</option>
</select>

<script>
  // 所有这三行做的是同一件事
  select.options[2].selected = true;
  select.selectedIndex = 2;
  select.value = 'banana';
</script>
```
和大多数其它控件不同，<select multiple> 允许多选。在这种情况下，我们需要遍历 select.options 来获取所有选定的值。

就像下面这样：

<select id="select" multiple>
  <option value="blues" selected>Blues</option>
  <option value="rock" selected>Rock</option>
  <option value="classic">Classic</option>
</select>

<script>
  // 从 multi-select 中获取所有选定的值
  let selected = Array.from(select.options)
    .filter(option => option.selected)
    .map(option => option.value);

  console.log(selected); // blues，rock
</script>
##### 新的选项
在选项元素的规范中，有一个很不错的简短语法用来创建 <option> 元素：

option = new Option(text, value, defaultSelected, selected);
该方法调用参数如下：

text —— 选项中的文本，

`value —— 选项的默认值,

defaultSelected —— 如果这个值是 true，那么 selected 属性就会默认创建，

selected —— 如果这个值是true`，那么这个选项就是已经被选择了。
``` javascript
let option = new Option("Text", "value");
// 创建 <option value="value">Text</option>
```

### 聚焦：focus/blur

focus/blur 事件
``` javascript
<style>
  .invalid { border-color: red; }
  #error { color: red }
</style>

Your email please: <input type="email" id="input">

<div id="error"></div>

<script>
input.onblur = function() {
  if (!input.value.includes('@')) { // not email
    input.classList.add('invalid');
    error.innerHTML = 'Please enter a correct email.'
  }
};

input.onfocus = function() {
  if (this.classList.contains('invalid')) {
    // remove the "error" indication, because the user wants to re-enter something
    this.classList.remove('invalid');
    error.innerHTML = "";
  }
};
</script>
```
#### 
focus/blur 方法
方法 elem.focus() 和 elem.blur() 可以设置和移除元素上的焦点。
火狐浏览器 在onblur 中 调用 focus() 会失败

注意，我们不可以通过在 onblur 事件处理器里调用 event.preventDefault() 来“阻止失去焦点”，因为 onblur 事件处理器是在元素失去焦点的之后运行的。
#### 允许在任何元素上聚焦：tabindex

从另一方面说，为了格式化某些东西而存在的元素像 <div>、
<span> 和 <table> — 默认是不能被聚焦的。elem.focus() 方法
不能作用于它们，而且 focus/blur 事件也绝不会被触发。
使用 HTML 属性 tabindex 可以改变这种默认情况。

这个属性的目的是当使用 Tab 在元素之间切换的时候指定它们的排列顺序。

也就是说：如果我们有两个元素，第一个有属性 tabindex="1"，第二个有 tabindex="2"，然后当焦点在第一个元素的时候，按下 Tab 键，会让焦点移动到第二个元素身上。

这里有两个特别的值：

tabindex="0" 让元素成为最后一个。
tabindex="-1" 意味着 Tab 应该忽略这个元素。
任何元素如果有属性 tabindex，它将会支持聚焦。

``` javascript

Click the first item and press Tab. Keep track of the order. Please note that many subsequent Tabs can move the focus out of the iframe with the example.
<ul>
  <li tabindex="1">One</li>
  <li tabindex="0">Zero</li>
  <li tabindex="2">Two</li>
  <li tabindex="-1">Minus one</li>
</ul>

<style>
  li { cursor: pointer; }
  :focus { outline: 1px dashed green; }
</style>
```
* 注意:顺序就像这样：1 - 2 - 0（0 总是最后一个）。正常情况下，<li> 元素不支持被聚焦，但 tabindex 使这成为可能，顺带还会触发事件和使 :focus 样式生效。
* elem.tabIndex 也一样有效
我们可以通过 JavaScript 使用 elem.tabIndex 来添加 tabindex 属性。效果是一样的。

focus 和 blur 没有冒泡,但是可以捕获
有 focusin 和 focusout 事件可以使用 — 恰好和 focus/blur 事件很像,只不过它们会向上冒泡。
``` javascript
<form id="form">
  <input type="text" name="name" value="Name">
  <input type="text" name="surname" value="Surname">
</form>

<style> .focused { outline: 1px solid red; } </style>

<script>
  // put the handler on capturing phase (last argument true)
  form.addEventListener("focusin", () => form.classList.add('focused'));
  form.addEventListener("focusout", () => form.classList.remove('focused'));
</script>
```
* document.activeElement 来获取正在被聚焦的元素

### 事件：change
change 事件是在元素变化结束之后触发的。

对于文本输入框来说，当其失去焦点的时候就会触发 change 事件。

例如，当我们在下面的文本区域中输入的时候，change 事件不会被触发。但是当我们将焦点移到别处时，例如点击按钮，就会触发 change 事件：

``` javascript
<input type="text" onchange="console.log(this.value)">
<input type="button" value="Button">
```
对于其它元素：select，input type=checkbox/radio，change 事件会在选项变化后立即触发。
### 事件：input
每当输入的值发生改变时，就会触发 input 事件。

例如：

<input type="text" id="input"> oninput: <span id="result"></span>
<script>
  input.oninput = function() {
    result.innerHTML = input.value;
  };
</script>

#### 事件：cut、copy 和 paste
这些事件发生于剪切/拷贝/粘贴一个值的时候。

它们属于 ClipboardEvent 类，并且提供对拷贝/粘贴的数据的访问方法。

我们也可以使用 event.preventDefault() 来终止操作。

例如，下面的代码阻止了所有的这样的事件，然后展示出了我们尝试剪切/拷贝/粘贴的内容：

<input type="text" id="input">
<script>
  input.oncut = input.oncopy = input.onpaste = function(event) {
    console.log(event.type + ' - ' + event.clipboardData.getData('text/plain'));
    return false;
  };
</script>
事件：submit
提交表单有两种方法：

第一种 — 点击 <input type="submit"> 或者 <input type="image">。
第二种 — 在输入框内按下 Enter 回车键。

submit 和 click 的关系
当在输入框中使用 Enter 发送表单时，click 事件在 <input type="submit"> 上也会触发。

这是相当有趣的，因为实际上我们没有点击任何元素。


#### submit 方法

如果要手动向服务器提交表单，我们可以调用 form.submit()。

### 页面生命周期

HTML 页面的生命周期有三个重要事件：

* DOMContentLoaded —— 浏览器完成全部 HTML 的加载，并构建 DOM 树，但像 <img> 和样式这样的外部资源可能还没有加载完成。
* load —— 浏览器加载完所有资源，包括 HTML 文档，图像，样式等。
* beforeunload/unload —— 当用户离开页面时。
每个事件都是有用的：

* DOMContentLoaded 事件 —— DOM 已经准备好，因此事件处理器可以查找 DOM 节点，并初始化接口。
* load 事件 —— 外部资源加载完成后，我们就可以应用样式表，获取图像大小等。
beforeunload 事件 —— 用户即将离开：我们可以检查用户是否保存了修改，并询问他是否真的要离开。
* unload 事件 —— 用户几乎已经离开了，但是我们仍然可以启动一些操作，比如发送统计数据。
  当用户最终离开时，window 上的 unload 事件会被触发。在处理器中，我们只能做一些不会涉及到延迟或询问用户的简单事情。正是由于这个限制，它很少被使用。我们可以用 navigator.sendBeacon 来发送网络请求。
  document.readyState 是文档的当前状态，可以在 readystatechange 事件中跟踪状态变更：
  loading —— 文档正在被加载。
  interactive —— 文档被解析，大概是与 DOMContentLoaded 同时发生，而不是在它之前发生。
  complete —— 文档和资源被加载，大概是与 window.onload 同时发生，而不是在它之前发生。
  ### script async, defer
  #### defer
  defer 属性告诉浏览器它应该继续处理页面，并在“后台”下载脚本，然后等页面处理完成后才开始执行此脚本。
  async
  #### async 属性意味着脚本是完全独立的：

  页面不会等待异步脚本，它会继续处理页面并显示内容。
  DOMContentLoaded 和 async 脚本不会彼此等待：
  DOMContentLoaded 可能发生在异步脚本之前（此时异步脚本在页面加载完成后才加载完成）
  DOMContentLoaded 也可能发生在异步脚本之后（此时异步脚本可能很短或者是从 HTTP 缓存中加载的）
  其他脚本不会等待 async 脚本加载完成，同样 async 脚本也不会等待其他脚本。
  因此，如果我们有几个 async 脚本，它们可能按任意次序执行，总之是先加载完成的就先运行：
  #### 动态脚本（Dynamic scripts）
  我们也可以使用 JavaScript 动态地添加脚本：
  ``` javascript
  let script = document.createElement('script');
  script.src = "/article/script-async-defer/long.js";
  document.body.append(script); // (*)
  ```
  #### onload, onerror
  ``` javascript
  ```

  ### 窗口

  #### window.open()
  打开窗口,有三个参数
  url
  name 窗口的名字
  settingStr 窗口设置的字符串,例如
  'width=800,height=600,left=calc(50vw - 400px),top:calc(50vh - 300px)'
  #### window.close() 关闭窗口

  ### 同源
  如果两个 URL 具有相同的协议，域名和端口，则称它们是"同源"的。

  以下的几个 URL 都是同源的：

  http://site.com

  http://site.com/

  http://site.com/my/page.html

  但是下面几个不是：

  http://www.site.com (www. 域名与其他不同)

  http://site.org (.org 域名与其他不同)

  https://site.com (协议与其他不同: https)

  http://site.com:8080 (端口与其他不同：8080)

  ### iframe

  iframe.contentWindow 是对 <iframe> 里 window 的引用。

  iframe.contentDocument 是对 <iframe> 里的 document 对象的引用。

  获取 localstrage 
  JSON.parse(getItem('key'));
  setItem('key',JSON.stringify('value'))
  strage 事件 在 localstrage 储存的值

  ### css 动画

  CSS 提供了五个属性来描述一个过渡：

  transition-property
  transition-duration
  transition-timing-function
  transition-delay

  贝塞尔曲线
  cubic-bezier(0, 0, 1, 1)
  简写

  ease (0.25, 0.1, 0.25, 1.0)
  ease-in (0.42, 0, 1.0, 1.0)
  ease-out (0.42, 0, 1.0, 1.0)
  ease-in-out (0.42, 0, 0.58, 1.0)
  
  阶跃函数（Steps）
  ``` javascript
  #stripe.animate  {
    transform: translate(-90%);
    transition: transform 9s steps(9, start);
  }
  ```
  #### step(9, start)

  第二个参数控制元素变化的时间, start 就是在这段时间开头开始动画, end 就是再这段时间结尾开始动画

  #### transitionend 事件
  CSS 动画完成后，会触发 transitionend 事件。

  ### js 动画

  #### requestAnimationFrame 函数
  ``` javascript
  function animate({timing, draw, duration}) {
    let start = performance.now();
    requestAnimationFrame(function animate(time) {
      // timeFraction 从 0 增加到 1
      let timeFraction = (time - start) / duration;
      if (timeFraction > 1) timeFraction = 1;
      // 计算当前动画状态
      let progress = timing(timeFraction);
      draw(progress); // 绘制
      if (timeFraction < 1) {
        requestAnimationFrame(animate);
      }
    });
  }
  ```
  #### timing(timeFraction)
  时序函数，类似 CSS 属性 transition-timing-function，传入一个已过去的时间与总时间之比的小数（0 代表开始，1 代表结束），返回动画完成度（类似 Bezier 曲线中的 y）。
  #### draw(progress)
  获取动画完成状态并绘制的函数。值 progress = 0 表示开始动画状态，progress = 1 表示结束状态。

  这是实际绘制动画的函数。

  ##### 时序函数
  上文我们看到了最简单的线性时序函数。

  让我们看看更多。我们将尝试使用不同时序函数的移动动画来查看它们的工作原理。

  * n 次幂
  如果我们想加速动画，我们可以让 progress 为 n 次幂。

  例如，抛物线：
  ``` javascript
  function quad(timeFraction) {
    return Math.pow(timeFraction, 2)
  }
  ```

  * 圆弧

  函数：

  function circ(timeFraction) {
    return 1 - Math.sin(Math.acos(timeFraction));
  }

  * 反弹：弓箭射击

  此函数执行“弓箭射击”。首先，我们“拉弓弦”，然后“射击”。

  与以前的函数不同，它取决于附加参数 x，即“弹性系数”。“拉弓弦”的距离由它定义。

  代码如下：

  function back(x, timeFraction) {
    return Math.pow(timeFraction, 2) * ((x + 1) * timeFraction - x);
  }

  * 弹跳
  想象一下，我们正在抛球。球落下之后，弹跳几次然后停下来。

  bounce 函数也是如此，但顺序相反：“bouncing”立即启动。它使用了几个特殊的系数：
  ``` javascript
  function bounce(timeFraction) {
    for (let a = 0, b = 1, result; 1; a += b, b /= 2) {
      if (timeFraction >= (7 - 4 * a) / 11) {
        return -Math.pow((11 - 6 * a - 11 * timeFraction) / 4, 2) + Math.pow(b, 2)
      }
    }
  }
  ```
  * 伸缩动画
  另一个“伸缩”函数接受附加参数 x 作为“初始范围”。
  ``` javascript
  function elastic(x, timeFraction) {
    return Math.pow(2, 10 * (timeFraction - 1)) * Math.cos(20 * Math.PI * x / 3 * timeFraction)
  }
  ```

  #### 逆转：ease*
  我们有一组时序函数。它们的直接应用称为“easeIn”。

  有时我们需要以相反的顺序显示动画。这是通过“easeOut”变换完成的。

  easeOut
  在“easeOut”模式中，我们将 timing 函数封装到 timingEaseOut中：
  ``` javascript
  timingEaseOut(timeFraction) = 1 - timing(1 - timeFraction);
  // 接受时序函数，返回变换后的变体
  function makeEaseOut(timing) {
    return function(timeFraction) {
      return 1 - timing(1 - timeFraction);
    }
  }
  ```
  #### easeInOut
  * 我们还可以在动画的开头和结尾都显示效果。该变换称为“easeInOut”。

  * 给定时序函数，我们按下面的方式计算动画状态：
  ``` javascript
  if (timeFraction <= 0.5) { // 动画前半部分
    return timing(2 * timeFraction) / 2;
  } else { // 动画后半部分
    return (2 - timing(2 * (1 - timeFraction))) / 2;
  }
  封装器代码：

  function makeEaseInOut(timing) {
    return function(timeFraction) {
      if (timeFraction < .5)
        return timing(2 * timeFraction) / 2;
      else
        return (2 - timing(2 * (1 - timeFraction))) / 2;
    }
  }

  bounceEaseInOut = makeEaseInOut(bounce);
  ```

  ## 正则表达式
  ### 模式（Patterns）和修饰符（flags）

  #### 定义:

  regexp = new RegExp('pattern', 'flags);
  ``` javascript
  regexp = /pattern/ // 没有修饰符
  regexp = /pattern/gmi // 伴随修饰符 g ,m , i
  ```
  #### 搜索

  ``` javascript
  let str = "I love JavaScript!"; // 将在这里搜索

  let regexp = /love/;
  console.log( str.search(regexp) ); // 2
  ```

  new RegExp 允许从字符串中动态地构造模式

  #### 修饰符
  正则表达式的修饰符可能会影响搜索结果。

  在 JavaScript 中，有 5 个修饰符：

  i
  使用此修饰符后，搜索时不区分大小写: A 和 a 没有区别（具体看下面的例子）。
  g
  使用此修饰符后，搜索时会查找所有的匹配项，而不只是第一个（在下一章会讲到）。
  ``` javascript
  let str = "+7(903)-123-45-67";

  let regexp = /\d/g;

  console.log( str.match(regexp) ); // array of matches: 7,9,0,3,1,2,3,4,5,6,7
  ```
// let's make the digits-only phone number of them:
console.log( str.match(regexp).join('') ); // 79035419441
  m
  多行模式（详见章节 文章 "regexp-multiline" 未找到）。
  u
  开启完整的 unicode 支持。该修饰符能够修正对于代理对的处理。更详细的内容见章节 Unicode：修饰符 “u” 和 class \p{...}。
  y
  粘滞模式（详见 下一章节）

  #### 简写

  * \d 数字(0-9) 等于[0-9]
  * \s 空白字符包括, \t (制表符), \n (换行符), \v, \f, \r
  * \w 单词 包括: 拉丁字母, 数字, 下划线 _ 

  相反的写法
  * \D
  * \S
  * \W
  大写即可,即上述小写相反的部分

  . 代表是所有的对象 (包括空白符号, 不包括空和回车)
  可以使用[/s/S]来表示真正的所有对象

  以下是主要的字符类别和它们对应的子类别：

  * 字母（Letter） L:
    * 小写（lowercase） Ll
    * 修饰（modifier） Lm,
    * 首字母大写（titlecase） Lt,
    * 大写（uppercase） Lu,
    * 其它（other） Lo。
  * 数字（Number） N:
    * 十进制数字（decimal digit） Nd,
    * 字母数字（letter number） Nl,
    * 其它（other） No。
  * 标点符号（Punctuation） P:
    * 链接符（connector） Pc,
    * 横杠（dash） Pd,
    * 起始引用号（initial quote） Pi,
    * 结束引用号（final quote） Pf,
    * 开（open） Ps,
    * 闭（close） Pe,
    * 其它（other） Po。
    * 标记（Mark） M (accents etc):
    * 间隔合并（spacing combining） Mc,
    * 封闭（enclosing） Me,
    * 非间隔（non-spacing） Mn。
    * 符号（Symbol） S:
    * 货币（currency） Sc,
    * 修饰（modifier） Sk,
    * 数学（math） Sm,
    * 其它（other） So。
    * 分隔符（Separator） Z:
    * 行（line） Zl,
    * 段落（paragraph） Zp,
    * 空格（space） Zs。
    * 其它（Other） C:
    * 控制符（control） Cc,
    * 格式（format） Cf,
    * 未分配（not assigned） Cn,
    * 私有（private use） Co,
    * 代理伪字符（surrogate） Cs。

  我们可以查找具有某种属性的字符，写作 \p{…}。为了顺利使用 \p{…}，一个正则表达式必须使用修饰符 u。
  ``` javascript
  let str = "A ბ ㄱ";

  console.log( str.match(/\p{L}/gu) ); // A,ბ,ㄱ
  console.log( str.match(/\p{L}/g) ); // null（没有匹配的文本，因为没有修饰符“u”）
  ```

  ### 开始和结束符 ^, $

  多行模式通过 ^$ 获取每行末尾的字符

  ### 词边界：\b
  词边界 \b 是一种检查，就像 ^ 和 $ 一样。
  有三种不同的位置可作为词边界：

  在字符串开头，如果第一个字符是单词字符 \w。
  在字符串中的两个字符之间，其中一个是单词字符 \w，另一个不是。
  在字符串末尾，如果最后一个字符是单词字符 \w。
  ### 转义,前面加斜杠

  ### 集合
  在方括号 […] 中的几个字符或者字符类意味着“搜索给定的字符中的任意一个”。

  #### 集合
  比如说，[eao] 意味着查找在 3 个字符 'a'、'e' 或者 `‘o’ 中的任意一个。

  这被叫做一个集合。集合可以在正则表达式中和其它常规字符一起使用。
  #### 范围
  方括号也可以包含字符范围。

  比如说，[a-z] 会匹配从 a 到 z 范围内的字母，[0-5] 表示从 0 到 5 的数字。
  \d – is the same as [0-9],
  \w – is the same as [a-zA-Z0-9_],
  \s – is the same as [\t\n\v\f\r ], plus few other rare unicode space characters.

  #### 在 […] 中不转义
  在方括号表示中，绝大多数特殊字符可以在不转义的情况下使用：

  表示一个点符号 '.'。
  表示一个加号 '+'。
  表示一个括号 '( )'。
  在开头或者结尾表示一个破折号（在这些位置该符号表示的就不是一个范围） `pattern:’-’。
  在不是开头的位置表示一个插入符号（在开头位置该符号表示的是排除）'^'。
  表示一个开口的方括号符号 '['。

  ### 数量 {n}

  #### 确切的位数 {5}
  ``` javascript

  接下来的例子将会查找一个五位数的数字：

  console.log( "I'm 12345 years old".match(/\d{5}/) ); //  "12345"
  ```
  #### 某个范围的位数：{3,5}
  ``` javascript
  我们可以将限制范围的数字放入括号中，来查找位数为 3 至 5 位的数字：\d{3,5}

  console.log( "I'm not 12, but 1234 years old".match(/\d{3,5}/) ); // "1234"
  ```

  缩写
  大多数常用的量词都可以有缩写：

  + 相当于 {1,}

  例如，\d+ 用来查找所有数字：
  ``` javascript
  let str = "+7(903)-123-45-67";

  console.log( str.match(/\d+/g) ); // 7,903,123,45,67
  ```

  ? 相当于 {0,1}

  代表“零个或一个”，相当于 {0,1}。换句话说，它使得符号变得可选。

  例如，模式 ou?r 查找 o，后跟零个或一个 u，然后是 r。

  所以他能够在 color 中找到 or，以及在 colour 中找到 our：
  ``` javascript
  let str = "Should I write color or colour?";

  console.log( str.match(/colou?r/g) ); // color, colour
  ```
  * {0,}
  代表着“零个或多个”，相当于 {0,}。也就是说，这个字符可以多次出现或不出现。

  接下来的例子将要寻找一个后跟任意数量的 0 的数字：
  ``` javascript
  console.log( "100 10 1".match(/\d0*/g) ); // 100, 10, 1
  ```

  ### 贪婪量词
  正则表达式默认 贪婪模式
  * 正则表达式看上去可能是这样的：/".+"/g。这个表达式的意思是：我们要查找这样一个句子，一个引号后跟一个或多个字符，然后以另一个引号结尾。

  …但如果我们试着在一个如此简单的例子中去应用它…
  ``` javascript
  let reg = /".+"/g;

  let str = 'a "witch" and her "broom" is one';

  console.log( str.match(reg) ); // "witch" and her "broom"
  ```
  …我们会发现它的运行结果与预期不同！

  它直接找到了一个匹配结果："witch" and her "broom"，而不是找到两个匹配结果 "witch" 和 "broom"。

  这可被称为“贪婪是万恶之源”。

  #### 懒惰模式
  懒惰模式中的量词与贪婪模式中的是相反的。它想要“重复最少次数”。

  我们能够通过在量词之后添加一个问号 '?' 来启用它，所以匹配模式变为 *? 或 +?，甚至将 '?' 变为 ??。

  这么说吧：通常，一个问号 ? 就是一个它本身的量词（0 或 1），但如果添加另一个量词（甚至可以是它自己），就会有不同的意思 —— 它将匹配的模式从贪婪转为懒惰。

  正则表达式 /".+?"/g 正如预期工作：它找到了 "witch" 和 "broom"：
  ### 替代方法

  在正则表达式中，通常有多种方法来达到某个相同目的。

  在用例中，我们能够在不启用懒惰模式的情况下用 "[^"]+" 找到带引号的字符串：
  ``` javascript
  let reg = /"[^"]+"/g;

  let str = 'a "witch" and her "broom" is one';

  console.log( str.match(reg) ); // witch, broom
  ```

  捕捉组

  例如: gogogo
  ``` javascript
  console.log( 'Gogogo now!'.match(/(go)+/i) ); // "Gogogo"
  ```

  match 方法:
  如果正则表达式,有括号,则

  match 方法 返回一个数组, (注意使用 g 修饰符,将无法返回数组,只会返回匹配的字符串)

  [0] 代表匹配的字符串
  [1] 代表第一个括号里的内容
  [2] 代表第二个括号里的内容

  matchAll 方法, 使用 g 修饰符, 按上面的操作全局匹配,返回一个可迭代对象

  ``` javascript
  let results = '<h1> <h2>'.matchAll(/<(.*?)>/gi);

  let [tag1, tag2] = results;

  console.log( tag1[0] ); // <h1>
  console.log( tag1[1] ); // h1
  console.log( tag1.index ); // 0
  console.log( tag1.input ); // <h1> <h2>
  ```

  捕获替代, 如果我们需要括号里面捕获的内容, 则使用 $n 
  (n 为序号)

  ``` javascript
  let str = "John Bull";
  let regexp = /(\w+) (\w+)/;

  console.log( str.replace(regexp, '$2, $1') ); // Bull, John
  ```

  可以使用 $<name> 来为捕获 添加名字(前面要写 ? 号)
  ``` javascript
  let regexp = /(?<year>[0-9]{4})-(?<month>[0-9]{2})-(?<day>[0-9]{2})/g;

  let str = "2019-10-30, 2020-01-01";

  console.log( str.replace(regexp, '$<day>.$<month>.$<year>') );
  // 30.10.2019, 01.01.2020
  ```

  使用 ?: 匹配括号里的内容,但是并不放在数组里
  ``` javascript
  let str = "Gogogo John!";

  // ?: exludes 'go' from capturing
  let regexp = /(?:go)+ (\w+)/i;

  let result = str.match(regexp);

  console.log( result[0] ); // Gogogo John (full match)
  console.log( result[1] ); // John
  console.log( result.length ); // 2 (no more items in the array)
  ```

  在正则表达式中使用捕获

  例子: 
  ``` javascript
  let str = `He said: "She's the one!".`;

  let regexp = /['"](.*?)['"]/g;

  // The result is not what we'd like to have
  console.log( str.match(regexp) ); // "She'
  ```
  ``` javascript
  let str = `He said: "She's the one!".`;

  let regexp = /(['"])(.*?)\1/g;

  console.log( str.match(regexp) ); // "She's the one!"
  ```

  给引用加名字

  \k<name>

  ``` javascript
  let str = `He said: "She's the one!".`;

  let regexp = /(?<quote>['"])(.*?)\k<quote>/g;

  console.log( str.match(regexp) ); // "She's the one!"
  ```

  ### 选择 OR |
  通常用括号括住要选择的部分: before(XXX|YYY)after

  时间的正则表达式:

  小时和分钟: ([01]/d|2[0-4]): [0-5]/d

  ### 前瞻断言与后瞻断言
  #### 前瞻断言
  * 前瞻肯定断言 x(?=y) 匹配后面有 y 的 x
  ``` javascript
  let str = "1 turkey costs 30€";

  console.log( str.match(/\d+(?=€)/) ); // 30 （正确地跳过了单个的数字 1）
  ```
  * 前瞻否定断言x(?!y) 匹配后面没有 y 的 x
  #### 后瞻断言
  后瞻肯定断言：(?<=y)x, 匹配 x, 仅在前面是 y 的情况。
  后瞻否定断言：(?<!y)x, 匹配 x, 仅在前面不是 y 的情况。
  
  * 一般来说，环视断言括号中（前瞻和后瞻的通用名称）的内容不会成为匹配到的一部分结果。

  例如：在模式 \d+(?!€) 中，€ 符号就不会出现在匹配结果中。

  但是如果我们想要捕捉整个环视表达式或其中的一部分，那也是有可能的。只需要将其包裹在另加的括号中。

  例如，这里货币符号 (€|kr) 和金额一起被捕获了：
  ``` javascript
  let str = "1 turkey costs 30€";
  let reg = /\d+(?=(€|kr))/; // €|kr 两边有额外的括号

  console.log( str.match(reg) ); // 30, €
  ```

  后瞻断言于此相同

  ### stick flag 'y' 用于 在确定位置检查字符串
  ``` javascript
  let str = 'let varName = "value"';

  let regexp = /\w+/y;

  regexp.lastIndex = 3;
  alert( regexp.exec(str) ); // null (there's a space at position 3, not a word)

  regexp.lastIndex = 4;
  alert( regexp.exec(str) ); // varName (word at position 4)
  ```

  ### 正则表达式方法

  #### str.match(regexp)
  三种情况:
  * 如果正则表达式没有 g 修饰符,返回第一个找到的字符
  * 如果有 g ,返回包含全部符合表达式字符的数组
  * 没找到返回 null

  如果不想有 null,则需写成
  ``` javascript
  let result = str.match(regexp) || [];
  ```
  #### str.matchAll(regexp)
  返回可迭代对象,可用Array.from 转化
  ``` javascript
  let str = '<h1>Hello, world!</h1>';
  let regexp = /<(.*?)>/g;

  let matchAll = str.matchAll(regexp);

  alert(matchAll); // [object RegExp String Iterator], not array, but an iterable

  matchAll = Array.from(matchAll); // array now

  let firstMatch = matchAll[0];
  alert( firstMatch[0] );  // <h1>
  alert( firstMatch[1] );  // h1
  alert( firstMatch.index );  // 0
  alert( firstMatch.input );  // <h1>Hello, world!</h1>
  ```
  #### str.split(regexp|substr, limit)
  ``` javascript
  alert('12-34-56'.split('-')) // array of [12, 34, 56]
  alert('12, 34, 56'.split(/,\s*/)) // array of [12, 34, 56]
  ```
  #### str.search(regexp) 
  查找函数
  找到字符串, 返回所在序号
  没找到,返回 -1
  #### str.replace(str|regexp, str|func)
  最简单的应用:(替换字符)
  ``` javascript
  // replace a dash by a colon
  alert('12-34-56'.replace("-", ":")) // 12:34-56
  // 若要全局替换,则 需要正则表达式
  alert( '12-34-56'.replace( /-/g, ":" ) )  // 12:34:56
  ```
  $&	inserts the whole match
  $`	inserts a part of the string before the match
  $'	inserts a part of the string after the match
  $n	if n is a 1-2 digit number, inserts the contents of n-th capturing group, for details see Capturing groups
  $<name>	inserts the contents of the parentheses with the given name, for details see Capturing groups
  $$	inserts character $

  第二个参数如果为函数,则
  函数有以下参数
  match – match所得的记过,
  p1, p2, ..., pn 被捕获的,
  offset – match 所开始的位置,
  input – 原字符串,
  groups 一个对象

  如果正则表达式没有捕获,则只有三个参数 str, offset, input
  例如: 
  下面的例子让 html 和 css 大写
  ``` javascript
  let str = "html and css";

  let result = str.replace(/html|css/gi, str => str.toUpperCase());

  alert(result); // HTML and CSS

  alert("Ho-Ho-ho".replace(/ho/gi, (match, offset) => offset)); // 0-3-6
  ```

  使用捕获的内容
  ``` javascript
  let str = "John Smith";

  let result = str.replace(/(\w+) (\w+)/, (match, name, surname) => `${surname}, ${name}`);

  alert(result); // Smith, John
  ```

  #### regexp.exec(str)

  * 正则表达式没有 g 修饰符, 与 match() 相同
  * 正则表达式有 g 修饰符
    regexp.exec(str) 返回一个对象
    包括现在查找到的字符串,和 字符串后面一位的序号,用于下一次继续使用该方法,可用于迭代器
  ``` javascript
  let str = 'More about JavaScript at https://javascript.info';
  let regexp = /javascript/ig;

  let result;

  while (result = regexp.exec(str)) {
    alert( `Found ${result[0]} at position ${result.index}` );
    // Found JavaScript at position 11, then
    // Found javascript at position 33
  }
  ```
  ##### 通过给正则表达式,设置 lastIndex 属性,来查找特定位置的字符串
  ``` javascript
  let str = 'Hello, world!';

  let regexp = /\w+/g; // without flag "g", lastIndex property is ignored
  regexp.lastIndex = 5; // search from 5th position (from the comma)

  alert( regexp.exec(str) ); // world
  ```

  ##### y 修饰符,如果有y修饰符,设置了 lastIndex 后, 只会在该位置来查找字符串,没找到返回 null 
  ``` javascript
  let str = 'Hello, world!';

  let regexp = /\w+/y;
  regexp.lastIndex = 5; // search exactly at position 5

  alert( regexp.exec(str) ); // null
  ```
  #### regexp.test(str)
  查找字符串, 找到返回下标,找不到返回 -1 .
  * 如果字符串有 g 修饰符,则返回一个对象有 lastIndex ,即和 exec() 相同
  ``` javascript
  let regexp = /love/gi;

  let str = "I love JavaScript";

  // start the search from position 10:
  regexp.lastIndex = 10;
  alert( regexp.test(str) ); // false (no match)
  ```