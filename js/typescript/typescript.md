### 编译方法
tsc [filename] --strictNullChecks
### 基本类型:
``` typescript
// 布尔值
let isDone: boolean = false;
// 数字
let decLiteral: Number = 6;
// 字符串
let str: string = "开始";
/// 数组
let list: number[] = [1, 2, 3];
// 元组
let x: [string, number];
// 枚举
enum Color = {Red, Green, Blue};
// 任意值
let notSure:any = 4;
// 空值
function warnUser():void {
  alert('This is my warning message');
}
// null 和 undefined
使用 --strictNullChecks 来防止 null,undefined 赋给 除 null undefined void 的其他类型
// never
// 其他依次类推

```

### 接口(对象的类型)
接口可以检测对象的数据类型
``` typescript
interface LabelledValue {
  label: string;
}

function printLabel(labelledObj: LabelledValue) {
  console.log(labelledObj.label);
}

let myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj);
```

接口也可以有可选参数
可选参数需要加 ? 号
``` typescript
interface SquareConfig {
  color?: string;
  width?: number;
}
```
注意: 如果传入的对象里, 没有 color 和 width 的任意一个,那么默认 typescript 报错
``` typescript
interface SquareConfig {
    color?: string;
    width?: number;
}

function createSquare(config: SquareConfig): { color: string; area: number } {
    // ...
}

let mySquare = createSquare({ colour: "red", width: 100 });
```
解决方法:
1. 类型断言(使用 as 手动告诉浏览器,这是可以的)
``` typescript
let mySquare = createSquare({ width: 100, opacity: 0.5 } as SquareConfig);
```
2. 字符串索引签名
``` typescript
interface SquareConfig {
    color?: string;
    width?: number;
    [propName: string]: any;
}
```
``` typescript
interface Point {
    readonly x: number;
    readonly y: number;
}
```
只读属性
属性名前面加 readonly
``` typescript
interface Point {
    readonly x: number;
    readonly y: number;
}
```

#### 函数类型

``` typescript
interface SearchFunc {
  (source: string, subString: string): boolean;
}
let mySearch: SearchFunc;
mySearch = function(src, sub) {
    let result = src.search(sub);
    return result > -1;
}
```

#### 类类型
``` typescript
interface ClockInterface {
    currentTime: Date;
}

class Clock implements ClockInterface {
    currentTime: Date;
    constructor(h: number, m: number) { }
}
```

#### 继承接口
``` typescript
interface Shape {
    color: string;
}

interface Square extends Shape {
    sideLength: number;
}

let square = <Square>{};
square.color = "blue";
square.sideLength = 10;
// 可继承多个接口
interface Shape {
    color: string;
}

interface PenStroke {
    penWidth: number;
}

interface Square extends Shape, PenStroke {
    sideLength: number;
}

let square = <Square>{};
square.color = "blue";
square.sideLength = 10;
square.penWidth = 5.0;
```
### 类
``` typescript
class Greeter {
    greeting: string;
    constructor(message: string) {
        this.greeting = message;
    }
    greet() {
        return "Hello, " + this.greeting;
    }
}

let greeter = new Greeter("world");
```
#### 继承
``` typescript
class Animal {
    move(distanceInMeters: number = 0) {
        console.log(`Animal moved ${distanceInMeters}m.`);
    }
}

class Dog extends Animal {
    bark() {
        console.log('Woof! Woof!');
    }
}

const dog = new Dog();
dog.bark();
dog.move(10);
dog.bark();
```

* 使用 super() 来继承父类的方法
``` typescript
class Animal {
    name: string;
    constructor(theName: string) { this.name = theName; }
    move(distanceInMeters: number = 0) {
        console.log(`${this.name} moved ${distanceInMeters}m.`);
    }
}

class Snake extends Animal {
    constructor(name: string) { super(name); }
    move(distanceInMeters = 5) {
        console.log("Slithering...");
        super.move(distanceInMeters);
    }
}

class Horse extends Animal {
    constructor(name: string) { super(name); }
    move(distanceInMeters = 45) {
        console.log("Galloping...");
        super.move(distanceInMeters);
    }
}

let sam = new Snake("Sammy the Python");
let tom: Animal = new Horse("Tommy the Palomino");

sam.move();
tom.move(34);
```

公共,私有 与 受保护

* 默认为 public

