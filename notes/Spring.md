# Spring

## Spring的核心概念
### IoC (Inversion of Control) container

IoC 也叫做 DI (Dependency Injection)，这是一个对象通过构造函数参数、工厂方法参数、或设置实例属性等方式来定义其所使用的其他对象的过程。IoC 容器在创建该对象时会注入这些依赖。这与 Bean 自己控制实例化通过直接使用构造函数来创建对象的方式相反，因此叫做控制反转。

org.springframework.beans 和 org.springframework.context 包是 IoC 容器的基础


### BeanFactory 
接口提供了一种能够管理任何类型对象的高级配置机制

### ApplicationContext 
是 BeanFactory 的子接口，增加了以下功能
- 更容易集成使用 Spring 的 AOP
- 消息资源处理（在国际化中使用）
- 事件发布
- 特定于应用层的上下文，例如在 web 应用中使用 WebApplicationContext

ApplicationContext 的实现类允许把在容器外面创建的对象（用户创建的）注册到容器中。通过 getBeanFactory() 获取 BeanFactory 的实现类，然后通过 registerSingleton(..) 和 registerBeanDefinition(..) 注册到容器中。

### Configuration Metadata

告诉IoC容器怎样实例化、配置和组装一个对象。支持三种方式

- XML-based configuration

    \<import resource=""\/\>：导入其他的配置文件，资源的路径是相对路径，\/会被忽略，但是最好还是不要使用\/

- Annotation-based configuration
- Java-based configuration  

    @Configuration  
    @Bean   
    @Import     
    @DependsOn

### BeanDefinition

在容器的内部，bean 的定义（XML文件中\<bean\/\>的定义) 表示成 BeanDefinition对象

- id：指定该 bean 的唯一标识，不可重复    
- name：指定 bean 的别名，可以有多个，中间使用,或;或空格分隔
    
### Instantiating Beans
- 通过构造方法实例化 bean
- 通过静态工厂方法实例化 bean
- 通过实例工厂方法实例化 bean

Spring 默认预实例化单例 bean，好处是在容器创建时可以发现配置问题

### DI
- 基于构造方法参数或静态工厂方法进行依赖注入，使用\<constructor-arg \/\>元素     
    构造方法参数解析：   
    - 通过参数类型
    - 通过参数位置索引
    - 通过参数名称  
        使用 @ConstructorProperties 来指定构造参数的名称
- 基于 Setter 方法进行依赖注入，使用\<property \/\>元素  
    该方法在一个对象执行完无参的构造方法或静态工厂方法进行实例化后执行


```
Spring 容器会把<value>中的元素解析成 Properties 实例
<bean id="mappings"
    class="org.springframework.context.support.PropertySourcesPlaceholderConfigurer">

    <!-- typed as a java.util.Properties -->
    <property name="properties">
        <value>
            jdbc.driver.className=com.mysql.jdbc.Driver
            jdbc.url=jdbc:mysql://localhost:3306/mydb
        </value>
    </property>
</bean>
```
idref element
```
方式一：
<bean id="theTargetBean" class="..."/>

<bean id="theClientBean" class="...">
    <property name="targetName">
        <idref bean="theTargetBean"/>
    </property>
</bean>


方式二：
<bean id="theTargetBean" class="..." />

<bean id="client" class="...">
    <property name="targetName" value="theTargetBean"/>
</bean>

两种方式作用相同，但是方式一要好于方式二。方式一会在部署时进行验证 bean 是否存在
```








- - -
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


## SpringMVC

M(Model): 业务模型，处理业务请求

HandlerMapping

HandlerAdapter

ViewResolver

V(View): 处理视图

C(Controller): DispatcherServlet.接收和分发请求，响应结果

