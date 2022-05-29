链接：[尚硅谷SSM实战演练丨ssm整合快速开发CRUD_哔哩哔哩_bilibili](https://www.bilibili.com/video/av21045215)

CRUD:create retrieve update delete

## MVC

MVC核心思想：模型-视图-控制器

​		Spring MVC是服务到工作者思想的实现。前端控制器是DispatcherServlet；应用控制器拆为处理器映射器(Handler Mapping)进行处理器管理和视图解析器(View Resolver)进行视图管理；支持本地化/国际化(Locale)解析及文件上传等；提供了非常灵活的数据验证、格式化和数据绑定机制；提供了强大的<u>约定大于配置</u>(惯例优先原则)的契约式编程支持。

1.让我们能非常简单的设计出干净的Web层;
2.进行更简洁的Web层的开发;
3.天生与Spring框架集成(如IoC容器、AOP等) ; 
4.提供强大的约定大于配置的契约式编程支持;
5.能简单的进行Web层的单元测试;
6.支持灵活的URL到页面控制器的映射;
7.非常容易与其他视图技术集成，如jsp. Velocity. FreeMarker等等， 因为模型数据不放在特定的API里，而是放在一个Model里(Map数据结构实现，因此很容易被其他框架使用) ;
8.非常灵活的数据验证、格式化和数据绑定机制，能使用任何对象进行数据绑定，不必实现特定框架的API;
9.支持灵活的本地化等解析;
10.更加简单的异常处理;
11.对静态资源的支持;
12.支持Restful风格。

### MVC请求流程

![image-20220525090332821](D:\typora_mds\2022！\Resources\image-20220525090332821.png)

1. 首先用户发送请求， 请求被SpringMvc前端控制器(DispatherServlet) 捕获;
2. 前端控制器(DispatherServlet)对请求URL解析获取请求URI，根据URI，调用HandlerMapping;
3. 前端控制器(DispatherServlet)获得返回的HandlerExecutionChain (包括Handler对象以及 Handler对象对应的拦截器) ;
4. DispatcherServlet根据获得的HandlerExecutionChain,选择-个合适的HandlerAdapter。 (附注: 如果成功获得HandlerAdapter后，此时将开始执行拦截器的preHandlel..)方法) ;
5. HandlerAdapter根据请求的Handler适配并执行对应的Handler; HandlerAdapter(提取Request中的模型数据，填充Handler入参,开始执行Handler (Controller)。 在填充Handler的入参过程中, 根据配置, Spring将做-些额外的工作:
   		HttpMessageConveter:将请求消息 (如Json. xml等数据) 转换成-个对象，将对象转换为指定的响应信息。
      		数据转换:对请求消息进行数据转换。如String转换成Integer. Double等数据格式化:
      		数据格式化。如将字符串转换成格式化数字或格式化日期等
      		数据验证：验证数据的有效性(长度、格式等)，验证结果存储到BindingResult或Error中)
6. Handler执行完毕,返回一个ModelAndView(即模型和视图)给HandlerAdaptor
7. HandlerAdaptor适配器将执行结果ModelAndView返回给前端控制器。
8. 前端控制器接收到ModelAndView后，请求对应的视图解析器。
9. 视图解析器解析ModelAndView后返回对应View;
10. 渲染视图并返回渲染后的视图给前端控制器。

### 环境搭建

依赖坐标添加

```xml
<!--需要引入的依赖：spring-web，spring-mvc，servlet-->
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-web -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>5.3.19</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.3.18</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.1.0</version>
      <scope>provided</scope>
    </dependency>

```

```xml
<!--插件-->
<plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>2.3.2</version>
        <configuration>
          <source>1.8</source>
          <target>1.8</target>
          <encoding>UTF-8</encoding>
        </configuration>
      </plugin>
      <plugin>
        <groupId>org.eclipse.jetty</groupId>
        <artifactId>jetty-maven-plugin</artifactId>
        <version>9.4.27.v20200227</version>
        <configuration>
          <scanIntervalSeconds>10</scanIntervalSeconds>
          <httpConnector>
            <port>8080</port>
          </httpConnector>
          <webAppConfig>
            <contextPath>/springmvc01</contextPath>
          </webAppConfig>
        </configuration>
      </plugin>
    </plugins>
```

