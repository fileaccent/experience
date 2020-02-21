使用数组Reduce访问嵌套对象

Array reduce 方法非常强大，可用于安全地访问嵌套对象。

``` javascript
  const getNestedObject = (nestedObj, pathArr) => {
    return pathArr.reduce((obj, key) =>
      (obj && obj[key] !== 'undefined') ? obj[key] : null, nestedObj);
}

// 将对象结构作为数组元素传入
const name = getNestedObject(user, ['personalInfo', 'name']);

// 要访问嵌套数组，只需将数组索引作为数组元素传入。.
const city = getNestedObject(user, ['personalInfo', 'addresses', 0, 'city']);
// 这将从 addresses 中的第一层返回 city

```