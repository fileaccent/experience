
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

  与join不同的是,如果split后面的括号中没有东西,那么他会把整个字符串变成一个长度为1, 第一项为该字符串的数组.如果括号里为 '' (为空,不是空格),那么他会一个一个字母的分割开来如果为其他字符,则为join()的逆过程

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
    
  通过这张图发现 它做的一个数字排序的过程(有点诡异,和我们想的不太一样);

  return a - b;

  从小到大排列;

  return b - a;

  从大到小排列;

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

  #### indexOf () 和 lastIndexOf ()

  查找元素在数组中的位置,如果找到了返回序号,找不到返回 -1 
  第一个参数是查找的元素,
  第二个是开始查找的位置.
  indexOf 从左到右 没有第二个参数默认从开头开始
  lastIndexOf 从右到左 没有第二个参数默认从结尾开始
  ``` javascript 
    var arr1 = [1,4,5,6,9,14];
    console.log(arr1.indexOf(5)); // 2
    console.log(arr1.indexOf(5,4)); // -1
    console.log(arr1.lastIndexOf(5)); // 2
    console.log(arr1.lastIndexOf(5,1)); // -1
  ```