配置servlet.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns="http://java.sun.com/xml/ns/javaee"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
         http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
         version="3.0">
  <filter>
    <description>char encoding filter</description>
    <filter-name>encodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
      <param-name>encoding</param-name>
      <param-value>UTF-8</param-value>
    </init-param>
  </filter>
  <filter-mapping>
    <filter-name>encodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>

  <!--Servlet请求分发器-->
  <servlet>
    <servlet-name>springMvc</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:servlet-context.xml</param-value><!--需要在resource目录下的servlet-context.xml文件-->
    </init-param>
    <!--表示启动容器时初始化Servlet-->
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>springMvc</servlet-name>
    <!--这是拦截请求，"/"代表拦截所有请求，"*.do"表示拦截所有.do请求-->
    <url-pattern>*.do</url-pattern>
  </servlet-mapping>
</web-app>

```

控制器

```java
package com.xxxx.springmvc.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.servlet.ModelAndView;

@Controller
public class HelloController {
    /**
     * 请求地址映射
     * @return
     */
    @RequestMapping("/hello")//请求路径
    public ModelAndView hello(){
        ModelAndView modelAndView = new ModelAndView();
        //设置数据
        modelAndView.addObject("hello","Hello SpringMVC");
        //设置视图名称
        modelAndView.setViewName("hello");
        return modelAndView;
    }
}
```

视图

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 祝金良
  Date: 2022/5/25
  Time: 11:24
  To change this template use File | Settings | File Templates.
--%>
<%@ page  language="java"  import="java.util.*" pageEncoding="UTF-8" %>
<%
    String path = request.getContextPath();
    String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>
<!DOCTYPE HTML>
<html>
<head>
    <base href="<%=basePath %>">
    <title>My Jsp page</title>
    <meta http-equiv="pragma" content="no-cache">
    <meta http-equiv="cache-control" content="no_cache">
    <meta http-equiv="expires" content="0">
    <meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
    <meta http-equiv="description" content="This is my page">
</head>
<body>
    ${hello}
</body>
</html>
```

运行：在maven添加命令行: `jetty:run`

### URL地址映射

通过注解`@RequestMapping`将请求地址与方法进行绑定，可以在类级别和方法级别声明。类级别的注解负责将一个特定的请求路径映射到一个控制器上，将url和类绑定；通过方法级别的注解可以细化映射，能够将一个特定的请求路径映射到某个具体的方法上，将url和类的方法绑定。

#### 1.映射单个路径

```java
/**
 * @RequsetMapping : 将请求路径与方法绑定，可以声明在类级别和方法级别
 *      使用方式：
 *          @RequestMapping("/请求url")
 *          @RequestMapping(value = "/请求url")
 */
@Controller
public class UrlController {
    @RequestMapping("/test01")
    public ModelAndView test01(){
        ModelAndView mv = new ModelAndView();
        mv.addObject("hello","test01");
        mv.setViewName("hello");
        return mv;
    }
    
    @RequestMapping("test02")//不加 / 也可以
    public ModelAndView test02(){
        ModelAndView mv = new ModelAndView();
        mv.addObject("hello","test02");
        mv.setViewName("hello");
        return mv;
    }
}
```

#### 2.映射多个url

```java
@Controller
public class UrlController {
	@RequestMapping("test03_01","test03_02")//支持一个方法绑定多个url
    public ModelAndView test03(){
        ModelAndView mv = new ModelAndView();
        mv.addObject("hello","test03");
        mv.setViewName("hello");
        return mv;
    }
    
    @RequestMapping(value = {"test03_01","test03_02"})//添加value，使用数组
    public ModelAndView test03(){
        ModelAndView mv = new ModelAndView();
        mv.addObject("hello","test03");
        mv.setViewName("hello");
        return mv;
    }
}
```

#### 3.映射url在控制器上

用于类上：父路径

