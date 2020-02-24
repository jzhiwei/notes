# The Java Programming Language

### 简介

- 变量名称可以是Unicode字符（π）
- 所有的对象都是通过对象引用来访问的，任何看起来存有某个对象的变量实际上保存的都是该对象的引用，这种变量类型称作引用类型。
- 泛型类是一个整体，如一个类声明接受的参数为泛型类SomeClass\<Object>，那么这个参数所对应的类泛型类型只能是\<Object>，其他类型都不可以，即使是Object的子类也不行。

### 类与对象

#### 类修饰符
- 注解
- public、default
- abstract
- final
- 严格浮点（strict floating point）


#### 字段的修饰符

- 注解
- 访问修饰符
- static
- final
- transient：与对象序列化有关
- volatile：与同步和内存模型有关

字段不可以既是 final 的又是 volatile 的。有多个修饰符时，推荐使用上面的顺序排列。

#### 访问控制

private 和 protected 只能用于成员，不能用于类或接口（内部类除外）

- private：类自身可访问
- package：类自身和该类所在的包可访问
- protected：类自身、所在包或子类可访问
- public：任何类可访问

