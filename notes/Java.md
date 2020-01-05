
### 监听器

监听对象的创建(initialized)和销毁(destroyed)
- ServletContextListener
- HttpSessionListener
- ServletRequestListener

监听对象属性的增加(attributeAdded)、删除(attributeRemoved)和替换(attributeReplaced)
- ServletContextAttributeListener
- HttpSessionAttributeListener
- ServletRequestAttributeListener

HttpSession绑定对象(valueBound)与解绑(valueUnbound)
- HttpSessionBindingListener: 该接口不需要在web.xml中注册，由实体类来实现该接口，当把一个实现该接口的实体类放入到HttpSession中，会触发valueBound方法。如果从HttpSession中移除，则触发valueUnbound方法。

HttpSession的钝化(sessionWillPassivate)与活化(sessionDidActivate)
- HttpSessionActivationListener: 该接口不需要在web.xml中注册，由实体类实现该接口，如果一个实体对象绑定了Session，当Session被钝化或活化时，会通知该对象。如果该对象想同时和Session钝化或活化，还需要实现Serializable接口。

Session的钝化和活化：Session默认存储在服务器的内存中，当Session数量过多时，会影响服务器性能，服务器会把不经常使用的Session保存到文件系统或数据库中，该过程称为Session的钝化，该过程由Web服务器自动完成。当被使用时反序列化到内存中称为Session的活化。

Tomcat中两种Session钝化管理器
1. org.apache.catalina.session.StandardManager
    - 当Tomcat服务器被关闭或重启时，tomcat服务器会将内存中的Session对象钝化到服务器的文件系统中；
    - 另一种情况是Web应用程序被重新加载时，内存中的Session对象也会被钝化到服务器的文件系统中
    - 钝化后的文件保存在Tomcat下的/work/Catalina/hostname/applicationname/SESSION.ser

2. org.apache.catalina.session.PersistentManager

    - 首先在钝化的基础上进行了扩展。前两种情况与StandardManager一样，第三种情况可以配置主流内存的Session对象数目，将不长使用的Session对象保存到文件系统或数据库，当使用时再重新加载。
    - 默认情况下，Tomcat提供两个钝化驱动类：

            org.apache.Catalina.FileStore
            org.apache.Catalina.JDBCStore

- - -
### 过滤器

对HttpRequest和HttpResponse进行过滤

- init(): Web容器创建过滤器实例后调用，该方法可以读取web.xml中配置的过滤器参数
- doFilter(): 当用户请求访问与过滤器关联的URL时调用。

        如果请求的资源URL关联了多个过滤器，会形成一个过滤器链，顺序按照web.xml中配置的顺序来执行。

        FilterChain: chain.doFilter()
        该方法表示放行，将请求传给下一个过滤器，如果没有下一个过滤器，会请求资源。

        发送请求会执行放行方法前的代码，返回响应会继续执行放行方法后面的代码。

- destory(): Web容器销毁过滤器实例前调用，用来释放过滤器占用的资源。

过滤器的分类

Servlet2.5
- REQUEST: 用户直接访问页面或者使用HttpResponse的sendRedirect重定向页面时
- FORWARD: 目标资源是通过RequestDispatcher的forward访问时或使用\<jsp:forward\>
- INCLUDE: 目标资源是通过RequestDispatcher的include访问时或使用\<jsp:include\>
- ERROR: 目标资源是通过声明式异常处理机制调用时
Servlet3.0
- ASYNC: 支持异步处理