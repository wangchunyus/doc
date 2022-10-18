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

+ **应用场景**
  + 开启延迟加载在一定程度上可以提高容器启动和服务器运转性能。
  + 对于不常 使用的Bean设置延迟加载， 可以节省资源消耗。

#### FactoryBean 和 BeanFactory             

+ BeanFactory 接口是容器的顶级接口，定义了容器的一些基础行为，负责产生和管理Bean的工厂，ApplicationContext等属于它的子接口。

+ FactoryBean 属于Spring中的工厂Bean， 可以生产某一个类型的Bean实例给我们，也就说我们可以自定义Bean的创建过程。

  + FactoryBean 是一个接口，提供了三个方法 

    +   T  getObject()  throws Exception;   //返回使用FactoryBean创建的实例

    +   class<?> getObjectType();  //返回创建Bean的类型

    +   default boolean isSingleton() {

        return true;     

      } //返回作用域是否单例

  + FactoryBean 的使用-->  在 myBatis中的 SqlSessionFactoryBean 中使用| spring自身也有 70多个bean使用过。

  

#### SpringBean的后置处理器

+ **spring 提供了两种处理bean的扩展接口**

  + BeanPostProcessor **（默认是会对整个spring 容器中的所有bean进行处理）**

    <!--源码-->

    + ```
      public interface BeanPostProcessor {
      
      // 初始化方法前 执行 ，主要做一些生成bean前的一些前置执行
         @Nullable
         default Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
            return bean;
         }
      
        // 初始化方法后 执行 ，主要做一些生成bean后的一些后置执行
         @Nullable
         default Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
            return bean;
         }
      ```

  + BeanFactoryPostProcessor（**BeanFactory级别的处理，是针对整个Bean的⼯⼚进⾏处理，典型应**

    **⽤:PropertyPlaceholderConfifigurer**）

    +   PropertyPlaceholderConfifigurer： 源码中处理 封装xml bean信息的 BeanDefinition 中的一些 properties中的信息  例如：  dataSource 中的一些  数据 ${username} / ${password} 的信息进行 转换后 在封装到 BeanDefinition中 

#### Spring-IoC源码

+ Bean对象创建的关键方法是 AbstractApplicationContext  类中那个的 refaresh() 方法  核心方法



#### Spring-循环依赖问题

解决方案讲解地址： [https://blog.csdn.net/qq_40277163/article/details/124399551]( https://blog.csdn.net/qq_40277163/article/details/124399551)