```java
/**	访问路径：localhost:8080/springmvc01/url/test01
*/
@Controller
@RequestMapping("url")//父路径
public class UrlController {
    @RequestMapping("/test01")
    public ModelAndView test01(){
        ModelAndView mv = new ModelAndView();
        mv.addObject("hello","test01");
        mv.setViewName("hello");
        return mv;
    }
}
```

**通过参数名称访问**

```java
//	访问路径：localhost:8080/springmvc01/url?test05
@Controller
@RequestMapping("url")//父路径
public class UrlController {
    @RequestMapping(param="test01")
    public ModelAndView test01(){
        ModelAndView mv = new ModelAndView();
        mv.addObject("hello","test01");
        mv.setViewName("hello");
        return mv;
    }
}
```

#### 4.设置url请求方式

可以通过method属性设置支持的请求方式，如`method=RequestMethod.POST`;如设置多种请求方式，以大括号包围，逗号隔开即可。

```java
/*默认get 和post都支持
如果设置了请求方式：必须按指定方式
		localhost:8080/springmvc01/url/test06   是不被支持的
*/
@RequestMapping(value="test06",method = RequestMethod.POST)
    public ModelAndView test06(){
        ModelAndView mv = new ModelAndView();
        mv.addObject("hello","test06");
        mv.setViewName("hello");
        return mv;
    }
```

### 参数绑定

客户端传递数据到后台需要的参数绑定，支持五种类型

| 基本类型 | String \| Date | 数组 | JavaBean | 集合(List,Set,Map) |
| -------- | -------------- | ---- | -------- | ------------------ |

#### 基本类型

```java
@Controller
public class ParamController {
    @RequestMapping("/data01")
    public void data01(int age,double money){
        System.out.println(age);
        System.out.println(money);
    }
}
```

通过浏览器输入参数：`http://localhost:8080/springmvc01/data01?age=10&money=23.5`

控制台输出

```
[INFO] Started Jetty Server
10
23.5
```

如果只传递1个参数，会报<font size=5px>500</font>错误：null不能转换为double类型

**设置参数默认值：**

```java
/**
     * @RequestParam 标记一个注解为形参,避免基本类型为空异常
     * @param age
     * @param money
     */
    @RequestMapping("/data02")
    public void data02(@RequestParam(defaultValue = "0") int age,@RequestParam(defaultValue = "0.0")  double money){
        System.out.println(age);
        System.out.println(money);
    }
```

**设置参数别名：**

```java
@RequestMapping("/data02")
    public void data02(@RequestParam(defaultValue = "0", name="userAge") int age,@RequestParam(defaultValue = "0.0", name="UserMoney")  double money){
        System.out.println(age);
        System.out.println(money);
    }
```

在浏览器传入参数必须使用别名

`http://localhost:8080/springmvc01/data01?userAge=10&UserMoney=23.5`

#### 包装类型

使用包装类型，具有默认值null，不会报空异常

```java
@Controller
public class ParamController {
    @RequestMapping("/data01")
    public void data01(Integer age,Double money){//改成包装类型即可
        System.out.println(age);
        System.out.println(money);
    }
}
```

#### 字符串类型

```java
@Controller
public class ParamController {
    @RequestMapping("/data01")
    public void data01(String userName,String userPwd){//字符串类型也支持默认值为null
        System.out.println(userName);
        System.out.println(userPwd);
    }
}
```

#### 数组

```java
/**
     * 传递参数格式： hobbies=sing&hobbies=dance
     * @param hobbies
     */
    @RequestMapping("/data06")
    public void data06(String[] hobbies){
        for(String hobby:hobbies){
            System.out.println(hobby);
        }
    }
```

#### JavaBean类型

```java
/**
     * 客户端请求的参数类型与javaBean属性字段名保持一致
     * @param user
     */
    @RequestMapping("/data07")
    public void data07(User user){
        System.out.println(user);
    }
```

`http://localhost:8080/springmvc01/data07?id=7&userName=admin&userPwd=1234`

```
[INFO] Started Jetty Server
User{id=7, userName='admin', userPwd='1234'}
```

#### 集合

一般集合类型都需要JavaBean类型来封装

```jsp
<form action='data08' method="post">
    <input name="phoneList[0].num" value="1234556"/>
    <input name="phoneList[1].num" value="124"/>
    <button type="submit"> 提交</button>
</form>
```

