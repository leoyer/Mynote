# Mynot
# Spring
>spring的设计目的是简化企业应用开发; 为开发者提供企业应用及web应用涉及的持久化，事务，消息中间件，分布式计算的集中管理；spring由核心/组件/应用三部分组成；IOC，AOP是其核心。

##IoC
>简单的来说就是将对象之间的关系交给容器统一管理，实现依赖注入。其实现过程分为以下几个步骤: 
- BeanDefinition的Resource定位
- BeanDefinition的解析
- 将解析的bean交给容器管理(即将bean存入类似xxxbeanFactory类中的Map集合中)
- IoC依赖注入(默认在加载时不会进行依赖注入，而是在第一次使用具体的类时才会注入。当然也可以设置lazy-init属性)

---
#####IOC装配过程:

![IOC装配过程](http://resume.leoyer.com/IOC-1.png)

#####IOC依赖注入过程:

![IOC依赖注入过程](http://resume.leoyer.com/IOC-2.png)

#####IOC容器的接口图：

![IOC容器的接口图](http://resume.leoyer.com/IOC-4.png)

>  从接口的继承关系上来看，spring 遵守了单一职责原则，每一个接口只负责新增一个新的功能点，可以根据功能上的需要，选择不同的接口去实现。

#####FileSystemApplicationContext容器：

![FileSystemApplicationContext容器](http://resume.leoyer.com/IOC-3.png)

>ApplicationContext 接口：  spring context核心接口 , 其由 BeanFactory 接口的子接口扩展而来，因此具有 BeanFactory 的所有功能，又因为其继承了 MessageSource, ApplicationEventPublisher, ResourcePatternResolver 接口，因此又具有国际化消息解析，资源加载， ApplicationEvent 事件发布的功能。在此接口自己定义的方法中提供了获取父 ApplicationContext 、获取自动装配 bean 工厂，获取启动时间和显示名称这四项功能.每往下一层都有新的特性。在做设计时可以吸收这种思想，从而达到增加程序扩展性，解偶等效果。

#####最后就不得不以下IOC容器的FactoryBean扩展机制 
>原理说出来也好简单，所有FactoryBean 实现FactoryBean接口的getObject()函数。Spring容器getBean(id)时见到bean的定义是普通class时，就会构造该class的实例来获得bean，而如果发现是FacotryBean接口的实例时，就通过调用它的getObject()函数来获得bean，仅此而以.......可见，很重要的思想，可以用很简单的设计来实现。 

Spring的AOP、ORM、事务管理、JMX、Quartz、Remoting、Freemarker、Velocity，都靠FacotryBean的扩展，FacotryBean几乎遍布地上：只不过当年对这类factoryBean比较麻木不仁，不问原理的照搬照用了。

```
<bean id="sessionFactory" class="org.springframework.orm.hibernate3.LocalSessionFactoryBean"/>  
  
<bean id="baseDAOService"  
class="org.springframework.transaction.interceptor.TransactionProxyFactoryBean"/>  
```

考察一个典型的FactoryBean：  
    一般会有两个变量，三个接口：  
    一个setter函数注入需要改装的pojo，一个内部变量保持装配后的对象returnOjbect。  
    implements三个接口 ：FactoryBean,InitializingBean和BeanFactoryAware 。  


----

spring boot  /Grails/Spring Roo/Spring-Loade
Spring的JSP标签除了支持WebSockets和HTML5
JavaConfig
Gradle
