# JavaScript 代码规范

## 作用

- <del>让你难受...</del>
- 代码更整洁，可读性更高
- 减少因为语法错误浪费的时间
- 提高可维护性，查找更加快速
- 好的代码带来好心情 ❤️
- ...

## 自动修复

**新版的 CLI 可通过以下命令来使用自动修复功能**

~~~bash
tofu lint -f
~~~

## 关闭校验

可通过在新模板的 .tofurc 配置文件中设置关闭校验 😎

~~~javascript
// .tofurc.js
...
rules: {
    fuckAllRules: true
}
...
~~~

## 规则

!> 注释表示说明或错误的写法

### 变量

1. 使用单行单声明符来声明不赋值的变量
2. 使用多行多声明符来声明赋值的变量
3. 不允许使用 undefined

~~~javascript
let a, b, c;
// let a;
// let b;
// let a; let b;

let a = 1;
let b = 1;
let c = 1;
// let a = 1, b = 1, c = 1;
// let a = b = c = 1;

// const, var 同理

// let a = undefined;
~~~

### 最佳实践

1.块语句必须添加大括号

~~~javascript
if (foo) {
    foo++;
}

while (bar) {
    baz();
}

if (foo) {
    baz();
} else {
    qux();
}
~~~

2.switch 语句必须添加 default 声明

3.不允许存在空函数

4.不允许存在多个空格

5.不允许使用包装对象

~~~javascript
// var stringObject = new String("Hello world");
// var numberObject = new Number(33);
// var booleanObject = new Boolean(false);
~~~

6.变量不允许重复声明

### 风格

1.单行块语句前后必须加空格

~~~javascript
function foo() { return true; }
// function foo() {return true;}
~~~

2.采用以下括号风格

~~~javascript
function foo() {        // function foo()
  return true;          // {
}                       //  return true;
                        // }

if (foo) {              // if (foo)
  bar();                // {
}                       //   bar();
                        // }

if (foo) {              // if (foo) {
  bar();                //   bar();
} else {                // }
  baz();                // else {
}                       //   baz();
                        // }

try {                   // try
  somethingRisky();     // {
} catch(e) {            //   somethingRisky();
  handleError();        // } catch(e)
}                       // {
                        //   handleError();
                        // }
~~~

3.逗号的风格
- 逗号后空一格

~~~javascript
[1, 2, 3]
function foo (a, b, c) {}
~~~

4.计算属性前后不允许使用空格

~~~javascript
const a = 'a';
const obj = {
    [a]: 1
    // [ a ]: 1
}
~~~

5.文件最后空一行

6.函数调用左括号前不允许添加空格

~~~javascript
foo(); // foo ();
~~~

7.四格缩进，且不允许混用 tab

8.对象键名冒号后必须添加一个空格

~~~javascript
call({
    foobar: 42,
    bat: 2 * 2
});

// call({
//     foobar:42,
//     bat:         2 * 2
// });
~~~

9.单行小于 120 字符

10.空行不允许多于一行

11.对象属性调用不允许添加空格

~~~javascript
// foo. bar .baz . quz
~~~

12.对象括号换行规则 - 若换则换，不换则已

~~~javascript
let a = {};
let b = { foo: 1 };
let e = {
    foo: 1,
    bar: 2
};
~~~

13.函数中变量声明规则如上

14.字符串最外引号必须使用单引号

15.行尾必须添加分号

16.函数参数声明括号前不允许添加空格

17.一元操作符空格规则
- 关键字后必须添加一个空格
- 符号操作符与操作数之间不允许添加空格

~~~javascript
let a = {};
let b = { foo: 1 };
let e = {
    foo: 1,
    bar: 2
};
~~~

18.块语句前必须添加空格

~~~javascript
function a() {}

try {} catch(a) {}

class Foo {
  constructor() {}
}
~~~

19.操作符前后必须添加空格

### ES6

1.箭头前后添加空格

2.generator函数 * 号前不允许空格，后必须空一格

~~~javascript
function* foo() {}
~~~

3.不允许给 const 声明的变量再次赋值

4.不允许重复使用 import

~~~javascript
// import { a1 } from 'a';
// import { a2 } from 'a';
import { a1, a2 } from 'a';
~~~

### 可能发生错误的情况

1.不允许重复声明函数

2.数组不允许有空槽

3.不允许有多余的不可能执行的语句

### 其他规则

!> 这些规则仅用于校验语法的正确性，都是多余的或者可能发生错误的写法

1. no-compare-neg-zero
2. no-eval
3. no-invalid-regexp
4. no-dupe-args
5. no-dupe-keys
6. no-duplicate-case
7. no-empty
8. no-empty-character-class
9. no-extra-semi
10. no-regex-spaces
11. no-unexpected-multiline
12. valid-typeof
13. no-lone-blocks
14. no-loop-func
15. no-self-assign
16. no-self-compare
17. no-unused-expressions
18. no-useless-concat
19. no-with
20. no-use-before-define
21. no-unneeded-ternary
22. no-dupe-class-members