### 请求域对象设置 

```java
//以下五种都可以使用：ModelAndView ,ModelMap, Model, Map, HttpServletRequest
@Controller
public class ModelController {

    @RequestMapping("/model01")
    public ModelAndView model01(){
        ModelAndView mv = new ModelAndView();
        //设置数据模型
        mv.addObject("hello","model01");
        mv.setViewName("hello");
        return mv;
    }

    @RequestMapping("/model02")
    public String model02(ModelMap modelMap){
        //设置请求域对象
        modelMap.addAttribute("hello","hello there");
        return "hello";
    }

    @RequestMapping("/model03")
    public String model03(Model model){
        //设置请求域对象
        model.addAttribute("hello","hello model03");
        return "hello";
    }

    @RequestMapping("/model04")
    public String model04(Map map){
        //设置请求域对象
        map.put("hello","hello model04");
        return "hello";
    }
    /**
     * Request 对象是内置对象，可以直接用
     */
    @RequestMapping("/model05")
    public String model05(HttpServletRequest httpServletRequest){
        httpServletRequest.setAttribute("hello","hello model05");
        return "hello";
    }
}
```

### 请求转发和重定向

spring MVC 默认使用服务器内部请求转发，也可以支持重定向页面

#### 重定向

发一个302状态码给浏览器，浏览器再请求跳转的网页

```java
@Controller
//重定向
public class ViewController {
    @RequestMapping("/view01")
    public String view01(){
        return "redirect:view.jsp";
    }

    /**
     * 重定向且传递参数
     * @return
     */
    @RequestMapping("/view02")
    public String view02(){
        return "redirect:view.jsp?uname=admin&upwd=1233445";
    }
}
```

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <h2>view页面</h2>
<h3>获取传递的参数：${param.uname} 和 ${param.upwd}</h3>
</body>
</html>
```

![image-20220525184819576](D:\typora_mds\2022！\Resources\image-20220525184819576.png)

如果直接url传递的参数有中文：会出现问题：使用`RedirectAttributes`

```java
@RequestMapping("/view03")
    public String view03(RedirectAttributes redirectAttributes){
        redirectAttributes.addAttribute("uname","张三");
        redirectAttributes.addAttribute("upwd","123454");
        return "redirect:view.jsp";
    }
```

```java
@RequestMapping("view04")
    public ModelAndView view04(ModelAndView mv){//不想写ModelAndView mv = new ModelAndView(),可以直接传入形参
        mv.addObject("uname","张三");
        mv.addObject("upwd","123445");
        mv.setViewName("redirect:view.jsp");//注意视图的ViewName
        return mv;
    }
```

重定向也可用从一个Controller传给另一个Controller

```java
@RequestMapping("view05")
    public ModelAndView view05(ModelAndView mv){//不想写ModelAndView mv = new ModelAndView(),可以直接传入形参
        mv.addObject("uname","张三");
        mv.addObject("upwd","123445");
        mv.setViewName("redirect:test");//要有控制器的方法的RequestMapping 为 test，就能传递
        return mv;
    }
```

注意：使用Model对象不能重定向，Model只在当前请求域中有效，而重定向包含两次请求

#### 请求转发

请求转发以 `forward` 开头

```java
@RequestMapping("view05")
public ModelAndView view05(ModelAndView mv){
    mv.addObject("uname","张三");
    mv.addObject("upwd","123445");
    mv.setViewName("forward:view.jsp");
    return mv;
}
```

```java
@RequestMapping("view06")
public String view06(){
    return "forward:view.jsp?uname=张三";//请求转发在url出现中文跳转不会乱码，因为没有经过浏览器
}
```

### JSON开发

**基本概念**

​		Json在企业开发中已经作为通用的接口参数类型，在页面(客户端)解析很方便。SpringMVC 对于json提供了良好的支持，这里需要修改相关配置，添加json数据支持功能

#### @ResponseBody

​		该注解用于将Controller的方法返回的对象，通过适当的`HttpMessageConverter`转换为指定格式后,写入到Response对象的body数据区。
​		返回的数据不是html标签的页面,而是其他某种格式的数据时(如json. xml 等)使用(通常用于ajax 请求)

#### @RequestBody

​		该注解用于读取Request请求的body部分数据，使用系统默认配置的`HttpMessageConverter`进行解析，然后把相应的数据绑定到要返回的对象上，再把`HttpMessageConverter`返回的对象数据绑定到controller中方法的参数上。

#### 依赖

```xml
<!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.13.2.2</version>
</dependency>
<!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-core -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-core</artifactId>
    <version>2.13.2</version>
