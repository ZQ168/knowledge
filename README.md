# knowledge
努力的意义在于，维持美好生活~  

### call，apply的记录
call是this之后跟一个一个的参数，apply后面跟着一个数组参数
### findIndex和indexOf的区别
```findIndex()：```  
1.findIndex（）在测试添加为true的时候就返回索引位置，之后不会再执行  
2.没找到返回-1  
3.空数组不执行，不改变原数组  
### 数组的方法
```Array.prototype.copyWithin()```  
copyWithin()方法不会改变原数组的长度，但是会改变原数组  
浅复制数组的一部分到同一数组中的另一个位置，并返回它，不会改变原数组的长度。  
不改变原数组的方法：```plice,map,filter,reduce,includes,every,some,concat,join,indexOf ```   
    ```lastIndexOf()  ```
改变原数组的方法：```splice,foreach,push  ```
因为数组是可以迭代的，所以有一下方法  
```Object.keys(),Object.values(),Object.entries() ``` 
## Object中的方法
``1、Object.freeze()  ``
阻止修改现有属性的特性和值，并阻止添加新属性  
两种用法：```Object.freeze({}) 和 Object.free(object) ``` 
```2、Object.assign()  ```
只能拷贝自身的属性，不能拷贝prototype  
  ```Object.assign([1, 2, 3], [4, 5])  ```
3、```Object.create() ``` 
new和Object.create()  
new有构造函数，Object.create()丢失构造函数constructor  
new原构造函数prototype属性    
Object.createfoo会成为所创建对象的---数据属性  
```
foo: {  
  enumerable:false,//对象属性是否可通过for-in循环，flase为不可循环，默认值为true  
  writable: true, //对象属性是否可修改,flase为不可修改，默认值为true  
  configurable: true, //能否使用delete、能否需改属性特性、或能否修改访问器属性、，false为不可重新定义，  默认值为true
  value: "goodnice"  
},
```
4、```Object.defineProperties(obj,props)```  
直接在一个对象上定义新的属性或修改现有属性，并返回该对象。  
Object中的configurable：true，表示该属性可以改，可以删，默认为false  
5、hasOwnProperty()  
判断对象自身属性中是否具有指定的属性。  
```obj.hasOwnProperty('name') ``` 
9、```Object.is()  ``` 
判断两个值是否相同。   
如果下列任何一项成立，则两个值相同：   
两个值都是 undefined   
两个值都是 null  
两个值都是 true 或者都是 false      
两个值是由相同个数的字符按照相同的顺序组成的字符串  
两个值指向同一个对象  
两个值都是数字并且  
都是正零 +0  
都是负零 -0  
都是 NaN  
都是除零和 NaN 外的其它同一个数字  
### node中的process  
```process.platform darwin是mac ``` 
optimization：优化  
webpack中的dll：  
Dll打包以后是独立存在的，只要其包含的库没有增减、升级，hash也不会变化，因此线上的dll代码不需要随着版本发布频繁更  新。  
App部分代码修改后，只需要编译app部分的代码，dll部分，只要包含的库没有增减、升级，就不需要重新打包。这样也大大提高了每次编译的速度。  
假设你有多个项目，使用了相同的一些依赖库，它们就可以共用一个dll。  
### 判断一个对象里面的属性值value全都是空    
```
const judge = (obj) => {  
  let flag = true;  
  for (const key in obj) {  
    if (obj[key]) flag = false;  
  }  
  return flag;  
};
```
### form表单校验的时候一般validateTrigger：onChange(）一般不要用onBlur（）
### 使用antd中的form的校验如果有多层form校验，一定使用最顶层的form往下传递，不能最先命名一个属性名，而是应该给一个对象拼值
### 子组件没有校验是因为子组件是在另外一个form中，无法拼接到一个form表单中
### js array替换索引位置的值
```
// n表示第几项，从0开始算起。  
// prototype为对象原型，注意这里为对象增加自定义方法的方法。 
Array.prototype.del = function(n) {  
  // 如果n<0，则不进行任何操作。    
  if(n<0)   
    return this;    
  else   
    return this.slice(0,n).concat(this.slice(n+1,this.length));  
};
```
## 如何判断一个数组里有某个值  
```newConditionType.splice(index, 1, value);  ```

### 每天一个小技巧，人生更有希望
今天看到一个很简洁的深拷贝，看到有些方法自己没有用过，记录下来：
```Object.getPrototypeOf()```
Object.getPrototypeOf()方法返回指定对象的原型（内部[[Prototype]]）
```
Object.getPrototypeOf(object)
```
```
const prototype1 = {};
const object1 = Object.create(prototype1);

console.log(Object.getPrototypeOf(object1) === prototype1)  

写一个完美的深拷贝
```
一个巧妙的深拷贝
```
// 判断类型的方法移到外部，避免递归过程中多次执行
const judgeType = origin => {
  return Object.prototype.toString.call(origin).replaceAll(new RegExp(/\[|\]|object /g), "");
};
const reference = ["Set", "WeakSet", "Map", "WeakMap", "RegExp", "Date", "Error"];

function deepClone(obj) {
  // 定义新的对象，最后返回
  //通过 obj 的原型创建对象
  const cloneObj = Object.create(Object.getPrototypeOf(obj), Object.getOwnPropertyDescriptors(obj));
  let newObj = undefined;
  // 遍历对象，克隆属性
  for (let key of Reflect.ownKeys(obj)) {
    const val = obj[key];
    const type = judgeType(val);
    if (reference.includes(type)) {
        newObj[key] = new val.constructor(val);
    } else if (typeof val === "object" && val !== null) {
        // 递归克隆
        newObj[key] = deepClone(val);
    } else {
        // 基本数据类型和function
        newObj[key] = val;
    }
  }
  return newObj;
}
```


### 关于Object.create()
MDN的解释：
```
const person = {
  isHuman: false,
  printIntroduction: function() {
    console.log(`My name is ${this.name}. Am I human? ${this.isHuman}`);
  }
};

const me = Object.create(person);

me.name = 'Matthew'; // "name" is a property set on "me", but not on "person"
me.isHuman = true; // inherited properties can be overwritten

me.printIntroduction();
```

Object.create(proto, propertiesObject)方法有几个参数：
proto  
新创建对象的原型对象。   

propertiesObject 可选   
如果该参数被指定且不为 undefined，则该传入对象的自有可枚举属性（即其自身定义的属性，而不是其原型链上的枚举属性）将为新创建的对象添加指定的属性值和对应的属性描述符。这些属性对应于 Object.defineProperties() 的第二个参数
  
