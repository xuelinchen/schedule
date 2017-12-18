javascript
===========

参考
------

https://developer.mozilla.org/en-US/docs/Web/JavaScript/


语法
--------

箭头函数
^^^^^^^^^^

   | (param1, param2, …, paramN) => { statements }
   | (param1, param2, …, paramN) => expression
   | // equivalent to: (param1, param2, …, paramN) => { return expression; }
   | // Parentheses are optional when there's only one parameter name:
   | (singleParam) => { statements }
   | singleParam => { statements }
   | singleParam => expression
   | // The parameter list for a function with no parameters should be written with a pair of parentheses.
   | () => { statements }
   | // Parenthesize the body of function to return an object literal expression:
   | params => ({foo: bar})   
   | // Rest parameters and default parameters are supported
   | (param1, param2, ...rest) => { statements }
   | (param1 = defaultValue1, param2, …, paramN = defaultValueN) => { statements }    
   | // Destructuring within the parameter list is also supported
   | let f = ([a, b] = [1, 2], {x: c} = {x: a + b}) => a + b + c;
   | f();  
   | // 6

示例 ::
   
    var materials = [
        'Hydrogen',
        'Helium',
        'Lithium',
        'Beryllium'
    ];
    
    materials.map(function(material) { 
        return material.length; 
    }); // [8, 6, 7, 9]
    
    materials.map((material) => {
        return material.length;
    }); // [8, 6, 7, 9]
    
    materials.map(material => material.length); // [8, 6, 7, 9]
        
示例2 ::
    
    function Person() {
        // The Person() constructor defines `this` as an instance of itself.
        this.age = 0;
    
        setInterval(function growUp() {
          // In non-strict mode, the growUp() function defines `this` 
          // as the global object, which is different from the `this`
          // defined by the Person() constructor.
          this.age++;
        }, 1000);
    }
    var p = new Person();

    In ECMAScript 3/5, the this issue was fixable by assigning the value in this to a variable that could be closed over.
    
    function Person() {
        var that = this;
        that.age = 0;
        
        setInterval(function growUp() {
          // The callback refers to the `that` variable of which
          // the value is the expected object.
          that.age++;
        }, 1000);
    } 
    
    function Person(){
        this.age = 0;
        
        setInterval(() => {
        this.age++; // |this| properly refers to the person object
        }, 1000);
    } 
    var p = new Person();