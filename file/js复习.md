### js 复习

- 创建函数的几种方式

  - 声明函数
    最普通最标准的声明函数的方法，包括函数名以及函数体
    ```
    function fn1(){}
    ```
  - 创建匿名函数表达式
    创建一个变量，这个变量的内容为一个函数
    ```
      var fn1 = function(){
        //注意 采用这种方法创建的函数为匿名函数，即没有函数 name
        var fn1 = function(){};
        getFunctionName(fn1).length;//0
    ```
  - 创建具名函数表达式
    创建一个变量，内容为一个带有名称的函数
    ```
      var fn1= function xx(){}
      //注意：具名函数表达式的函数名只能在创建函数内部使用 外部使用即为undefined
      即采用此种方法创建的函数在函数外层只能使用fn1 不能使用xx的函数名
    ```
  - Function 构造函数
    可以给`function` 构造函数传一个函数字符串，返回包含这个字符串命令的函数，此种方法创建的是匿名函数
  - 自执行函数

  ```
  (function(){})();
  (function fn1(){})();
  ```

  - 闭包

    先来看一个栗子

    ```
      var age = 10;
      function foo(){
        console.log(age);
        var name = 'lizi';
        return function(){
          console.log(name)
        }
      }
      console.log(name);
      var bar = foo()
      bar()
    ```

    实际运行

    ```
      var age
      var bar
      function foo(){
        var name
        console.log(age); //10 函数内部可以访问到全局变量
        name ='lizi';
        return function(){
          console.log(name) //lizi
        }
      }
      age = 10
      console.log(name);//undefined
      bar = foo();
      bar()
    ```

    栗子 2

    ```
      var i = 0;
      function out(){
        function inner(){
          i++
          console.log(i)
        }
        return inner; //inner就是一个闭包函数，因为他能够访问out函数的作用域
      }
      var inner1 = out()
      inner1();//1
      inner1();//2
      inner1();//3
    ```

    ```
      function fn(){
        var arr=[];
        for(var i =0;i<5;i++){
          arr[i] =function(){

            return i  //5 5 5 5 5
          }
        }
        return arr; //[f,f,f,f,f]
      }
      var list =fn();
      for(var i = 0 ,len = list.length;i<len;i++){
        console.log(list[i]()) //5 5 5 5 5
      }
    ```

    - 总结：闭包的概念 有权访问另一个函数作用域的变量的函数
