title: ES6中的代理对象
author: shh33
categories:
  - ES6
typora-root-url: ..
tags:
  - 数据保护
  - 代理对象
date: 2019-08-28 16:59:00
password:
top:
---

```javascript
{
  var Person = function() {
​      var data = {
​      name: 'es3',
​      sex: 'male',
​      age: 15
​    }
​    this.get = function(key) {
​      return data[key]
​    }
​    this.set = function(key, value) {
​      if (key !== 'sex') {
​        data[key] = value
​      }
​    }
  }
```

//声明一个实例

```javascript
  var person = new Person();
```

  // 读取

```javascript
console.table({name: person.get('name'), sex: person.get('sex'), age:person.get('age')});
```

![1566981354107](/images/1566981354107.png)

  // 修改

```javascript
person.set('name', 'es3-cname');

console.table({name: person.get('name'), sex: person.get('sex'), age:person.get('age')});
```

![1566981519105](/images/1566981519105.png)

```javascript
 person.set('sex', 'female');

 console.table({name: person.get('name'), sex: person.get('sex'), age: person.get('age')});
```

![1566981533339](/images/1566981533339.png)

```
}
```

# ES5

```javascript
{
  var Person = {
​    name: 'es5', 
​    age: 15
  };
  
  Object.defineProperty(Person, 'sex', {
​    writable: false,
​    value: 'male'
  });
  
  console.table({
​    name: Person.name,
​    age: Person.age,
​    sex: Person.sex
  });
  
  Person.name = 'es5-cname';
  
  console.table({
​    name: Person.name,
​    age: Person.age,
​    sex: Person.sex
  });

  try {
​    Person.sex = 'female';
​    console.table({
​      name: Person.name,
​      age: Person.age,
​      sex: Person.sex});
  } catch (e) {
​    console.log(e);
  }

} 
```

![1566981878277](/images/1566981878277.png)

*// ES6*

```javascript
{

  let Person = {
​    name: 'es6',
​    sex: 'male',
​    age: 15
  };
  
  let person = new Proxy(Person, {
  
​    get(target, key) {
​      return target[key]
​    },

​    set(target,key,value){
​      if(key!=='sex'){
​        target[key]=value;
​      }
​    }
  });


  console.table({
​    name:person.name,
​    sex:person.sex,
​    age:person.age
  });

  try {

​    person.sex='female';
  } catch (e) {
​    console.log(e);
  } finally {
  }
}
```

![1566982135689](/images/1566982135689.png)

> 1. Proxy是代理