* private
若变量或函数被设置为 private 则只能在类内使用
``` typescript
class Animal {
    private name: string;
    constructor(theName: string) { this.name = theName; }
}

new Animal("Cat").name; // 错误: 'name' 是私有的.
```
* protected
只能在类和被继承的类中使用

#### 存取器
下面这个版本里，我们先检查用户密码是否正确，然后再允许其修改员工信息。 我们把对fullName的直接访问改成了可以检查密码的set方法。 我们也加了一个get方法，让上面的例子仍然可以工作。
``` typescript
let passcode = "secret passcode";

class Employee {
    private _fullName: string;

    get fullName(): string {
        return this._fullName;
    }

    set fullName(newName: string) {
        if (passcode && passcode == "secret passcode") {
            this._fullName = newName;
        }
        else {
            console.log("Error: Unauthorized update of employee!");
        }
    }
}

let employee = new Employee();
employee.fullName = "Bob Smith";
if (employee.fullName) {
    alert(employee.fullName);
}
```

#### 抽象类

抽象类 是 类的一个样式
继承的类需要照着 抽象类去书写
``` typescript
abstract class Department {

    constructor(public name: string) {
    }

    printName(): void {
        console.log('Department name: ' + this.name);
    }

    abstract printMeeting(): void; // 必须在派生类中实现
}

class AccountingDepartment extends Department {

    constructor() {
        super('Accounting and Auditing'); // 在派生类的构造函数中必须调用 super()
    }

    printMeeting(): void {
        console.log('The Accounting Department meets each Monday at 10am.');
    }

    generateReports(): void {
        console.log('Generating accounting reports...');
    }
}

let department: Department; // 允许创建一个对抽象类型的引用
department = new Department(); // 错误: 不能创建一个抽象类的实例
department = new AccountingDepartment(); // 允许对一个抽象子类进行实例化和赋值
department.printName();
department.printMeeting();
department.generateReports(); // 错误: 方法在声明的抽象类中不存在
```
抽象类中没有generateReports(),在子类中声明是错误的

#### 把类当做接口使用
``` typescript
class Point {
    x: number;
    y: number;
}

interface Point3d extends Point {
    z: number;
}

let point3d: Point3d = {x: 1, y: 2, z: 3};
```

### 函数
完整函数类型
现在我们已经为函数指定了类型，下面让我们写出函数的完整类型。
``` typescript
let myAdd: (x:number, y:number) => number =
    function(x: number, y: number): number { return x + y; };
```
#### 解释:
前半句 

let myAdd: (x:number, y:number) => number

变量 myAdd 是一个函数 ,该函数有两个数字参数,并且返回一个数字

后半句

function(x: number, y: number): number { return x + y; };
正常的 js 函数,但是为参数和返回值,都设置了类型
#### 可以只在等号一边设置类型

#### 可选参数和默认参数
##### 可选参数
lastName?: string
##### 默认参数
lastname = 'john
#### 剩余运算符
参考 ES6 剩余运算符

### this 
参考 ES6 
如果对象,要使用 对象作为 this 需要给函数设置 this:<对象名>

#### 重载函数(改变参数类型)
``` typescript
let suits = ["hearts", "spades", "clubs", "diamonds"];
// 重载函数,指定函数的参数类型和返回类型
function pickCard(x: {suit: string; card: number; }[]): number;
function pickCard(x: number): {suit: string; card: number; };
function pickCard(x): any {
    // Check to see if we're working with an object/array
    // if so, they gave us the deck and we'll pick the card
    if (typeof x == "object") {
        let pickedCard = Math.floor(Math.random() * x.length);
        return pickedCard;
    }
    // Otherwise just let them pick the card
    else if (typeof x == "number") {
        let pickedSuit = Math.floor(x / 13);
        return { suit: suits[pickedSuit], card: x % 13 };
    }
}

let myDeck = [{ suit: "diamonds", card: 2 }, { suit: "spades", card: 10 }, { suit: "hearts", card: 4 }];
let pickedCard1 = myDeck[pickCard(myDeck)];
alert("card: " + pickedCard1.card + " of " + pickedCard1.suit);

let pickedCard2 = pickCard(15);
alert("card: " + pickedCard2.card + " of " + pickedCard2.suit);
```

