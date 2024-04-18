# typescirpt基礎

# First, About Javascript

- JavaScriptって聞いたことある？
- JavaScriptはWebブラウザで動作する言語である．
- JavaScriptはWebブラウザで完結する言語なので、元々、システムコールの仕組みなどを持たない．
- プロトタイプベースのオブジェクト指向言語だと言われている．
- ECMAScriptという仕様に基づいて実装されている．
- Google Mapにおいて革新的な利用をされたことによって、一気に再注目され、デファクトスタンダードになった．

- Have you ever heard of JavaScript?
- JavaScript is a language that runs in a Web browser.
- Since JavaScript is a language that runs entirely in the Web browser, it does not have a system call mechanism.
- It is said to be a prototype-based object-oriented language.
- It is implemented based on the ECMAScript specification.
- The innovative use of JavaScript in Google Maps has brought it back into the limelight and made it the de facto standard.

# About TypeScript

- TypeScriptはJavaScritpのスーパーセットである．
    - スーパーセットとは？
        - **特定の対象物に対して既存のものをすべて含んだ上でより機能が拡張されている上位互換となるモノ**
- TypeScriptはJavaScriptにある機能を全て含んだ上で、「型」の機能をより充実させたものである．

- TypeScript is a superset of JavaScritp.
    - What is a superset?
        - **A superset that includes all the existing features of a particular object, but with enhanced functionality**.
- TypeScript is a superset of JavaScritp that includes all the existing features of JavaScript, but with enhanced "type" functionality.

# About Node JS

