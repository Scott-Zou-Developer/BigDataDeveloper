## Erlang程序设计

### 1.什么是并发？

#### 1.1 给并发建模

##### 1.1.1 开始模拟

**spawn：** spawn是一个Erlang基本函数，它会创建一个并发进程并返回一个进程标识符。

**spawn的调用方式：**  spawn(ModName, FuncName, [Arg1, Arg2,...,ArgN])。

- ModName：想要执行代码的模块名。
- Function：模块里的函数名。
- [Arg1, Arg2,...,ArgN]：一个列表，包含了想要执行的函数参数。
- Spawn返回的是一个进程标识符（PID，Process IDentifier），可以用来与新创建的进程交互。

#### 1.2 并发的好处

### 2.Erlang速揽