</dependency>
<!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-annotations -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-annotations</artifactId>
    <version>2.13.2</version>
</dependency>

```

#### 修改servlet-context.xml

```xml
<!--添加用于数据转换的两个bean对象-->
<mvc:annotation-driven>
	<mvc:message-converters>
    	<bean class="org.springframework.http.converter.StringHttpMessageConverter"/>
        <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter"/>
    </mvc:message-converters>
</mvc:annotation-driven>
```

```java
//直接使用,使之返回的的bean能被浏览器解析（已是Json格式）//原本没有网页的情况下就会404，现在可以将bean对象直接打印
@ResponseBody
```

#### @RequestBody

​		`@RequestBody`注解常用来处理`content-type`不是默认的`application/x-www-form-urlcoded`类型的内容，比如说: `application/json` 或者是`application/xml`等。一般情况下来说常用其来处理`application/json`类型。`@RequestBody`接受的是一个 json格式的字符串，一定是一个字符串。
​		通过`@RequestBody`可以将请求体中的JSON字符串绑定到相应的bean上，当然，也可以将其分别绑定到对应的字符串上。

### 拦截器

​		SpringMVC中的`Interceptor`拦截器也是相当重要和相当有用的，它的主要作用是拦截用户的请求并进行相应的处理。比如通过它来进行权限验证，或者是来判断用户是否登陆等操作。对于SpringMVC拦截器的定义方式有两种：

​		实现接口： `org.springframework.web.servlrt.HandlerInterceptor`

​		继承适配器：`org.springframework.web.servlet.handler.HandlerInterceptorAdapter`

#### 拦截器实现

HandlerIntercepter接口

先定义拦截器的实现类，重写方法

```java
public class MyInterceptor01 implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("目标handler执行前执行拦截器--> preHandle");
        return true;
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("目标方法执行后，视图生成之前执行拦截器-->postHandle");
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("视图生成之后执行拦截器-->afterCompletion");
    }
}
```

然后在配置文件：添加拦截器配置

```xml
<!--拦截器配置-->
    <mvc:interceptors>
        <!--直接定义在标签中，拦截器会拦截所有请求-->
        <bean class="com.xxxx.springmvc.interceptor.MyInterceptor01"/>
    </mvc:interceptors>
```

运行：

```
目标handler执行前执行拦截器--> preHandle
拦截的方法
目标方法执行后，视图生成之前执行拦截器-->postHandle
视图生成之后执行拦截器-->afterCompletion
```

拦截器配置方式二：

```xml
<mvc:interceptors>
        <!--直接定义在标签中，拦截器会拦截所有请求-->
        <!--<bean class="com.xxxx.springmvc.interceptor.MyInterceptor01"/>-->
        <mvc:interceptor>
            <!--通过 mvc:mapping 配置需要被拦截的资源，支持通配符，可配置多个-->
            <!--“/**” 表示拦截项目下所有-->
            <mvc:mapping path="/**"/>
            <!--可通行的资源：-->
            <mvc:exclude-mapping path="/test/*"/><!--注意：这里是url，用的是RequestMapping下的路径-->
            <bean class="com.xxxx.springmvc.interceptor.MyInterceptor01"/>
        </mvc:interceptor>
    </mvc:interceptors>
```

如果有多个拦截器，则根据配置的顺序执行

#### 用户控制器

使用拦截器完成用户是否登入请求验证功能

```java
/**
 * 用户模块：
 *      用户登入
 *      用户添加、更新、删除（需要拦截）
 */@Controller
