#JS 继承机制 猜想和整理4 class继承

拷贝继承和原型继承那两章都是2010年的事情了。`class`从ES6开始正式被引入到JavaScript中。

```js
class Animal {
    constructor(name) {
        this.name = name;
    }
}

class Cat extends Animal{
    constructor(name){
        super(name);
    }
    say(){
        return "Hello, "+this.name+"!";
    }
}
```

简直。太舒服。

*因为不是所有的主流浏览器都支持ES6的class。如果一定要现在就用上，就需要一个工具把class代码转换为传统的prototype代码，可以试试Babel这个工具。*