# MyBatis

轻量级的ORM框架，有两套配置文件，一是全局配置文件，二是实体对象的映射配置文件

### MyBatis的架构

XML配置文件 -> SqlSessionFactory -> SqlSession -> Executor -> MappedStatement

### 语法

#{}

- 相当于JDBC SQL语句中的占位符(?)
- 会对参数的类型进行解析，如传入的是String类型，则会加上''引号
- 如果传入的参数是简单数据类型，参数名可以任意

${}

- 相当于JDBC SQL语句中的连接符(+)
- 不会对参数类型进行解析，会原样替换参数
- 如果传入的参数是简单数据类型，参数名必须是value

#### 主键返回

使用<selectKey>
- keyProperty: 指定返回的主键存储在对象中的哪个属性
- order: 指定执行顺序。AFTER表示在插入语句之后执行