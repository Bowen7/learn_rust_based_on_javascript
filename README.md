# learn_rust_based_on_javascript

从一名惯用 JavaScript 的开发者的角度出发，学习 Rust

## 基本编程概念

### 变量

在 ES6 中，我们摒弃了之前万能的 `var` ，取而代之的是 `let` 和 `const` ，而 Rust 中，定义变量同样是使用 `let` 和 `const` （当然，这并非 ES6 或 Rust 的首创，只是英文的词汇）

与 JavaScript 不同，Rust 中的变量默认都是不可变的（immutable），即使是使用 `let` 。如果想声明一个可变的变量，需要加上关键字 `mut` （mutable），如下：

```rust
let mut x = 0;
```

ES6 中，`const` 和 `let` 的差别仅限于 `const` 声明的变量为常量，不能改变。而 Rust 中 `const` 和 `let` 的差别就更大了

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

Tips：`let` 重复声明与 使用 `mute` 的区别：

我们可以使用多次 `let` 对变量进行赋值，也可以在最开始声明变量时使用 `let mut` 。这二者的区别在与 使用 `let mut` 声明的变量，在修改时，变量的类型不能改变，如下：

```rust
let a = 1;
let a = "1"; // it's ok

let mut b = 1;
b = "1"; // error
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