# Spring

### Spring创建Web项目的应用上下文是通过ContextLoaderListener自动创建的，该类在Spring-WebMVC包中

### Spring源码分析

- DefaultListableBeanFactory

    默认的BeanFactory实现类，由该类创建Bean

- BeanDefinition

    XML文件中bean的定义

- BeanFactoryPostProcessor

    BeanFactory的后置处理器，用于修改BeanDefinition

- BeanPostProcessor

    Bean的后置处理器，用于修改Bean

### AOP

AOP(面向切面编程)，有两种实现方式

织入：将通知应用到切入点的过程

1. 静态织入

    AspectJ的实现方式，有自己的编译器，通过预编译的方式实现

2. 动态织入

    1. Spring AOP，通过动态代理的方式在运行期间把通知织入到切入点。使用\<aop:advisor\>标签配置。

    2. Spring + AspectJ，也是通过动态的代理的方式在运行期间织入。默认使用的方式。

切入点表达式

    execution([修饰符] 返回值类型 包名.类名.方法名(参数))
    修饰符：可省略
    返回值类型：可以使用通配符*
    包名：多级包名用.分隔；包名可以使用通配符*；省略中间的包名使用..
    类名：可以使用通配符*
    方法名：可以使用通配符*
    参数：可以使用通配符*，如果有多个参数，可以使用..

