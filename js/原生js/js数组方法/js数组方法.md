
### 前言:

数组在 js 中,有举足轻重的作用,因为几乎所有的类型都可以转化成数组,
并且它还拥有一些非常出色的函数,今天拖欠了很久的数组在这里总结一下.

### 创建数组的方法:
#### 用array创建:

  ``` javascript
    // 创建一个空数组
    var arr = new Array();
    console.log(arr);
    // 创建一个一项的数组
    var arr1 = new Array(1); // 这个1的意思是创建一个长度为1的空数组
    console.log(arr1);
    // 创建字符串数组
    var arr2 = new Array("join", "allen", "fileaccent");
    console.log(arr2);
  ```

#### 用 [ ] 创建

  ``` javascript
    // 创建一个空数组
    var arr3 = [];
    console.log(arr3);
    var arr4 = [1];
    console.log(arr4);
    var arr5 = ["join", "allen", "fileaccent"];
    console.log(arr5);
  ```

  这里发现一个有趣的事情,本来arr1与arr4应该是一样的,可是他们却产生了不同的结果,可以在后面的学习中,学习一下!

  ![js数组定义](img\js数组定义.PNG)

### 数组的原型方法
  #### join ( )  连接函数
  // 连接函数 将数组连接成特定的字符串
  ``` javascript
    arr5 = ["join", "allen", "fileaccent"];
    console.log(arr5.join()); // join,allen,fileaccent (默认输出)
    console.log(arr5.join('')); // 输出 joinallenfileaccent
    console.log(arr5.join(',')); // 输出 join,allen,fileaccent
    console.log(arr5.join(' ')); // 输出 join allen fileaccent
  ```
  <span style="color:rgb(5,56,56);">
  join后面的括号里面是连接字符串中间的连接部分,<br/>
  希望字符串中间什么都没有要加上 ' ',如果为空则默认加上 , 号 
  </span>

  #### split ( ) 切片函数
  // 切片函数 将字符串切成数组(为 join() 的逆过程)
  ``` javascript
    arr5 = ["join", "allen", "fileaccent"];

    console.log('join,allen,fileaccent'.split()); 

    // ["join,allen,fileaccent"](默认输出)

    console.log('joinallenfileaccent'.split('')); 

    // 输出 ["j", "o", "i", "n", "a", "l", "l", "e", "n", "f", "i", "l", "e", "a", "c", "c", "e", "n", "t"]

    console.log('join,allen,fileaccent'.split(',')); 

    // 输出 ["join", "allen", "fileaccent"]

    console.log('join allen fileaccent'.split(' ')); 

    // 输出 ["join", "allen", "fileaccent"]
  ```

  与join不同的是,如果split后面的括号中没有东西,那么他会把整个字符串变成一个长度为1, 第一项为该字符串的数组.

  如果括号里为 '' (为空,不是空格),那么他会一个一个字母的分割开来.

  如果为其他字符,则为join()的逆过程

  #### 上述两种结合

  name上述两种结合就可以实现一些,很好的操作

  比如可以:反序排列字母
    
  ``` javascript
    var str = "faflafjlac";
    console.log(str.split('').reverse().join('')); // 输出 caljfalfaf
  ```
  其他骚操作任你想象

  #### push () 尾部添加函数

  可以接收任意数量的参数，把它们逐个添加到数组末尾，并返回修改后数组的长度.
  ``` javascript
    var arr = ['arr', 'allen','fileaccent'];
    console.log(arr.push()); // 3 可以得到数组长度,虽然我感觉没人这么闲
    console.log(arr); // ["arr", "allen", "fileaccent"]
    console.log(arr.push('405')); // 4
    console.log(arr); //  ["arr", "allen", "fileaccent", "405"]
    // 骚操作
    // var arr1 = undefined;
    // console.log(arr1.push()); 
    // console.log(arr1); 
    // 报错和 length 一个逼样
  ```
  #### pop () 尾部删除函数

  不需要接受参数,返回被删除的项

  ``` javascript
    console.log(arr.pop()); // 405
    console.log(arr); 
    // ["arr", "allen", "fileaccent"]
  ```
  #### shift () 去头函数 
  (与pop的区别只是,一个作用在头部,一个作用在尾部)
  ``` javascript
    console.log(arr.shift()); // arr
    console.log(arr); // ["allen", "fileaccent"]
  ```
  #### unshift () 添头函数 
  (与pop的区别只是,一个作用在头部,一个作用在尾部)
  ``` javascript
    console.log(arr.unshift('arr')); // 3 返回长度,hhh
    console.log(arr); // ["arr", "allen", "fileaccent"]
  ```
  #### sort () 排序函数

  默认以ASCII值排序

  返回改变后的数组

  原数组也被改变(有点反人类, 要注意!)

  ``` javascript
    console.log(arr.sort()); // ["allen", "arr", "fileaccent"]
    console.log(arr); // ["allen", "arr", "fileaccent"]
  ```

  如果想让数组按照自己想要的方式排序可以传入一个数组

  ``` javascript
    var arr1 = [12,45,31,56,313,45,12];
    // 你想排序数字,但是默认会排序ASCII值,
    // 那么就要使用下面的格式
    console.log(arr1.sort(function(a, b) {
      console.log('a =' + a);
      console.log('b =' + b);
      console.log(arr1);
      return a - b;
    })); // [12, 12, 31, 45, 45, 56, 313]
  ```
  ![js方法sort](img\js方法sort.PNG)
    
  return a - b;

  从小到大排列;

  return b - a;

  从大到小排列;

  通过这张图发现 它做的一个数字排序的过程(有点诡异,和我们想的不太一样);

  以从小到大排序为例:

  function 函数接受两个参数 a, b ,

  a,b分别为数组的相邻两项.

  如果return 返回负数不交换,

  返回正数就将小的那个插到前面适合的位置,重复直到数组从小到大排列

  #### reverse() 反转函数

  反转数组项的顺序

  ``` javascript
    var arr1 = ['fileaccent', 'yuri', 'allen'];
    console.log(arr1.reverse()); // ["allen", "yuri", "fileaccent"]
    console.log(arr1); // ["allen", "yuri", "fileaccent"]
  ```

  该方法返回改变后的数组,原数组也改变,这点和 sort() 相同

  #### concat() 追加函数

  向数组后添加项目不只一个

  ``` javascript
    var arr1 = [1,2,3,4];
    var arr2 = [5,6,89,[4,7]];
    console.log(arr1.concat(5,[8,9])); // [1, 2, 3, 4, 5, 8, 9]
    console.log(arr1.concat(5,[[8,9]])); // [1, 2, 3, 4, 5, Array(2)]
    console.log(arr1.concat(arr2)); // [1, 2, 3, 4, 5, 6, 89, Array(2)]
    console.log(arr1); // [1, 2, 3, 4]
    console.log(arr2); // [5, 6, 89, Array(2)]
  ```
  <span style="color:rgb(200,45,124)">注意concat不改变原数组!</span>

  concat 后面的括号中,可以传入单个字符,可以传一个数组,他们都会被添加到最后,若要添加一个数组的项,则要传入[[8,9]];

  #### slice () 截取函数

  返回从原数组中指定开始下标到结束下标之间的项组成的新数组

  ``` javascript
    var arr1 = [1,4,5,6,9,14];
    console.log(arr1.slice(1)); // [4, 5, 6, 9, 14]
    // 若只有一个参数则获取后面的所有元素
    console.log(arr1); // [1,4,5,6,9,14]
    console.log(arr1[1]); // 1
    console.log(arr1[5]); // 14
    console.log(arr1.slice(1,5)); // [4, 5, 6, 9]
    // 第一个参数是开始位置,返回的数组包括它,

    // 第两个参数是结束位置,返回的数组不包括它,返回第二个参数之前的元素

    // 注意该函数不会改变原数组
  ```

  #### splice () 万能函数

  添加删除样样都可以做, 注意会改变原数组

  ``` javascript
    var arr1 = [1,4,5,6,9,14];
    console.log(arr1.splice(1,2, 49, 34)); // [4, 5]
  ```
  第一个参数是操作元素的序号, 比如上面就是从 元素 4 开始操作;

  第二个参数是删除的个数,从选定的元素开始删除,选定的元素也要被删,上述表达式删除了两个元素;
  第三个以后的参数是被添加的元素,这里在该位置添加了 49 和 34

  函数的返回值,为被删除元素组成的数组

  ``` javascript
    console.log(arr1); // [1, 49, 34, 6, 9, 14]
  ```

  原数组的两个元素被删除,并添加了两个元素

  这里能不能第三个参数传入数组呢

  ``` javascript
    var arr2 = [10, 20 ,30]
    console.log(arr1.splice(1,2,arr2)); // [49, 34]
    console.log(arr1); // [1, Array(3), 6, 9, 14]
  ```

  和我们想的不太一样

  如何把数组接在相应的位置,等后面有时间讨论

  #### indexOf () 和 lastIndexOf () 查找函数

  查找元素在数组中的位置,如果找到了返回序号,找 不到返回 -1

  第一个参数是查找的元素,

  第二个参数是开始查找的位置.

  第三个参数是查找的位数,从开始位置查找几位;

  indexOf 从左到右 没有第二个参数默认从开头开始

  lastIndexOf 从右到左 没有第二个参数默认从结尾开始

  ``` javascript 
    var arr1 = [1,4,5,6,9,14];
    console.log(arr1.indexOf(5)); // 2
    console.log(arr1.indexOf(5,4)); // -1
    console.log(arr1.lastIndexOf(5)); // 2
    console.log(arr1.lastIndexOf(5,0,2)); // -1
    console.log(arr1.lastIndexOf(5,1)); // -1
  ```

  #### forEach(), map() 遍历函数
  接受一个类型为函数的参数

  第一个参数为该项的值

  第二个参数为该项的序号

  第三个参数为数组本身

  ``` javascript
    var arr1 = [1,4,2,4,5,7,8,10];
    arr1.forEach(function(val, index, arr1) {
      val = val * val;
      console.log(val); // 1
      console.log(index); // 0
      console.log(arr1); // [1,4,2,4,5,7,8,10]
      // 以第一项为例
    })
    console.log(arr1); // [1, 4, 2, 4, 5, 7, 8, 10]
    var arr2 = [1,4,2,4,5,7,8,10];
    console.log(arr2.map(function(val) {
      return val * val;
    })); // [1, 16, 4, 16, 25, 49, 64, 100]
    console.log(arr2); // [1, 4, 2, 4, 5, 7, 8, 10]
  ```
  从上述的测试我们可以看到:

  forEach只能读取信息,不能改变该数组的值,只返回undefined,
  故只可以进行,求和等等基本操作

  map可以操作数组, 返回操作后的数组,不改变原数组,比较强大!

  #### filter() 过滤函数
  ``` javascript
  arr3 = ['a',1,3,46,'b'];
  console.log(arr3.filter((val, item) => {
    return typeof(val) === 'string'
  })) // ["a", "b"]
  ```
  filter()同样接受一个函数参数

  如果返回 true,则保存该项,返回值为所有保存项的数组,
  其余和上述的函数相同

  #### every() some() 整体判断函数

  every()判断每项是否符合条件,如果符合则返回 true ,否则返回 false

  some()判断是否有项符合条件,如果有返回 true, 否则返回 false

  ``` javascript
    var arr1 = [1,5,5,7,8,9,11];
    console.log(arr1.every((val) => {
      return val < 10;
    }))
    console.log(arr1.some((val) => {
      return val < 10;
    }))
  ```

  #### reduce() reduceRight() 递归函数

  这两个方法都会实现迭代数组的所有项，然后构建一个最终返回的值。

  reduce()方法从数组的第一项开始，逐个遍历到最后,

  而 reduceRight()则从数组的最后一项开始，向前遍历到第一项。

  这两个方法都接收两个参数：

  一个在每一项上调用的函数和（可选的）作为归并基础的初始值。

  传给 reduce()和 reduceRight()的函数接收 4 个参数：

  前一个值、当前值、项的索引和数组对象。

  这个函数返回的任何值都会作为第一个参数自动传给下一项。

  第一次迭代发生在数组的第二项上，因此第一个参数是数组的第一项，第二个参数就是数组的第二项。

  下面代码用reduce()实现数组求和.

  ``` javascript
  var values = [1,2,3,4,5];
  var sum = values.reduceRight(function(prev, cur, index, array){
  return prev + cur;
  });
  console.log(sum); // 15
  ```

  所有数组方法到此结束