#### 范式函数
让类型也成为参数
``` typescript
function identity<T>(arg: T): T {
    return arg;
}
let output = identity<string>("myString");  // type of output will be 'string'
function loggingIdentity<T>(arg: T[]): T[] { // 表示 以T为类型的数组
    console.log(arg.length);  // Array has a .length, so no more error
    return arg;
}
```
#### 范式类
``` typescript
class GenericNumber<T> {
    zeroValue: T;
    add: (x: T, y: T) => T;
}

let myGenericNumber = new GenericNumber<number>();
myGenericNumber.zeroValue = 0;
myGenericNumber.add = function(x, y) { return x + y; };
```

#### 泛型约束

通过接口约束 泛型类型需要有 length 属性
``` typescript
interface Lengthwise {
    length: number;
}

function loggingIdentity<T extends Lengthwise>(arg: T): T {
    console.log(arg.length);  // Now we know it has a .length property, so no more error
    return arg;
}
```
在泛型约束中使用类型参数
你可以声明一个类型参数，且它被另一个类型参数所约束。 比如，现在我们想要用属性名从对象里获取这个属性。 并且我们想要确保这个属性存在于对象obj上，因此我们需要在这两个类型之间使用约束。
``` typescript
function getProperty<T, K extends keyof T>(obj: T, key: K) {
    return obj[key];
}

let x = { a: 1, b: 2, c: 3, d: 4 };

getProperty(x, "a"); // okay
getProperty(x, "m"); // error: Argument of type 'm' isn't assignable to 'a' | 'b' | 'c' | 'd'.
```

在泛型里使用类类型
在TypeScript使用泛型创建工厂函数时，需要引用构造函数的类类型。比如，
``` typescript
function create<T>(c: {new(): T; }): T {
    return new c();
}
```
一个更高级的例子，使用原型属性推断并约束构造函数与类实例的关系。
``` typescript
class BeeKeeper {
    hasMask: boolean;
}

class ZooKeeper {
    nametag: string;
}

class Animal {
    numLegs: number;
}

class Bee extends Animal {
    keeper: BeeKeeper;
}

class Lion extends Animal {
    keeper: ZooKeeper;
}

function createInstance<A extends Animal>(c: new () => A): A {
    return new c();
}

createInstance(Lion).keeper.nametag;  // typechecks!
createInstance(Bee).keeper.hasMask;   // typechecks!
```

### 高级类型

#### 联合类型

string | number

null 和 undefined

如果一个函数包含可使用 null | undefined 的参数
,那么后面的函数,如果需要该参数并且使用 不包含 null | undefined 的部分 那么需要再该参数后面加 !
``` typescript
function broken(name: string | null): string {
  function postfix(epithet: string) {
    return name.charAt(0) + '.  the ' + epithet; // error, 'name' is possibly null
  }
  name = name || "Bob";
  return postfix("great");
}

function fixed(name: string | null): string {
  function postfix(epithet: string) {
    return name!.charAt(0) + '.  the ' + epithet; // ok
  }
  name = name || "Bob";
  return postfix("great");
}
```

类型别名

type Name =  string;
给 string 起一个 Name 的别名

字符串字面量类型
字符串字面量类型允许你指定字符串必须的固定值。 在实际应用中，字符串字面量类型可以与联合类型，类型保护和类型别名很好的配合。 通过结合使用这些特性，你可以实现类似枚举类型的字符串。
``` typescript
type Easing = "ease-in" | "ease-out" | "ease-in-out";
class UIElement {
    animate(dx: number, dy: number, easing: Easing) {
        if (easing === "ease-in") {
            // ...
        }
        else if (easing === "ease-out") {
        }
        else if (easing === "ease-in-out") {
        }
        else {
            // error! should not pass null or undefined.
        }
    }
}

let button = new UIElement();
button.animate(0, 0, "ease-in");
button.animate(0, 0, "uneasy"); // error: "uneasy" is not allowed here
```

#### 索引类型
``` typescript
function pluck<T, K extends keyof T>(o: T, names: K[]): T[K][] {
  return names.map(n => o[n]);
}

interface Person {
    name: string;
    age: number;
}
let person: Person = {
    name: 'Jarid',
    age: 35
};
let strings: string[] = pluck(person, ['name']); // ok, string[]
``

导入,导出
与ES6完全相同

三斜线导入
/// <reference types="someLib" />