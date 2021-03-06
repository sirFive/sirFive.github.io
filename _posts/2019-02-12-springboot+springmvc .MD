---
layout: post
title: "springBoot+springMvc"
date: 2019-02-12
description: "复习--springBoot+springMvc"
tag: 复习
---
### 1.springBoot
#### 1.什么是 Spring Boot
Spring Boot是spring开源组织下的子项目，是spring组件一站式解决方案。主要是简化了spring的使用难度和简化了繁重的配置，提供了各种启动器，使开发者更容易上手。
#### 2.为什么要用 Spring Boot
独立运行、配置简化、自动配置、无代码生成和xml配置、应用监控、上手容易。
#### 3.SpringBoot 的核心注解是哪个？它主要由哪几个注解组成的
启动类上面的注解是@SpringBootApplication，它也是SpringBoot的核心注解，主要组合包含了以下 3 个注解：  
@SpringBootConfiguration：组合了 @Configuration 注解，实现配置文件的功能。  
@EnableAutoConfiguration：开启自动配置的功能，也可以关闭某个自动配置的选项，如关闭数据源自动配置功能： `@SpringBootApplication(exclude = { DataSourceAutoConfiguration.class })`。  
@ComponentScan：Spring组件扫描。
#### 4.SpringBoot 自动配置原理
@EnableAutoConfiguration 开启自动配置，它使用@import(EnableAutoConfigurationImportSelector.class)注解来完成导入配置的功能，导入的类使用了SpringFactoriesLoader.loadFactoryNames方法来
加载类路径及所有jar包下META-INF/spring.factories配置中映射的自动配置的类。
这些自动配置类又通过@EnableConfigurationProperties 注解支持通过xxxxProperties读取application.properties/application.yml属性文件中我们配置的值。如果我们没有配置值，就使用默认值，这就是所谓约定>配置的具体落地点。
#### 5.SpringBoot 中的 Starters
Starters可以理解为启动器，它包含了一系列可以集成到应用里面的依赖包，你可以一站式集成Spring及其他技术，而不需要到处找示例代码和依赖包。如`spring-boot-starter-web`,
它集成了`spring-web`,`spring-webmvc`,`spring-boot-starter-json`等模块。
#### 6.如何在 SpringBoot 启动的时候运行一些特定的代码
可以实现接口 ApplicationRunner 或者 CommandLineRunner，这两个接口实现方式一样，它们都只提供了一个 run 方法。
#### 7.SpringBoot 配置加载顺序
在 SpringBoot 里面，可以使用以下几种方式来加载配置。1）properties文件；2）YAML文件；3）系统环境变量；4）命令行参数；等。
#### 8.参考链接
[参考文章1](https://www.jianshu.com/p/63ad69c480fe) 
[参考文章2](https://www.cnblogs.com/3xmq/p/springboot.html)

### 2.SpringMVC
#### 1.什么是SpringMVC
SpringMVC是一个基于MVC架构、用来简化web应用程序开发的应用开发框架，它是Spring的一个模块,无需中间整合层来整合。
#### 2.SpringMVC的流程
（1）用户发送请求至前端控制器DispatcherServlet；  
（2） DispatcherServlet收到请求后，调用HandlerMapping处理器映射器，请求获取Handle；  
（3）处理器映射器根据请求url找到具体的处理器，生成处理器对象及处理器拦截器(如果有则生成)一并返回给DispatcherServlet；  
（4）DispatcherServlet通过HandlerAdapter处理器适配器调用处理器；  
（5）执行处理器(Handler，也叫后端控制器)； 
（6）Handler执行完成返回ModelAndView；  
（7）HandlerAdapter将Handler执行结果ModelAndView返回给DispatcherServlet；  
（8）DispatcherServlet将ModelAndView传给ViewResolver视图解析器进行解析；  
（9）ViewResolver(包括InternalResourceViewResolver、XmlViewResolver、BeanNameViewResolver)解析后返回具体View；  
（10）DispatcherServlet对View进行渲染视图（即将模型数据填充至视图中）；  
（11）DispatcherServlet响应用户。  
![springMvc流程图](/images/article/javaWeb/springmvc-process.jpg "springMvc流程图")  
#### 3.Spring MVC 常用的 5 个注解
@RequestMapping :用于处理请求 url 映射的注解，表示类中的所有响应请求的方法都是以该地址作为父路径。  
@RequestBody :注解实现接收http请求的json数据，将json转换为java对象。  
@ResponseBody :注解实现将controller方法返回对象转化为json对象响应给客户。  
@PathVariable :请求路径参数。  
@RequestParam :方法参数。
#### 4.SpringMVC的主要组件
（1）前端控制器 DispatcherServlet（不需要程序员开发）  
作用：接收请求、响应结果，相当于转发器，有了DispatcherServlet 就减少了其它组件之间的耦合度。  
（2）处理器映射器HandlerMapping（不需要程序员开发）  
作用：根据请求的URL来查找Handler  
（3）处理器适配器HandlerAdapter  
注意：在编写Handler的时候要按照HandlerAdapter要求的规则去编写，这样适配器HandlerAdapter才可以正确的去执行Handler。  
（4）处理器Handler（需要程序员开发）  
（5）视图解析器 ViewResolver（不需要程序员开发）  
作用：进行视图的解析，根据视图逻辑名解析成真正的视图（view）  
（6）视图View（需要程序员开发jsp）  
View是一个接口， 它的实现类支持不同的视图类型（jsp，freemarker，pdf等等）
#### 5.SpringMvc和AJAX相互调用方式
通过Jackson框架就可以把Java里面的对象直接转化成Js可以识别的Json对象。具体步骤如下 ：  
（1）加入Jackson.jar  
（2）在配置文件中配置json的映射  
（3）在接受Ajax方法里面可以直接返回Object,List等,但方法前面要加上@ResponseBody注解。
#### 6.Spring MVC的异常处理
将异常抛给Spring框架，由Spring框架来处理；我们只需要配置简单的异常处理器，在异常处理器中添视图页面即可。
#### 7.配置拦截get方式提交的方法
在@RequestMapping注解里面加上method=RequestMethod.GET。
#### 8.SpringMvc中函数的返回值类型
返回值可以有很多类型,有String, ModelAndView。ModelAndView类把视图和数据都合并的一起的，但一般用String比较好。
#### 9.springMVC和struts2的区别
（1）springMvc的入口是一个servlet即前端控制器（DispatchServlet），而struts2入口是一个filter过虑器（StrutsPrepareAndExecuteFilter）。  
（2）springMvc是基于方法开发(一个url对应一个方法)，请求参数传递到方法的形参，可以设计为单例或多例(建议单例)，struts2是基于类开发，传递参数是通过类的属性，只能设计为多例。  
（3）Struts采用值栈存储请求和响应的数据，通过OGNL存取数据，springMvc通过参数解析器是将request请求内容解析，并给方法形参赋值，将数据和视图封装成ModelAndView对象，最后又将ModelAndView
中的模型数据通过request域传输到页面。Jsp视图解析器默认使用jstl。
#### 10.SpringMVC怎么设定重定向和转发
（1）在返回值前面加"forward:"就可以让结果转发,譬如`forward:user.do?name=method4`  
（2）在返回值前面加"redirect:"就可以让返回值重定向,譬如`redirect:http://www.baidu.com`
#### 11.SpringMvc里面拦截器是的写法
有两种写法,一种是实现HandlerInterceptor接口；另外一种是继承适配器类,接着在接口方法当中，实现处理逻辑，
然后在SpringMvc的配置文件中配置拦截器即可。
```
<!-- 配置SpringMvc的拦截器 -->
<mvc:interceptors>
 
    <!-- 配置一个拦截器的Bean就可以了 默认是对所有请求都拦截 -->
    <bean id="myInterceptor" class="com.xie.action.MyHandlerInterceptor"></bean>
 
    <!-- 只针对部分请求拦截 -->
    <mvc:interceptor>
 
       <mvc:mapping path="/modelMap.do" />
 
       <bean class="com.xie.action.MyHandlerInterceptorAdapter" />
 
    </mvc:interceptor>
 
</mvc:interceptors>
```
#### 12.如何解决POST和GET请求中文乱码问题
（1）解决post请求乱码问题：在web.xml中加入CharacterEncodingFilter过滤器。  
（2）get请求中文参数出现乱码解决方法有两个：  
①修改tomcat配置文件添加编码与工程编码一致; 
```
<ConnectorURIEncoding="utf-8" connectionTimeout="20000" port="8080" protocol="HTTP/1.1" redirectPort="8443"/>
``` 
②另外一种方法对参数进行重新编码。
```
String userName = new String(request.getParamter("userName").getBytes("ISO8859-1"),"utf-8")
```
#### 13.SpringMvc的控制器是不是单例模式,如果是,有什么问题,怎么解决？
是单例模式,所以在多线程访问的时候有线程安全问题,不要用同步,会影响性能的,解决方案是在控制器里面不能写字段。
#### 14.在方法里面得到Request,或者Session
直接在方法的形参中声明request,SpringMvc就自动把request对象传入。
#### 15.参考链接
[参考文章](https://blog.csdn.net/a745233700/article/details/80963758)
