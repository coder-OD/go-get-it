# 创建对象

## 1. 工厂模式

### ES5 实现工厂模式
```javascript
function reatePerson(name) {
  let person = new Object();
  person.name = name;

  person.sayName = function() {
    console.log(`name is ${name}`);
  }

  return person;
}
```

### ES6 实现工厂模式
```javascript
class User {
  constructor(name) {
    this.name = name;
  }
}

class UserFactory {
  static createUser(name) {
    return new User(name);
  }
}

const user = UserFactory.createUser('test');
```
---
 ## 2. 构造函数模式
 ```javascript
function Person(name) {
  this.name = name;
  this.sayName = function() {
    console.log(this.name);
  }
}
const person = new Person('test');
 ```
### 手动实现new
```javascript
const myNew = (constructor, ...args) => {
  let obj = {};
  obj.__proto__ = constructor.prototype;
  res = constructor.call(obj, ...args);

  return res instanceof Object ? res : obj;
}
```
---
## 3. 原型模式
> 我们创建的每个函数都有一个prototype属性，这个属性指向一个对象，函数的实例可以访问原型对象的属性和方法。

### 原型与实例属性检测
```javascript
// 由于 in 操作符只要通过对象能够访问到属性就返回 true，hasOwnProperty() 只在属性存在于实例中时才返回 true，因此只要 in 操作符返回 true 而 hasOwnProperty() 返回 false，就可以确定属性是原型中的属性。 
'name' in obj && !obj.hasOwnProperty('name')
```
---
## 4. 组合使用构造函数和原型模式
构造函数用于定义实例属性和方法，原型对象则用于定义共享属性和方法。
```javascript
// 构造函数
function Person(name, age, job){
  this.name = name;
  this.age = age;
  this.job = job;
  this.friends = ['Amy', 'Ben'];
}

// 原型模式
Person.prototype = {
  constructor: Person,
  sayName: function(){
    console.log(this.name);
  }
}
```