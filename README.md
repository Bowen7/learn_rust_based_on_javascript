# learn_rust_based_on_javascript

从一名惯用 JavaScript 的开发者的角度出发，学习 Rust

# 基本编程概念

## 变量

在 ES6 中，我们摒弃了之前万能的 `var` ，取而代之的是 `let` 和 `const` ，而 Rust 中，定义变量同样是使用 `let` 和 `const` （当然，这并非 ES6 或 Rust 的首创，只是英文的词汇）

与 JavaScript 不同，Rust 中的变量默认都是不可变的（immutable），即使是使用 `let` 。如果想声明一个可变的变量，需要加上关键字 `mut` （mutable），如下：

```rust
let mut x = 0;
```

ES6 中，`const` 和 `let` 的差别仅限于 `const` 声明的变量为常量，不能改变。而 Rust 中 `const` 和 `let` 的差别就更大了：

- `const` 不能使用 `mut`
- `const` 常量必须声明类型，如下

```rust
const A = 1; // error
const A: u32 = 1; // ok
```

- `let` 可以重复声明，像 JavaScript 中的 `var` 一样：

```rust
let x = 5;
let x = x + 1; // it's ok, x = 6
```

Rust 中的 `const` 和 `let` 还支持表达式赋值，如下：

```rust
let a = {
    let _a = 1;
    _a // 注意：没有分号 
};
const A: u32 = {
    let _a = 1;
    _a // 注意：没有分号
};
```

表达式最后的 _a 不带分号，表示返回值

> Tips：`let` 重复声明与 使用 `mute` 的区别：

我们可以使用多次 `let` 对变量进行赋值，也可以在最开始声明变量时使用 `let mut` 。这二者的区别在与 使用 `let mut` 声明的变量，在修改时，变量的类型不能改变，如下：

```rust
let a = 1;
let a = "1"; // it's ok

let mut b = 1;
b = "1"; // error
```

## 数据类型

像 JavaScript 的数据类型分为基本数据类型和复杂数据类型一样，Rust 的数据类型也有两类：标量类型和复合类型

### 标量类型

与 JavaScript 的基本数据类型一致，表示一个单独的值。Rust 的标量类型又分为 4 小类：

- 整型
- 浮点型
- 布尔型
- 字符型

其中，整型又分为 `i8`、`u8` 、`i16`、 `u16` 等等。`i` 表示有符号，即有正负，`u` 表示无符号。后面的数字表示长度，如 `i8`，它能表示 -255 至 255 的值

浮点型则分为两类：`f32`、`f64`，默认为 `f64`

### 复合类型

复合类型可以将多个值组合进一个类型。Rust 有两种原生的复合类型：元组（tuples）和数组（array）

元组：元组可以将多个不同类型的值组合在一起，它的长度自声明后不允许改变：

```rust
fn main() {
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;

    println!("The value of y is: {}", y);
}
```

可以通过这种方式访问元组的元素：`let (x, y, z) = top;` ，这种语法有些类似 ES6 的解构赋值

元组也可根据其索引访问：

```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);

    let five_hundred = x.0;

    let six_point_four = x.1;

    let one = x.2;
}
```

数组：Rust 的数组元素必须是同类型的，而且，与元组一样，它的长度是固定的，声明后不能改变（这与 JavaScript 非常不同）

访问数组元素则与 JavaScript 一致：

```rust
fn main() {
    let a = [1, 2, 3, 4, 5];

    let first = a[0];
    let second = a[1];
}
```

# 函数

在 JavaScript 中，我们使用 `function` 关键字声明函数（或者使用箭头函数）；Rust 则是使用 `fn` 关键字

在 JavaScript 中，函数命名通常使用 驼峰命名法（Camel-Case），Rust 则是使用 蛇形命名法（snake case），即所有字母都是小写，空格由下划线替代

一个基本的函数：

```rust
fn printX(x: i32) {
    println!("The value of x is: {}", x);
}
```

有返回值的函数：

```rust
fn five1() -> i32 {
    return 5;
}

fn five2() -> i32 {
    5
}
```

当函数有返回值时，我们需要定义返回值的类型，通过 `→ type` 的方式定义。

上面两种方式都可以使函数返回数字 5，第一种我们在 JavaScript 中已经知晓了，不再赘述。而在 Rust 中，函数如果没有 `return`，则会隐式地返回最后的表达式，在前面的变量一章，已经介绍过表达式了，在函数 `five2` 中，`5` 就是一个单独的表达式。

甚至可以无限嵌套表达式

```rust
fn five() -> i32 {
    {
        {
            {
                5
            }
        }
    }
}
```

> Tips：表达式后没有分号

```rust
fn five() -> i32 {
    5;
}
```

上面的函数在定义时就会报错，因为在 `5` 后面加上了分号，它不再是一个表达式，而是一段语句。所以函数没有返回值，与定义的返回类型 `i32` 冲突

# 注释

与 JavaScript 相同：

```rust
fn main() {
    // nothing
}
```