@RequestMapping("/userInfo")
public class UserInfoController {
    @RequestMapping("/login")
    public ModelAndView userLogin(HttpSession httpSession){
        System.out.println("用户登入...");
        ModelAndView mv = new ModelAndView();
        mv.setViewName("success");
        User user = new User();
        user.setUserName("admin");
        user.setId(1);
        user.setUserPwd("123456");
        //通过session对象
        httpSession.setAttribute("user",user);
        return mv;
    }
    @RequestMapping("/add")
    public ModelAndView userAdd(){
        System.out.println("用户添加...");
        ModelAndView mv = new ModelAndView();
        mv.setViewName("success");
        return mv;
    }
    @RequestMapping("/update")
    public ModelAndView userUpdate(){
        System.out.println("用户更新...");
        ModelAndView mv = new ModelAndView();
        mv.setViewName("success");
        return mv;
    }
    @RequestMapping("/delete")
    public ModelAndView userDelete(){
        System.out.println("用户删除...");
        ModelAndView mv = new ModelAndView();
        mv.setViewName("success");
        return mv;
    }
}
```

```java
public class LoginInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        //通过session来判断用户是否登入
        User user = (User) request.getSession().getAttribute("user");
        if(user==null){
            //拦截请求并返回到登入页面
            response.sendRedirect(request.getContextPath()+"login.jsp");
            return false;
        }
        return true;
    }
}
```

```xml
<mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <mvc:exclude-mapping path="/userInfo/login"/>
            <bean class="com.xxxx.springmvc.interceptor.LoginInterceptor"/>
        </mvc:interceptor>
    </mvc:interceptors>
```

### 文件上传

依赖

```xml
<!-- https://mvnrepository.com/artifact/commons-fileupload/commons-fileupload -->
<dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.3.3</version>
</dependency>
```

依赖中的 MultipartRequest 接口

```java
Iterator<String> getFileNames();
MultipartFile getFiles(String val1);
List<MultipartFile> getFiles(String val1);//用于多文件上传
```

servlet-context.xml修改

```xml
<!--文件上传的配置-->
    <bean id="multipartResolver"
          class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
        <property name="maxUploadSize">
            <value>104857600</value><!--允许文件上传的最大尺寸-->
        </property>
        <property name="maxInMemorySize">
            <value>4096</value><!--大于值生成硬盘临时文件，小于时保存在内存中-->
        </property>
    </bean>
```

前台

```jsp
<body>
    <form method="post" action="uploadFile" enctype="multipart/form-data">
        <input type="file" name="file"/>
        <button>上传</button>
    </form>
</body>
```

获取项目目录

```java
String path = request.getServletContext().getRealPath("/");//    "/"表示根目录:webapp下
```

文件存放目录

```java
File uploadFile = new File(path +"/upload");
if(!uploadFile.exists()){
    uploadFile.mkdir();
}
```

获取上传文件的文件名：生成随机的名字，避免重复

```java
String originlName = file.getOriginalFileName();//file 是jsp表单传的文件对象
String suffix = originalName.substring(originalName.lastIndexOf("."));
    //通过系统当前毫秒数生成随机名
String fileName = System.currentTimeMillis()+suffix;
```

上传文件

```java
file.tranferTo(new File(path, fileName));
```

多文件上传——————修改

页面表单：准备多各文件域

```jsp
<body>
    <form method="post" action="uploadFile" enctype="multipart/form-data">
        <input type="file" name="file"/>
        <input type="file" name="file"/>
        <input type="file" name="file"/>
        <button>上传</button>
    </form>
</body>
```

```java
//大方法名
public String uploadFile(HttpServletRequest request,@RequestParam("files") List<MultipartFile> files){
    if(files!=null&&files.size()>0){
        for(MultipartFile file : files){
            //封装上面的方法
        }
    }
}
```

## SSM框架集成

### 配置pom

需要的依赖：

- junit
- spring-context
- spring-test
- spring-jdbc
- spring-tx
- aspectjweaver
- c3p0
- mybatis
- mybatis-spring
- mysql-connector-java
- slf4j-log4j       日志
- slf4j-api     日志
- pagehelper   分页插件
- spring-web
- spring-webmvc
- javax.servlet-api
- jackson-core<版本>
- jackson-databind<版本>
- jackson-annotations<版本>
- commons-fileupload

```

