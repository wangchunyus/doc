# Spring 篇



## IOC 



#### General：

+ **ioc实现的方式**
  + 纯xml形式（bean信息定义全部配置到xml中管理）
  + xml+注解形式
  + 纯注解形式
+ **IOC容器的启动方式**
  + 带有xml的启动方式
    + JavaSE：`ApplicationContext app =new ClassPathXmlApplicationContext("beans.xml");`
    + JavaWeb: `ContextLoadListener(配置监听器 加载xml)`
  + 纯注解形式
    + JavaSE：`ApplicationContext app =new AnnotationConfigApplicationContext(springConfig.class);` 
    + JavaWeb: `ContextLoadListener(配置监听器 加载xml)`

+  **Bean作用域**
  +  Singleton  - 单例模式(销毁容器时，对象就被销毁)
  + Prototype -  原型模式（多例）/ 每次都会生成一个新的bean （spring只负责创建bean，不负责销毁。GC回收）
  + Request
  + Seesion
  + Application
  + Websocket

#### Lazy-Init  延迟加载

ApplicationContext容器中默认是在启动服务器时将所有的 作用域为’singleton‘ 的bean提前初始化。

+ **配置延迟加载**
  + xml方式： 在xml中 `<bean id ='Test1' class = 'com.edu.....'  lazy-init = 'true'>`开启了延迟加载
  + 在纯注解方式： 可以在Test1 的这个实体类上 加上@Lazy 这个注解 表示开启延迟加载

+ 应用场景
  + 开启延迟加载在一定程度上可以提高容器启动和服务器运转性能。
  + 对于不常 使用的Bean设置延迟加载， 可以节省资源消耗。

​             