- Node.jsはJavaScriptの実行環境
- 元々ブラウザ上でしか動いていなかった、JavaScirptをローカルPC上で動くようにしてくれた．
- その結果、JavaScritpはフロントエンドのみの言語から、バックエンドで使用可能な言語になった．
- **イベントループ**という特殊な並行処理の特徴を持つ．
    - イベントループが何かをよく説明してくれている動画
    - [https://www.youtube.com/watch?v=8aGhZQkoFbQ&t=1s](https://www.youtube.com/watch?v=8aGhZQkoFbQ&t=1s)
- 関数型プログラミングについて
    - [https://www.youtube.com/watch?v=e-5obm1G_FY](https://www.youtube.com/watch?v=e-5obm1G_FY)

- Node.js is a JavaScript execution environment
- JavaScirpt, which originally ran only in the browser, can now run on a local PC.
- As a result, JavaScritp has gone from a front-end-only language to one that can be used on the back end.
- **It has a special concurrency feature called an event loop**.
    - Video that explains well what an event loop is.
    - [https://www.youtube.com/watch?v=8aGhZQkoFbQ&t=1s](https://www.youtube.com/watch?v=8aGhZQkoFbQ&t=1s)
- About Functional Programming
    - [https://www.youtube.com/watch?v=e-5obm1G_FY](https://www.youtube.com/watch?v=e-5obm1G_FY)

# **Let's leave the hard stuff out…**

## Challenge first Step of Node.js

### Install node.js LTS 18.16.0

[](https://nodejs.org/en)

What is Node.js?(For Japanese speakers)

[Node.jsとはなにか？なぜみんな使っているのか？ - Qiita](https://qiita.com/non_cal/items/a8fee0b7ad96e67713eb)

- バージョン管理をしたい人用
    
    pythonのpyenv的なもので `n` というバージョン管理ツールがあります．
    
    ```bash
    sudo npm install -g n
    # stable　versionの確認
    n --stable
    # latest versionの確認
    n --latest
    # latest versionのインストール
    sudo n latest
    # nodeのバージョン確認
    node -v
    ```
    

Open your Terminal

```bash
$ node
Welcome to Node.js v18.16.0.
Type ".help" for more information.
> console.log('Hello World')
```

`console.log`はC言語の`printf`だし、pythonの`print`

### About variables

<aside>
💡 Please use “const” and “let”!!!

</aside>

```tsx
const //初期値を定義でき、再代入ができない　Initial values can be defined and cannot be reassigned
let   //再代入可能　reassignable

const foo = 'foo'
let  bar = 'bar'

//error
foo = 'foo2'
//OK
bar = 'bar2'
```

- constの注意（発展的な話）
    
    ```tsx
    const object = {
        key: "値"
    };
    
    //OK
    object.key = "新しい値";
    
    //error
    object = {key: "atai"}
    ```
    

### About Type

Why type is necessary?

どうして型が必要なのか？

<aside>
💡 型安全(Type Safe)
型を使って、プログラムが不正なことをしないように防ぐこと
Using types to prevent programs from doing bad things

</aside>

what is the bad things?

- 数値とリストを掛け合わせる Multiply “numbers” and “lists”
- 存在しないメソッドの呼び出し  Call to non-existent method

In JavaScirpt, these code is OK!!!!????

```tsx
a = 3 + []  
console.log(a)

a = 3  + [1]
console.log(a) 

a = 3  + [21]
console.log(a) 

function test(b) {
	return b / 2
}
conslole.log(test('z'))
```

- result of above
    
    ```tsx
    a = 3 + []  
    console.log(a) //3
    
    a = 3  + [1]
    console.log(a) //31
    
    a = 3  + [21]
    console.log(a) //321
    
    function test(b) {
    	return b / 2
    }
    conslole.log(test('z')) //NaN
    ```
    
- About Data type
    
    より低レイヤの話をすると、JavaScriptも型を持ってはいるが、実は実行時に型を推論するプログラムが裏で動いている．
    データ型が存在しないと、メモリ上でその変数や定数の情報を何バイト分、あるメモリアドレスを先頭として見ればいいわからない．そういう意味で、あらゆる言語では、実行においては、データ型の推測が必須．
    
    On a lower level, JavaScript also has types, but there is actually a program running behind the scenes to infer the type at runtime.
    Without a data type, there is no way to know how many bytes of information about a variable or constant to look at in memory, starting at a certain memory address. In this sense, all languages must infer the data type at runtime.
    

# ここが複雑(**Here's the complication.**)

- Node.jsはJavaScriptの実行環境（TypeScriptの実行環境ではない）
- Node.js is a JavaScript execution environment (not a TypeScript execution environment)

- TypeScriptで書いたコードをNode.jsで実行するには、TypeScriptをJavaScriptにトランスパイルしないといけない．
- To run code written in TypeScript in Node.js, TypeScript must be transpiled to JavaScript

- そのために、TSCを使います．
- For this purpose, TSC is used.

```bash
sudo npm i typescript -g
```

毎回以下の操作を忘れないようにしてください．

1. `tsc ~.ts`
2. `node ~.js`

## Type of TypeScript(TypeScriptの型)

型を明示するには、アノテーションをつける

<aside>
💡 backendの研修中は100％つけるように心がけましょう
Try to keep it on 100% of the time during BACKEND training!

</aside>

```tsx
let <変数名> : <型アノテーション> = //の形で宣言する
let a: number = 1 // aはnumber型
let b: string = 'hello' //bはstring型
let c: boolean[] = [true, false] //cはbooleanの配列
```

- TypeScriptは漸進的型付け言語 (**TypeScript is a progressively typed language?**)
    
    実はTypeScriptはコンパイルするために必ずしも全ての型がわかっている必要なない．型付けされていないプログラムであっても、TypeScriptはいくつかの型を推論して、ミスを見つけてくれる．ただ、プログラム内の全てのものの型がわかっている時にTypeScriptはもっとも効果を発揮してくれる．
    
    In fact, TypeScript does not require all types to be known in order to compile. Even if the program is not typed, TypeScript can infer some types and find mistakes. However, TypeScript is most effective when it knows the types of everything in the program.
    

### problem1

以下の出力を得られるようにコードを書いてみてください．

Try writing code to get the following output. 

please use `Object.prototype.toString.call(x)` function to get the type

```bash
$ tsc ex00/ex00.ts
$ node ex00/ex00.js
[object Number]
[object Boolean]
[object String]
[object Undefined]
[object Array]
[object Null]
[object Object]
```

## About function

```jsx
//よくある関数宣言のパターン
function add1(a :number, b :number) :number {
	return a + b
}

//関数式を変数に割り当てるパターン
const add2 = function(a :number, b :number) :number{
	return a + b
}

//名前付き関数を変数に割り当てるパターン
const add3 = function addFn(a :number, b :number) :number{
	return a + b
}

//アロー関数のパターン１
const add4 = (a :number, b :number) :number => {
	return a + b
}

//アロー関数のパターン２　{}を省略するとreturnなしで値が返される
const add5 = (a:number , b:number):number => a + b

//アロー関数のパターン３　パラメータ（引数）が一つならパラメータを囲む()も省略できる
//JavaScriptでの実装でのみ可能
const add6 = a => a + 1
```

# TypeScriptになれる

以下のドキュメントを読みつつ、課題をこなしましょう．

Read the following documents and complete the assignments.

[現代の JavaScript チュートリアル](https://ja.javascript.info/)

[第一部: 基本文法 · JavaScript Primer #jsprimer](https://jsprimer.net/basic/)

[TypeScriptのあらまし | TypeScript入門『サバイバルTypeScript』](https://typescriptbook.jp/overview)

[JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

[Tutorials | MDN](https://developer.mozilla.org/en-US/docs/Web/Tutorials#javascript_tutorials)

[TypeScript Deep Dive 日本語版](https://typescript-jp.gitbook.io/deep-dive/)

[JavaScript 学習レッスン I | Progate](https://prog-8.com/lessons/es6/study/1)

## roop and if else

### problem 1

Create a function that displays `Negative` or `Positive` depending on the integer’s sign entered as a parameter. If n is negative, displays `Negative` If n is positive or zero, displays `Positive`

this is the prototype of function

```tsx
function isNegative(i: number):void{
    //write some programs
};
```

### problem2

Create a function which reverses a given array of integer (first goes last)

this is the prototype of function

```tsx
function revNumberArray(numbers: number[]):number[]{
    //write some programs
}
```

- callback関数について
    
    関数の引数として、関数を実行することができる．
    
    ```tsx
    const array1 = [0,1,2,3]
    const array2 = array1.map((element) =>  {
        console.log('${element}を変換')
        return element * 10
    })
    console.log('変換完了：',array2)
    ```
    

### problem3

Create a function which sorts an array of integers by ascending order.

this is the prototype of function

```tsx
function sortNumber_array(numbers: number[]):number[]{
    //write some programs
}
```

### problem4

Create a function that displays all different combinations of three different digits in ascending order, listed by ascending order.

Here’s the expected output

```bash
$ tsc ~.ts
$ node ~.js
012, 013, 014, 015, 016, 018, 019, 023, ...., 789
```

- 978 isn’t there because 789 already is.
- 999 isn’t there because 9 is present more than once.

this is the prototype of function

```tsx
function printComb():void{
	//write some programs
}
```

## Difficultがついてる問題はskipしてOKです！チャレンジ問題です！

### problem5(a little difficult)

Create a function that displays all different combination of two digits between 00 and 99, listed by ascending order.

Here’s the expected output

```bash
$ tsc ~.ts
$ node ~.js
00 01, 00 02, 00 03, 00 04, 00 05, ...., 00 99, 01 02, 01 03, ...., 97 99, 98 99
```

this is the prototype of function

```tsx
function printComb2():void{
	//write some programs
}
```

### problem6 (difficult)

Create a function that displays all different combinations of n numbers by ascending order.

n will be so that: 0 < n < 10

if n = 2, heer’s the expected output

```bash
$ tsc ~.ts
$ node ~.js
01, 02, 03, ... 09, 12, ..., 79, 89
```

this is the prototype of function

```tsx
function printCombn(n:int):void{
	//write some programs
}
```

### problem7(difficult)

Create a function that displays a number in a base system in the terminal

this number is given in the shape of an number, and the radix in the shape of a string of characters.

the base-system contains all useable symbols to display that number:

- `0123456789` is the commonly used base system to represent decimal numbers
- `01` is a binary base system
- `0123456789ABCDEF` an hexadecimal base system
- `poneyvif` is an octal base system

the function must handle negative numbers

if there’s an invalid argument, nothing should be displayed. Examples of invalid arguments

- base is empty or size of 1
- base contains the same character twice
- base contains `+` or `-`

this is the prototype of function

```tsx
function putnbrBase(n : number, base : string):void {

}
```

## object, map and array

<aside>
💡 In those problems, if there is no Type annotation, think and made.

</aside>

### problem 1

set the type declaration to the object

```jsx
let obj = {foo: 'bar', baz: 42 };
```

- answer
    
    ```tsx
    let obj:{foo: string, baz: number} = {foo: 'bar', baz: 42 };
    ```
    

### problem2

merge `const a = { a: 'a' }`and `const b = { b: 'b' }` , and make 
`c= {a: 'a', b:'b'}`

```tsx
const a = { a: 'a' };
const b = { b:'b'};
const c = <write some code>
```

- answer
    
    ```tsx
    const a: {a: string} = { a: 'a' };
    const b: {b: string} = { b:'b'};
    const c: {a: string, b: string} = Object.assign({}, a, b);
    ```
    

### problem3

there is an array

```tsx
const arry = ['aa','bb','cc','dd','ee','ff','gg'];
```

From this array, make new array have`[dd, ee, ff]`

```tsx
const arry = ['aa','bb','cc','dd','ee','ff','gg'];
const newArry = <write some code>
```

- answer
    
    ```tsx
    const arry: string[] = ['aa','bb','cc','dd','ee','ff','gg'];
    const newArray: string[] = arry.slice(-4,-1);
    
    const newArray: string[] = arry.slice(3,-1);
    ```
    

### problem4

任意の変数がarrayであるかどうかを判断するために使える関数を探してください．

Find a function that can be used to determine if an arbitrary variable is an array.

- answer
    
    ```tsx
    Array.isArray(arry)
    ```
    

### problem5

以下のコードに関して、それぞれ実行されるかどうかをみて、理由を考えてください．(xは宣言されていません)JavaSriptで試してみてください．

```tsx
//1
if (typeof x === 'undefined') {
  console.log('1')
}

//2
if(x === undefined){
 console.log('2')
}
```

６

- answer
    
    ```tsx
    //1は実行される
    //2は実行されない(ReferenceError)
    
    //typeofは変数が存在しない場合エラーは投げない。
    //ただこのような値の存在チェックは避けるべき
    //グローバル上の値のチェックはfor in
    ```
    

### problem6

以下のコードはそれぞれ実行されますか？理由も考えなさい

1の方はxが宣言されていますが、2の方はyが宣言されていません

JavaSriptで試してみてください．

```tsx
//1
let x;
if (x === void 0) {
}

//2
// 直前まで y は宣言されていない
if (y === void 0) {
}
```

- answer
    
    ```tsx
    //1は宣言はされているが値が割り当てられていない場合です。
    //実行される
    
    //2は宣言されていない場合です。
    //実行されない
    
    //void 0 は確実にundefindeを返すことが保証されています
    //undefinedはただのglobal変数なので
    undefined = "foo";
    undefined;
    //'foo'
    で代入でき、保証はされていない
    
    e.g:
    undefined = 1;
    console.log(!!undefined); //true
    console.log(!!void(0)); //false
    ```
    

### problem7

change the `let obj = {foo: 'bar', baz: 42 };` to Map Object.

use `tsc obj/problem2/test.ts --lib ES2023,dom`

- answer
    
    ```tsx
    var obj：{foo: string, baz: number} = { foo: 'bar', baz: 42 }; 
    var map = new Map(Object.entries(obj));
    console.log(map); // Map { foo: 'bar', baz: 42 }
    ```
    

### problem8

Make

```tsx
const arr = [
    { key: 'foo', val: 'bar' },
    { key: 'hello', val: 'world' }
];
```

map object.

output is like this

```tsx
{'foo' => 'bar', 'hello' => 'world'}
```

- answer
    
    ```tsx
    const arr: {key:string, val:string}[] = [
        { key: 'foo', val: 'bar' },
        { key: 'hello', val: 'world' }
    ];
    const result:Map<string, string> = new Map(arr.map((i) => [i.key, i.val]));
    console.log(result);
    ```
    

### problem9

Make this object  a multidimensional array.

```tsx
const myObject = = {1: ['e', 'ee', 'eee'], 2: ['f', 'ff','fff']};
```

output is like this.

```tsx
[[‘e’,’ee’,’eee’],[‘f’,’ff’, ‘fff’]]
```

- answer
    
    `tsc <file path> -lib ES2017, dom` じゃないとダメかも
    
    ```tsx
    const myObject  = {1: ['e', 'ee', 'eee'], 2: ['f', 'ff','fff']};
    const newArr = Object.keys(myObject).map(function(elem){
       return myObject[elem]
    })
    //[[‘e’,’ee’,’eee’],[‘f’,’ff’, ‘fff’]]
    
    //other
    const myObject  = {1: ['ee', 'eee', 'efe'], 2: ['faf', 'fafa','fa']};
    const arr = Object.values(myObject);
    ```
    

### problem10

like this, use the index as a key and the array elements as their respective values.

```tsx
['a','b','c’] →　{0: 'a’, 1: 'b', 2: 'c'}
```

- answer
    
    ```
    //1
    const arry = ['a', 'b', 'c'];
    function toObject(arry){
     const obj = {};
     const len =  arry.length;
     for(let i=0; i < len; i++){
      obj[i] = arry[i]
     }
     return obj
    }
    toObject(arry)
    //{0: 'a', 1: 'b', 2: 'c'}
    
    //2
    const arry = ['a', 'b', 'c'];
    const obj = arry.reduce(function(o, v, i){
     o[i] = v;
     return o;
    },{})
    obj
    //{0: 'a', 1: 'b', 2: 'c'}
    
    //3
    [{a: 1},{b: 3}].reduce(function(result, item){
     var key = Object.keys(item)[0]
     result[key] = item[key];
     return result;
    },{})
    //{a: 1, b: 3}
    ```
    

### problem11

Make  `[ [1, 2], [], [3]]` flat.

output is like this.

```tsx
[1, 2, 3]
```

- answer
    
    ```tsx
    const myArray = [[1,2],[],[3]];
    const flatArray = Array.prototype.concat.apply([],myArray);
    ```
    

### problem12

add `eee` in front of the `let ary = ['aaa', 'bbb', 'ccc'];`

It`s mean make this.

```tsx
['eee', 'aaa', 'bbb', 'ccc']
```

- answer
    
    ```tsx
    var ary = ['aaa', 'bbb', 'ccc'];
    ary.unshift('eee');
    ```
    

### problem13

This code output `[3, 3, 3]`

please fix and output `[1, 2, 3]`

```tsx
const arr = [];
for (let i=0; i < 3; i++) {
    arr.push(() => i);
}
arr.map(x => x());
```

- answer
    
    ```
    const arr = [];
    for (let i=0; i < 3; i++) {
        arr.push(() => i);
    }
    arr.map(x => x()); // [0,1,2]
    ```
    

### problem14

Compare string variable a with string variable b and return true if the number appears before variable a

input example

```tsx
let a = 'aabbccdde1e23ffgg';
let b = 'aabbccddee123ffgg';

function string_comp(a:string, b:string):boolean{
	//write some code
}
```

- answer
    
    ```tsx
    var a = 'aabbccdde1e23ffgg';
    var b = 'aabbccddee123ffgg';
    
    function string_comp(a:string, b:string):boolean{
    	return a.search(/\d/) < b.search(/\d/);
    }
    
    ```
    

### problem15

Execute this code.

```tsx
const characters = ['b', 'd', 'a', 'c'];
const sortedCharacters = characters.sort()
sortedCharacters
//['a', 'b', 'c', 'd']
sortedCharacters === characters //This line is true
```

change the second line of above and sort and then return a new array.

If done correctly, the last line will be false.

```jsx
const characters = ['b', 'd', 'a', 'c'];
const sortedCharacters = <think this line>
sortedCharacters
//['a', 'b', 'c', 'd']
sortedCharacters === characters //This line is false
```

- answer
    
    配列をsortした返り値は同じオブジェクトを参照します。 sortをした上で新しい配列を返すようにしてください。
    
    ```tsx
    const characters = ['b', 'd', 'a', 'c'];
    const sortedCharacters = characters.slice().sort();
    sortedCharacters === characters
    //false
    ```
    

### problem16

There is a Object like

```tsx
let obj = {
 'prop1': 'value1',
 'prop2': 'value2',
 'prop3': 'value3'
}
```

Use `Json.stringfy` and make the function to output

```tsx
"{
	"prop1": "value1",
	"prop2": "value2"
}"
```

Note, there is no `prop3`

- answer
    
    ```tsx
    var obj = {
     'prop1': 'value1',
     'prop2': 'value2',
     'prop3': 'value3'
    }
    var str = JSON.stringify(obj, ['prop1', 'prop2'], '\t');
    str
    //
    "{
    	"prop1": "value1",
    	"prop2": "value2"
    }"
    
    //ex
    関数で出力を
    function selectedProperties(key, val) {
        // the first val will be the entire object, key is empty string
        if (!key) {
            return val;
        }
        if (key === 'prop1' || key === 'prop2') {
            return val;
        }
        return;
    }
    var str = JSON.stringify(obj, selectedProperties, '\t');
    str
    //
    {
        "prop1": "value1",
        "prop2": "value2"
    }
    ```
    

### problem17

```tsx
const foo = 'outer';
function bar(func = x => foo) {
    const foo = 'inner';
    console.log(func());
}
bar();
```

What is the output of this code, and think why the output happen.

- answer
    
    outerが出力される．関数のスコープについて考えると良い．
    

## recursive and roop

### problem 1

Create a function that returns the n-th element of the Fibonacci swquence.

The first element being at the 0 index.

We’ll consider that the Fibonacci sequence starts like this `0, 1, 1, 2…`

overflows must not be handled.

this is the prototype of function

```tsx
function fibonacci(n: number):number{
}
```

<aside>
💡 If you can afford it, find out how many digits it can handle.

</aside>

### problem2

Create a function that returns square root of a number(if it exists), or 0 if the square root is an irrational number

this is the prototype of function

```tsx
function sqrt(n: number):number{
}
```

### problem3

Create a function that returns 1 if the number given as a parameter is a prime number, and 0 is it isn’t

this is the prototype of function

```tsx
function prime(n: number):number{
}
```

### problem4(difficult)

Ten Queens

Create a function that displays all possible placements of the ten queens on a chessboard which would contain ten columns and ten lines, without them being able to reach each other in a single move, and returns the number of possibilities.

Recursivity is required to solve this problem.

 this is the prototype of function

```tsx
function tenQueens():void{
}
```

Here’s how it’ll be displayed

```tsx
$ tsc ~.ts
$ node ~.js
0257948136
0258683147
...
4605713829
4609582731
...
9742061863
```
## 全部終わって暇になった人むけの課題
[Elevator Saga - the elevator programming game](https://play.elevatorsaga.com/)

## Call back function

### example

If you call some functions as a function arguments, it’s a `callback function`

- 関数は値であり、オブジェクト型の一つ
- 関数は値を受け取ることができる
- 関数は関数に値を渡すことができる．
- 関数に渡される関数はコールバック関数
- コールバック関数を使う関数は高階関数

- A function is a value, an object type
- A function can receive a value
- A function can pass a value to a function.
- A function passed to a function is a callback function
- A function that uses a callback function is a higher-order function

- 関数を別々に定義している例 Example of defining functions separately

```jsx
function funcA(text: ()=>void) {
  text(); // funcB
  console.log('メッセージを受け取りました'); // funcA
}

// コールバック関数 → funcAの呼び出し時に引数に指定される
function funcB():void {
  console.log('こんにちは');
}

// funcAの呼び出し → 引数にfuncBを指定
funcA(funcB);
```

- 引数に直接関数を記述する Write functions directly in arguments

```jsx
function funcA(text:()=> void) {
  text();
  console.log('メッセージを受け取りました');
}

// funcAの呼び出し → 引数に関数式を定義
funcA(function():void { 
  console.log('こんにちは');
});

// "こんにちは"
// "メッセージを受け取りました"
```

アロー関数を使う場合 when using the Arrow function

```jsx
function funcA(text:()=>{}) {
  text();
  console.log('メッセージを受け取りました');
}

// funcAの呼び出し → 引数に関数式を定義
funcA(() => { 
  console.log('こんにちは');
});

// "こんにちは"
// "メッセージを受け取りました"
```

setTimeoutを使う例

```jsx
setTimeout(<fuction>, <time>);

function sayHi() {
  console.log('こんにちは');
}

setTimeout(sayHi, 3000); // 3秒後に出力

// use functional expression(関数式を使う例)
setTimeout(()　=> {
  console.log('こんにちは');
}, 3000);
```

```jsx
const array1 = [0,1,2,3]
const array2 = array1.map((element) =>  {
    console.log('${element}を変換')
    return element * 10
})
console.log('変換完了：',array2)
```

### problem

```jsx
function Person() {
    let self = this;
    self.age = 0;

    setInterval(function() {
        // The callback refers to the `self` variable of which
        // the value is the expected object.
        self.age++;
    }, 1000);
}
var p = new Person();
p
//{age: 1} //1秒ごとに1足される
```

rewrite callback function in `setInterval`  as a arrow function.

Also, if you need, set Type Annotation


## その他話しておきたいこと

### 厳密比較のこと

```tsx
const str = new String('うさぎ');
 
console.log( 'うさぎ' == str ); 
 
console.log( 'うさぎ' === str )；
```

`==` : 左辺と右辺が等しい場合にはtrueを返す

`===` :[https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Strict_equality](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Strict_equality)
