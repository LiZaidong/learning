[Typescript 入门教程](https://ts.xcatliu.com/basics/type-of-array.html)

[深入理解 Typescript](https://jkchao.github.io/typescript-book-chinese/typings/overview.html#%E6%B3%9B%E5%9E%8B)

https://github.com/PleaseStartYourPerformance/TypeScript

TypeScript

- 原始数据类型

  - 布尔值，数值，字符串，null，undefined，symbol
  - `let decimal: number = 6;`
    - 声明之后立即赋值，decimal为数值类型的变量
  - 不能访问不属于已定义类型的属性和方法
  - 数组内已有多个数据类型，新加入的值可以不定义类型，会使用联合类型替代

- 空值 `void`

  - 可用来表示函数没有返回值

  ```
  function alertName(): void {
      alert('My name is Tom')
  }
  ```

- null 和undefined

  - 声明一个空值的变量没有用，因为它只能表示undefined 和 null
  - null 类型只能被赋值为null
  - undefined 类型只能被赋值为undefined
  - null和undefined，跟void的区别
    - null和undefined是所有类型的子类型，可以赋值给其他类型的变量
    - 而void不行

- 任意类型 `any`

  - 普通类型在赋值过程中是不允许改变类型的

  - 如果是`any` 类型，允许被赋值为任意

  - 任意值上访问任何属性和方法都是允许的

  - 变量定义的时候设定类型，就默认为any

    ```
    let a
    等价于
    let a: any
    ```

- 类型推论

  - 在没有明确指定类型的情况下，会推测吃一个类型
  - 如果在定义的时候没有赋值，不管之后有没有赋值，都会被定义为`any`类型而不被类型检查

- 联合类型

  - 表示取值可以是多个类型中的其中之一，用`|`分隔
  - 当不确定一个联合类型的变量是什么类型时，只能访问此联合类型的所有类型里共有的属性和方法

- 交叉类型

  - 使用`extends` 通过继承一个对象的另一个对象生成一个新的对象的，拥有两个对象的全部功能，可以用在泛型的传参里

- 接口 interface

  - 任意属性，一般用  propName  表示
    - 在定义属性的时候，可以使用`[propName: string]: any`，来定义任意属性
    - 任意属性的key的类型必须是number或者string
    - 一旦定义了任意类型，并且任意属性的key的类型是string，那么其余确定属性和可选属性必须是它的子级
    - 如果存在可选属性，任意属性的类型必须包含undefined
    - 一个接口中只能定义一个任意属性，如果存在多个属性，必须使用联合类型

  - 对于readonly制度属性的限制只在第一次给对象赋值的时候，而不是第一次给属性赋值的时候

  - 也可以使用内联注解语法注解任何内容，类似匿名函数，虽然省去了命名的麻烦，但是不利于复用

    - ```
      interface Person: {
          name: string;
          age: number;
      }
      let p: Person;
      // 内联
      let p2: {
          name: string;
          age: number;
      }
      ```

    - 

- 数组类型

  - 可以用属性类型为数字的接口来定义类数组

- 类型断言

  - 当类之间有继承关系时，可以使用类型断言将比较抽象的父类断言为更为具体的子类
  - 类型断言不是类型转换，断言结果会在转换结果中删除

- 声明文件

  - 只有`function`、`class`、`interface`可以直接默认到处，其他的变量需要事先定义再导出
  - 只要.ts或者.d.ts文件中有import或export，那么文件中的delare就会变成局部变量

- 类型别名type：就是给类型重新起一个名字，常用于联合类型

- 字符串字面量类型

  - ```
    type letter = 'a' | 'b' | 'c'` 表示letter的值只能是这三者之一
    enum letter {
        a = 'a',
        b = 'b',
        c = 'c'
    }
    type letter2 = keyof typeof letter
    ```

- 元祖

  - 当赋值或者访问一个已知索引的元组，会得到正确的值
  - 在对元组中的元素进行操作前，需要先给元组自身赋值
  - 对元组本身进行操作，需要提供所有指定的类型
  - 访问一个不存在的元素，必须是元祖中已经存在中的值的类型中的一种

- 枚举

  - 成员被赋值默认从数字0开始，递增往后，递增的步长为1，即使前面的值被手动赋值为小数或者负数，
  - 未手动赋值的项会接着上一个枚举的值递增
  - `const enum` 常数枚举，
    - 与普通枚举的区别
      - 在编译阶段会被删除
      - 不能包含计算成员

- 类

  - public 修饰公共的属性和方法，可以在任意位置访问，默认的属性和方法都是public
  - private 修饰私有的属性和方法，私有的属性和方法不能在声明的类之外访问，z在子类中也不行
  - protected 修饰受保护的属性和方法，受保护的属性和方法可以在子类中访问
  - private 和 protected
    - 当构造函数被修饰为private时，不能被继承也不能被实例化
    - 构造函数被修饰为protected时，只可以被继承

  - 修饰符和readonly还可以用在构造函数的参数中，等同于在类中定义该属性并且给属性赋值

- 类与接口

  - 通过 implements 关键字来实现，可以将复用的功能使用接口来定义，在类中具体实现
  - 在ts中接口之所以能够继承类，是因为在创建class时，同时也创建了类型，在创建类型的时候，过滤了构造函数，静态属性和方法

- 泛型

  - 在定义函数，接口和类的时候，不事先指定具体类型
  - 泛型可以代表 任意类型
  - 泛型约束，对泛型中必须包含的属性进行约束，从而约束泛型
  - 泛型和any的区别
    - any表示任意类型，泛型表示任意一种类型特定的类型
      - 例如函数接收any，返回any，并不能对参数进行约束，T可以
      - https://juejin.cn/post/6844903863791648782
      - https://juejin.cn/post/6844903887363653645

- 关键字

  - keyof，类似object.keys，获取的是interface的key
  - typeof，获取一个变量声明或对象的类型
  - is

- interface和type的区别

- > https://www.cnblogs.com/EnSnail/p/11233592.html

  - interface支持合并多个声明，type只能用&进行拼接
  - interface支持extends继承，implements实现
  - interface的key不支持计算属性，type支持