```

### 设置资源目录和插件

```xml
<!-- Maven项目：如果源代码(src/main/java) 存在xml，properties，tld文件
	Maven默认不会自动编译该文件到输出目录，因此要编译这些文件，需要
	显式配置 resources标签-->
<build>
<finalName>ssm01</finalName>
    <resources>
    	<resource>
        	<directory>src/main/java</directory>
            <includes>
            <include>**/*.xml</include>
            <include>**/*.properties</include>
            <include>**/*.tld</include>
            </includes>
            <filtering>false</filtering>
        </resource>
    </resources>
</build>

<!--插件-->
<plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>2.3.2</version>
        <configuration>
          <source>1.8</source>
          <target>1.8</target>
          <encoding>UTF-8</encoding>
        </configuration>
      </plugin>
      <plugin>
        <groupId>org.eclipse.jetty</groupId>
        <artifactId>jetty-maven-plugin</artifactId>
        <version>9.4.27.v20200227</version>
        <configuration>
          <scanIntervalSeconds>10</scanIntervalSeconds>
          <httpConnector>
            <port>8080</port>
          </httpConnector>
          <webAppConfig>
            <contextPath>/ssm01</contextPath><!--项目路径-->
          </webAppConfig>
        </configuration>
      </plugin>
    </plugins>
```

### 配置web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app id="WebApp-ID" version="3.0"
         xmlns="http://java.sun.com/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
         http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd">
  <!--启动Spring容器-->
    <context-param>
    	<param-name>contextConfigLocation</param-name>
        <param-value>classpath:sprimh.xml</param-value>
    </context-param>
    <!--设置监听器-->
    <listener>
    	<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
<!--编码过滤-->
    <filter>
    <description>char encoding filter</description>
    <filter-name>encodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
      <param-name>encoding</param-name>
      <param-value>UTF-8</param-value>
    </init-param>
  </filter>
  <filter-mapping>
    <filter-name>encodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>

  <!--Servlet请求分发器-->
  <servlet>
    <servlet-name>springMvc</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:servlet-context.xml</param-value><!--需要在resource目录下的servlet-context.xml文件：springMVC的-->
    </init-param>
    <!--表示启动容器时初始化Servlet-->
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>springMvc</servlet-name>
    <!--这是拦截请求，"/"代表拦截所有请求，"*.do"表示拦截所有.do请求-->
    <url-pattern>*.do</url-pattern>
  </servlet-mapping>
</web-app>

```

### 配置spring.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop.xsd
        http://www.springframework.org/schema/tx
        http://www.springframework.org/schema/tx/spring-tx.xsd">
    <context:component-scan base-package="com.xxxx.ssm">
    <!--context:exclude-filter标签：排除对某个注解的扫描，（过滤controller层）-->
    <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/><!--因为在springmvc中也扫描了controller层，因此排除-->
    </context:component-scan>
<!--配置Aop自动代理-->
    <aop:aspectj-autoproxy/>
    <context:property-placeholder location="classpath:db.properties"/>
    <!--配置c3p0数据源-->
    <bean id='dataSource' class="com.mchange.v2.c3p0.ComboPooledDataSource">
    	<property name="driver" value="${jdbc.driver}"/>  
		<property name="jdbcUrl" value="${jdbc.url}"/>  
		<property name="username" value="${jdbc.username}"/>  
		<property name="password" value="${jdbc.password}"/>  
    </bean>
    <!--配置事务管理器-->
    <bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    	<property name="datasource" ref="dataSource"></property>
    </bean>
    <!--设置事务增强-->
    <tx:advice id="txAdvice" transaction-manager="txManager">
    	<tx:attributes>
        	<tx:method name="add*" propagation="REQUIRED"/>
            <tx:method name="insert*" propagation="REQUIRED"/>
            <tx:method name="update*" propagation="REQUIRED"/>
            <tx:method name="delete*" propagation="REQUIRED"/>
        </tx:attributes>
    </tx:advice>
    <!--aop切面配置-->
    <aop:config>
    	<aop:pointcut id="ServicePointcut" expression="execution(* com.xxxx.ssm.service..*.*(..))"/>
        <aop:advisor advice-ref="txAdvice" pointcut-ref="servicePointcut"/>
    </aop:config>
    <!--配置SqlsesionFactory-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlsessionFactoryBean">
    	<property name="dataSource" ref="dataSource"></property>
        <property name="configLocation" value="classpath:mybatis.xml"/>
        <property name="mapperLocations" value="classpath:com/xxxx/ssm/mapper/*.xml"/>
    </bean>
        <!--配置扫描器-->
    <bean id="mapperScanner" class="org.mybatis.spring.mapper.MapperScannerConfigurer">
    	<property name="basePackage" value="com.xxxx.ssm.dao"/>
        <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
    </bean>

</beans>
```

### 配置servlet-context.xml

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/mvc
                           http://www.springframework.org/schema/mvc/spring-mvc.xsd
                           http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context
                           http://www.springframework.org/schema/context/spring-context.xsd">
    <!--开启扫描器-->
    <context:component-scan base-package="com.xxxx.ssm.controller"/>
    <!--使用默认的servlet响应文件-->
    <mvc:default-servlet-handler/>
    <!--开启注解驱动-->
    <mvc:annotation-driven>
    	<mvc:message-converters>
        	<bean class="org.springframework.http.converter.StringHttpMessageConverter"/>
            <bean class="org.springframework.http.converter.json.MappingJacksonMessageConverter"/>
        </mvc:message-converters>
    </mvc:annotation-driven>
    <!--配置视图解析器-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"
          id="internalResourceViewResolver">
        <!--前缀：在WEB-INF目录下的jsp目录下-->
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <!--后缀：以.jsp结尾的资源-->
        <property name="suffix" value=".jsp"/>
    </bean>

    <!--拦截器配置-->
   <!-- <mvc:interceptors>
        &lt;!&ndash;直接定义在标签中，拦截器会拦截所有请求&ndash;&gt;
        &lt;!&ndash;<bean class="com.xxxx.springmvc.interceptor.MyInterceptor01"/>&ndash;&gt;
        <mvc:interceptor>
            &lt;!&ndash;通过 mvc:mapping 配置需要被拦截的资源，支持通配符，可配置多个&ndash;&gt;
            &lt;!&ndash;“/**” 表示拦截项目下所有&ndash;&gt;
            <mvc:mapping path="/**"/>
            &lt;!&ndash;可通行的资源：&ndash;&gt;
            <mvc:exclude-mapping path="/test/*"/>&lt;!&ndash;注意：这里是url，用的是RequestMapping下的路径&ndash;&gt;
            <bean class="com.xxxx.springmvc.interceptor.MyInterceptor01"/>
        </mvc:interceptor>
    </mvc:interceptors>-->
    
    <!--文件上传的配置-->
    <bean id="multipartResolver"
          class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
        <property name="maxUploadSize">
            <value>104857600</value><!--允许文件上传的最大尺寸-->
        </property>
        <property name="maxInMemorySize">
            <value>4096</value><!--大于值生成硬盘临时文件，小于时保存在内存中-->
        </property>
    </bean>
</beans>
```

### 配置mybatis.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
		PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
		"http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
	<typeAliases>
    	<package name="com.xxxx.ssm.po"/>
    </typeAliases>
    <plugins>
    	<plugin interceptor="com.github.pagehelper.PageIntercepter"></plugin>
    </plugins>
</configuration>
```

### 配置dp.properties

```properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/MyBatis?useSSL=false
jdbc.username=root
jdbc.password=root
```

### 配置log4j.properties

```properties
log4j.rootLogger=DEBUG, Console
#Console
log4j.appender.Console=org.apache.log4j.ConsoleAppender
log4j.appender.Console=layout=org.apache.log4j.PatternLaylot
log4j.appender.Console.layout.ConbersionPattern=%d [%t] %-5p [%c] - %m%n
log4j.logger.java.sql.ResultSet=INFO
log4j.logger.org.apache=INFO
log4j.logger.java.sqsl.Connection=DEBUG
log4j.logger.java.sql.Statement=DEBUG
log4j.logger.java.sql.PreparedStatement=DEBUG
```

