##                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    HTML

```html
<!--列表-->
<ul>
    <li>无序列表
    <li>
</ul>
<ol>
    <li>有序列表
    <li>
</ol>
```

```html
<!--表格-->
<table>
    <caption></caption>
    <tr>表格行标记
        <td>单元格标记</td>
        <td></td>
        <td></td>
    </tr>
</table>
```



```html
<!--表单-->
<form acation="" method="post" name="myform">
    用户名:<input name="username" type="text" id="UserName4" maxlength="20">
    密码:<input name="pwd1" type="password" id="PWD14" size="20" maxlength="20">
    确认密码:<input name="pwd2" type="password" id="PWD25" size="20" maxlength="20">
    性别:<input name="sex" type="radio" class="noboder" value="男"checked>
    	男&nbsp;
    	<input name="sex" type="radio" class="noboder" value="女"checked>
    	女
    爱好:<input name="like" type="checkbox" id="like" value="体育">
    	体育
    	<input name="like" type="checkbox" id="like" value="看书">
    	看书
    	<input name="like" type="checkbox" id="like" value="旅游">
    	旅游
    E-mail:<input name="email" type="text" id="PWD224" size="50">
    <input name="submit" type="submit" class="btn_grey" value="确认保存">
</form>
```

### CSS语法格式

**选择器**

- 标记选择器
- 类选择器
- id选择器

```css
选择符{属性:属性值;}
标记选择器：
<style>
h2{
    font-family:宋体;
    color:red;
}
a{
    font-size:9px;
    color:#F93;
}
</style>
```

但是如果一个页面有多个h2标记，想让它们每个不一样，就不能使用上面的**标记选择器**了，而引用**类选择器**。

类选择器的名称由用户自己定义，以"."开头

```html
<style>
.one{
    font-family:宋体;
	color:red;
}
.two{
     font-family:宋体;
    font-size:24px;
}
</style>
</head>
<body>
    <h2 class="one">
        应用了选择器one
    </h2>
    <h2 class="two">
        应用了选择器two
    </h2>
</body>

```

**id选择器**：命名以"#"开始，html页面不能包含两个相同id，因此定义的id选择器只能使用一次

```html
<style>
#first{
    font-family:宋体;
	color:red;
}
#second{
     font-family:宋体;
    font-size:24px;
}
</style>
</head>
<body>
   <p id="first">
       第一个选择器
    </p>
    <p id="second">
        第二个选择器
    </p>
</body>
```

以上例子是内嵌式，在页面中包含<css></css>，最常用的是链接式，CSS单独在一个文件中，在html中使用<link>标记引用

```html
<link rel="stylesheet" href="path" type="text/css">
```

这样创建一个css.css文件

```css
h1,h2,h3{
    color:#6CFw;
    font-family:"Trebuchet MS",Arial 
}
p{
    color:#F0Cs;
    font-weight:200;
    font-size:24px;
}
```

然后

```html
<title></title>
<link herf="css.css"/>
<body>
    <h2>
        标题二
    </h2>
    <p>
        页面文章
    </p>
</body>
```

## JavaScript

JavaScript是一种**基于对象和事件驱动**并具有*安全性能*的<u>解释型</u>脚本语言，且不需要编译，直接嵌入在html运行

```html
<form name="form1" method="post" action="">
    请输入真实姓名：<input name="realName" type="text" id="realName" size="40">
    <br>
    <input name="Botton" type='botton' class="btn_grey" onclick="checkRealName()" value="检测">
</form>
```

辨析自定义js函数checkRealName()，用于检测验证输入姓名是否正确，是否是两个或以上汉字

```html
<script language="javascript">
	function checkRealName(){
    val str = form1.realName.value;
    if(str==""){
        alert("请输入真实姓名！");
        form1.realName.focus();return;
    }else{
        val objExp = /[\u4E00-\u9FA5]{2,}/;   //
        if(objExp.text(str)==true){
            alert("您输入的真实姓名不正确");
        }else{
            alert("您输入的真实姓名不正确");
        }
    }
}
</script>
```

### 事件处理程序调用

在Js中调用事件处理程序，首先需要获得处理对象的引用，然后将要执行的处理函数赋值给对应的事件

```html
<input name="bt_save" type='botton' value="保存">
<script language="javascript">
	var b_save=document.getElmentById("bt_save");
    b_save.onclick=function(){
        alert("单击了保存按钮");
    }
</script>
```

在html中，只需要在标记中添加相应的事件

```html
<input name="by_save" type="button" value="保存" onclick="alert("单击了保存按钮");"
```

### 常用对象

# Servlet

### Servlet工作流程

在配置了tomcat的web项目下定义一个普通类，用于实现Servlet

```java
package com.demo.servlet;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * 实现servlet
 * 1.创建普通类
 * 2.继承HttpServlet类
 * 3.重写service方法，用看来处理请求，快捷键ctrl+o
 * 4.写完了但是浏览器不怎么访问哪个类，设置注解，指定访问路径，如下在类前写@Webservlet("/ser01")
 */
@WebServlet("/ser01")//打开浏览器，该资源在ser01路径即可得到，注意斜杠必须要有
public class Servlet01 extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //super.service(req, resp);
        //打印内容到控制台
        System.out.println("Hello servlet!");
        //通过流输出数据到浏览器
        resp.getWriter().write("Hello there");
    }
    //service方法是doGet和doPost方法的整合，用来应对浏览器的get或者post请求
}
```

运行该项目，在浏览器可获得输出Hello there，其路径是`Localhost:8080/demo/ser01`，其中/demo在配置tomcat中，Deployment中的Application context修改，/ser01通过该类的注解指定了访问路径。

浏览器如何获得服务器的资源？

1. 浏览器通过http发送Get 请求，根据请求头找到主机，根据请求行获取当前访问的应用和资源路径`/demo/ser01`
2. 服务器创建对应的Servlet（第二次以后就直接调用了），调用service方法，并生成req和resp对象
3. 通过req来获取传递的参数，通过resp来回应，

### Servlet生命周期

Servlet没有main()方法，不能独立运行，它的运行完全由Servlet 引擎来控制和调度。所谓生命周期， 指的是servlet容器何时创建servlet实例、何时调用其方法进行请求的处理、何时并销毁其实例的整个过程。

●实例和初始化时机
当请求到达容器时，容器查找该servlet对象是否存在，如果不存在，则会创建实例并进行初始化。

●就绪/调用/服务阶段
有请求到达容器，容器调用servlet对象的service()方法处理请求的方法在整个生命周期中可以被多次调用;HttpServlet的service()方法，会依据请求方式来调用doGet()或者doPost()方法。但是，这两个do方法默认情况下，会抛出异常,需要子类去override.

●销毁时机
当容器关闭时(应用程序停止时)，会将程序中的Servlet实例进行销毁。

上述的生命周期可以通过Servlet中的生命周期方法来观察。在Servlet中有三个生命周期方法,不由用户手
动调用，而是在特定的时机有容器自动调用，观察这三个生命周期方法即可观察到Servlet的生命周期。

```
1. Web Client向Servlet容器(Tomcat) 发出Http请求
2. Servlet容器接收Web Client的请求
3. Servlet容器创建一个HttpServletRequest对象，将Web Client 请求的信息封装到这个对象中
4. Servlet容器创建一个HttpServletResponse对象
5. Servlet容器调HttpServlet对象service方法，把Request与Response作为参数，传给HttpServlet
6. HttpServlet调用HttpServletRequest对象的有关方法，获取Http请求信息
7. HttpServlet 调用HttpServletResponse对象的有关方法，生成响应数据
8. Servlet容器把HttpServlet的响应结果传给Web Client
```

### HttpServletRequest对象

`HttpServletRequest`对象：主要作用是用来接收客户端发送过来的请求信息，例如：请求的参数，发送的头信息等都属于客户端发来的信息，`service()`方法中形参接收的是`HttpServletRequest`接口的实例化对象，表示该对象主要应用在HTTP协议上，该对象是由Tomcat封装好传递过来。

`HttpServletRequest`是ServletRequest的子接口，ServletRequest 只有一个子接口，就是HttpServletRequest。既然只有一个子接口为什么不将两个接口合并为一个?

从长远上讲：现在主要用的协议是HTTP协议，但以后可能出现更多新的协议。若以后想要支持这种新协议，只需要直接继承ServletRequest接口就行了。

在HttpServletRequest接口中，定义的方法很多，但都是围绕接收客户端参数的。但是怎么拿到该对象呢?不需要，直接在Service方法中由(tomcat)容器传入过来，而我们需要做的就是取出对象中的数据，进行分析、处理。

#### 常用方法

| 方法名               | 介绍                                                         |
| -------------------- | ------------------------------------------------------------ |
| getRequestURL()      | 获取客户端发送请求完整URL（从http开始，到？前结束）          |
| getRequestURI()      | 获取请求行中资源名称部分（从站点名开始，到？前结束）         |
| getQueryString()     | 获取请求行的参数部分                                         |
| getMethod()          | 获取客户端请求方式                                           |
| getProtocol()        | 获取HTTP版本号                                               |
| getContextPath()     | 获取webapp名字                                               |
| **getParameter()**   | 获取指定名称的参数值（**重要**）（不管什么类型都返回字符串） |
| getParameterValues() | 获取指定名称的所有参数值（返回字符串数组）                   |

```java
// getRequestURL 返回的是StringBuffer类型，如果直接用String节会报错
String url = req.getRequestURL();//报错
//可以直接在后面家空字符串
String url = req.getRequestURL()+"";//就行
```

#### 请求乱码问题

​        由于现在的request属于接收客户端的参数，所以必然有其默认的语言编码，主要是由于在解析过程中默认使用的编码方式为IS0-8859-1(此编码不支持中文)，所以解析时一定会出现乱码。要想解决这种乱码问题，需要设置request中的编码方式，告诉服务器以何种方式来解析数据。或者在接收到乱码数据以后，再通过相应的编码格式还原。

> Tomcat8.0以上版本的GET请求不会乱码，POST请求会

方式一：

```java
req.setCharacterEncoding("UTF-8");//要在获取之前设置,且只针对post请求
```

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>    <!--login.jsp文件，采用表单提交，请求POST-->
<html>
<head>
    <title>登入</title>
</head>
<body>
    <form method="post" action="ser01">
        姓名：<input type="text" name="uname"> <br>
        密码：<input type="password" name="upwd"><br>
        <button>登入</button>
    </form>
</body>
</html>
```

方式二：（不常用了）

```java
//针对Tomcat7及以下的get乱码
String uname= new String(req.getParameter("uname").getBytes("ISO-8859-1"),"UTF-8")
```

#### <span id="qqzf">请求转发*</span>

​		请求转发，是一种**服务器的行为**，当客户端请求到达后，服务器进行转发，此时会将请求对象进行保存，地址栏中的**URL地址不会改变**，得到响应后，服务器端再将响应发送给客户端，**从始至终只有一个请求发出**。

实现方式如下，达到多个资源协同响应的效果。

```java
req.getRequestDispatcher(url).forward(req,resp);
//相当用户请求了一个资源，但服务器可同时将参数传给多个资源，比如这里从servlet传给jsp，而用户地址栏不变
req.getRequestDispatcher(login.jsp).forward(req,resp);
```

#### request作用域

通过该对象可以在一个请求中传递数据，作用范围：在一次请求中有效，即服务器跳转有效

```java
//设置域对象内容
req.setAttribute(String name, Object o);
//获取域对象内容
req.getAttribute(String name);
//删除域对象内容
req.removeAttribute(String name);
```

一般后台跳转后台不常见，而是前台获取后台数据使用多点

> 注：在jsp文件中写java代码需要代码块如下：

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
    <title>$Title$</title>
  </head>
  <body>
      <h2>index页面</h2>
  <%
    String name = (String) request.getAttribute("name");
    System.out.println("name:"+ name);
    Integer age = (Integer) request.getAttribute("age");
    System.out.println("age:" +age);
  %>
  </body>
</html>

```

```java
@WebServlet("/ser02")
public class Servlet02 extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("Servlet 02...");
        req.setAttribute("name","admin");
        req.setAttribute("age",29);
        //请求转发到jsp，jsp是动态页面，可以拿到后台数据
        req.getRequestDispatcher("index.jsp").forward(req,resp);
    }
}
```

```
onnected to server
[2022-05-01 09:37:34,038] Artifact WebDemo:war exploded: Artifact is being deployed, please wait…
[2022-05-01 09:37:34,310] Artifact WebDemo:war exploded: Artifact is deployed successfully
[2022-05-01 09:37:34,310] Artifact WebDemo:war exploded: Deploy took 273 milliseconds
name:null
name:null
//这里是访问了ser02后
Servlet 02...
name:admin
```

### HttpServletResponse对象

Web服务器收到客户端的http请求，会针对每一次请求， 分别创建一个用于代表请求的 request对象和代表响应的response对象。

request和response对象代表请求和响应:获取客户端数据，需要通过request对象；向客户端输出数据，需要通过response对象。

HttpServletResponse的主要功能用于服务器对客户端的请求进行响应，将Web服务器处理后的结果返回给客户端。service()方法中形参接收的是HttpServletResponse接口的实例化对象，这个对象中封装了向客户端发送数据、发送响应头，发送响应状态码的方法。

#### 响应数据

响应时需要获取输出流，有两种形式：（**两者不能同时使用**）：因为resp对象只能响应一次

​		**getWriter()**		：获取字节流（只能响应回字符）

​		**getOutputStream()**    ：获取字节流（能响应一切数据）

```java
//获取字节流
        PrintWriter writer = resp.getWriter();
        writer.write("Hello");
```

```java
		ServletOutputStream out = resp.getOutputStream();
        out.write("Hi".getBytes(StandardCharsets.UTF_8));//注意需要getByte
```

#### 响应乱码问题

当服务器端和客户端编码格式不同就可能出现乱码问题

只需要在服务器端告知服务器支持中文的编码格式：

```java
resp.setCharacterEncoding("UTF-8");
```

同时还要只当客户端的解码方式：

```java
resp.setHeader("content-type","text、html;character=UTF-8");
```

```java
	    resp.setCharacterEncoding("UTF-8");
        resp.setHeader("content-type","text/html;character=UTF-8");
        PrintWriter writer = resp.getWriter();
        writer.write("<h2>你好</h2>");
```

#### 重定向

​       重定向是一种**服务器指导，客户端的行为**。客户端发出第一个请求， 被服务器接收处理后，服务器会进行响应，在响应的同时，服务器会给客户端一个新的地址(下次请求的地址`response.sendRedirect(url);`) ，当客户端接收到响应后，会立刻、马上、自动根据服务器给的新地址发起**第二个请求**，服务器接收请求并作出响应，重定向完成。

**地址栏会改变**

```java
resp.sendRedirect("s05");//重定向到Servlet05
```

重定向是有两次请求，两次resp，因此参数不会传递，和[请求转发](#qqzf)不同

请求转发和重定向的区别

| 请求转发  req.getResquestDispatcher().forward()  | 重定向  resp.sendRedirct()                            |
| ------------------------------------------------ | ----------------------------------------------------- |
| 一次请求，数据在request域中共享                  | 两次请求，request域中数据不共享                       |
| 服务器端行为                                     | 客户端行为                                            |
| 地址栏不会变化                                   | 地址栏发生变化                                        |
| 绝对地址定位到站点后（**只能找当前站点的资源**） | 绝对地址可写到http://（**可以跳转到互联网任意地址**） |

### Cookie对象

#### Cookie的创建和发送

```java
Cookie cookie = new Cookie("uname","zhangshan");
//发送
resp.addCookie(cookie);
```

#### Cookie的获取

返回的是Cookie数组

```java
Cookie[] cookies = req.getCookies();
//遍历前需要做非空和长度判断
```

#### Cookie设置到期时间

`setMaxAge(int time);`

**取值**

> - 负整数：默认值为-1.表示只在浏览器内存中存活，关闭窗口即消失
> - 正整数：指定秒数，存在硬盘上
> - 0：表示该Cookie作废，如果原来浏览器已保存，则通过此删除客户端不管是内存还是硬盘上的Cookie

```java
Cookie cookie = new Cookie("uname","zhangshan");
//设置三天后失效
cookie.setMaxAge(-1);
```

#### Cookie注意点

1. Cookie保存在当前浏览器中

2. 中文
   需要通过`URLEncoder.encode()`来编码，再通过`URLDecoder.decoder()`来解码(过期方法)

   ```java
   String name = "张三";
   String value = "历时";
   name = URLEncoder.encode(name);
   value = URLEncoder.encode(value);
   Cookie cookie = new Cookie(name,value);
   resp.addCookie(cookie);
   ```

   ```
   URLDecoder.decode(cookie.getName());
   URLDecoder.decode(cookie.getValue());
   ```

3. 同名Cookie
   发送重复的会覆盖原有Cookie

4. 浏览器存放Cookie的数量
   不同浏览器对Cookie的大小和数量有限制

#### Cookie路径

Cookie 的setPath设置Cookie路径

情景一：当前服务器下任何项目资源都可获得Cookie对象

```java
/*当前为:s01*/
Cookie cookie = new Cookie("XXX","xxx");
//表示当前服务器下所有项目都能访问
cookie.setPath("/");
resp.addCookie(cookie);
```

情景二：当前项目下的资源可获取Cookie对象（默认不设置Cookie的path）

```java
/*当前为:s01*/
Cookie cookie = new Cookie("XXX","xxx");
//
cookie.setPath("/s01");//默认情况
resp.addCookie(cookie);
```

情景三：指定项目下的资源才可获取

```java
/*当前为:s01*/
Cookie cookie = new Cookie("XXX","xxx");
//设置路径为"/s02"
cookie.setPath("/s02");//就算cookie是s01产生的，s01也不能获取
resp.addCookie(cookie);
```

情景四：指定目录下的资源可获取

```java
/*当前为:s01*/
Cookie cookie = new Cookie("XXX","xxx");
//设置路径为"/s02"
cookie.setPath("/s02/cook");//仅s02下的cook才能拿到
resp.addCookie(cookie);
```

### HttpSession对象

​		HttpSession对象是`javax.servlet.http.HttpSession` 的实例，该接口并不像`HttpServletRequest`或`HttpServletResponse`还存在一个父接口， 该接口只是一个纯粹的接口。这因为session本身就属于HTTP协议的范畴。
​		对于服务器而言，每一个连接到它的客户端都是一个session, servlet 容器使用此接口创建HTTP客户端和HTTP服务器之间的会话。会话将保留指定的时间段，跨多个连接或来自用户的页面请求。一个会话通常对应于一个用户，该用户可能多次访问一个站点。可以通过此接口查看和操作有关某个会话的信息，比如会话标识符、创建时间和最后一次访问时间。 在整个session中，最重要的就是属性的操作。

​		session无论客户端还是服务器端都可以感知到，若重新打开一个新的浏览器，则无法取得之前设置的session,因为每一个session只保存在当前的浏览器当中，并在相关的页面取得。
​		Session的作用就是为了标识一次会话，或者说确认一个用户；并且在一次会话(一个用户的多次请求)期间共享数据。我们可以通过`request.getSession()`方法，来获取当前会话的session对象。

```java
//如果存在，则获
//所有获取和req对象有关
HttpSession session = req.getSession();//如果存在，则获取；如果不存在，则创建
//获取Session会话标识符
String id = session.getId();
//获取Session的创建时间
session.getCreationTime();
//获取最后一次访问时间
session.getLastAccessedTime();
//判断是否是新的session对象
session.isNew();
```

```
Connected to server
[2022-05-03 03:05:48,141] Artifact Cookies:war exploded: Artifact is being deployed, please wait…
[2022-05-03 03:05:48,544] Artifact Cookies:war exploded: Artifact is deployed successfully
[2022-05-03 03:05:48,544] Artifact Cookies:war exploded: Deploy took 404 milliseconds
8A4898019275E7A2B96D710BB32105D4
1651561550273
1651561550274
false
```

#### 标识符JSESSIONID

​		Session既然是为了标识一次会话，那么此次会话就应该有一个唯一的标志， 这个标志就是sessionld。

​		每当一次请求到达服务器，如果开启了会话(访问了session)，服务器第一步会查看是否从客户端回传一个名为`JSESSIONID`的cookie，如果没有则认为这是一次新的会话， 会创建一个新的session对象，并用唯一的sessionld为此次会话做一个标志。如果有`JESSIONID`这个cookie回传，服务器则会根据`JSESSIONID`这个值去查看是否含有id为`JSESSION`值的session对象，如果没有则认为是一个新的会话， 重新创建一个新的 session对象，并标志此次会话;如果找到了相应的session对象，则认为是之前标志过的一次会话，返回该session对象，数据达到共享。

​		这里提到一个叫做`JSESSIONID`的cookie，这是一个比较特殊的cookie，当用户请求服务器时，如果访问了session，则服务器会创建一个名为`JSESSIONID`，值为获取到的session (无论是获取到的还是新创建的)的`sessionld`的cookie对象，并添加到response对象中，响应给客户端，有效时间为关闭浏览器。
​		**所以Session的底层依赖Cookie来实现**。

#### Session域对象

Session用来表示一次会话，在一次会话中数据是可以共享的，这时session作为域对象存在，可以通过`setAttribute(name,value)`方法向域对象中添加数据，通过`getAttribute(name)`从域对象中获取数据，通过`removeAttribute(name)`从域对象中移除数据。

```java
@WebServlet("/ss02")
public class Session02 extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //session域对象 和 request域对象 比较
        HttpSession session = req.getSession();
        session.setAttribute("uname","admin");
        session.setAttribute("upwd","123456");

        session.removeAttribute("upwd");

        req.setAttribute("name","zhangshan");

        //请求转发
        req.getRequestDispatcher("index.jsp").forward(req,resp);
    }
}
```

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
    <title>获取域对象</title>
  </head>
  <body>
    <%
      String uname = (String) request.getSession().getAttribute("uname");
      String upwd = (String) request.getSession().getAttribute("upwd");

      String name = (String) request.getAttribute("name");

      out.print("uname :"+uname+", upwd: "+upwd+", name:"+name);
    %>
  </body>
</html>
```

打开服务器

```
uname :null, upwd: null, name:null
```

跳转ss02：upwd由于remove后删除

```
uname :admin, upwd: null, name:zhangshan
```

注意session和request作用域的区别：

> 在请求转发中，session和request都是有效的
>
> 在重定向中，session有效

将ss02改为：

```java
@WebServlet("/ss02")
public class Session02 extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //session域对象 和 request域对象 比较
        HttpSession session = req.getSession();
        session.setAttribute("uname","admin");
        session.setAttribute("upwd","123456");

        session.removeAttribute("upwd");

        req.setAttribute("name","zhangshan");

        //请求转发
        resp.sendRedirect("index.jsp");
    }
}
```

跳转ss02：

```
uname :admin, upwd: null, name:null
```

只要服务器端还在，在客户端不管打开关闭该页面，session都还在。

#### Session域对象销毁

1. **默认到期：**
   在Tomcat 的conf的web.xml修改（30分钟，如果继续操作，将重新计时）

```xml
<session-config>
    <session-timeout>30</session-timeout>
</session-config>
```

**2.自己设定到期时间：**

```java
//获取session对象最大活动时间
session.getMaxInactiveInterval();
//修改
session.setMaxInactiveInterval(15);//15秒失效
```

**3.立即销毁**：

```java
session.invalidate();
```

**4.关闭浏览器**

**5.关闭服务器**

### ServletContext对象

​		每一个web应用都有且仅有一个ServletContext 对象，又称**Application对象**，从名称中可知，该对象是与应用程序相关的。在WEB容器启动的时候，会为每一个WEB应用程序创建一个对应的ServletContext对象。
​		该对象有两大作用，第一、作为域对象用来共享数据，此时数据在整个应用程序中共享；第二、该对象中保存了当前应用程序相关信息。例如可以通过`getServerlnfo()` 方法获取当前服务器信息，`getRealPath(String path)`获取资源的真实路径等。

#### ServletContext对象的获取

```java
//1.通过req对象获取
ServletContext servletContext1 = req.getServletContext();
//2.通过session对象获取,很多时候没有req对象，需要使用session对象
ServletContext servletContext2 = req.getSession().getServletContext();
//3.通过ServletConfig对象获取
ServletContext servletcontext3 = getServletConfig().getServletContext();
//4.直接获取
ServletContext servletContext4 = getServletContext();
```

常用方法

```java
//1.获取服务器的版本信息
String serverInfo = req.getServletContext().getServerInfo();
//2.获取当前项目路径
String path = req.getServletContext().getRealPath("/");
```

#### ServletContext域对象

ServletContext域对象是Servlet三大域对象最大的一个，其数据能在整个应用程序获取

### 文件下载和上传

#### 文件上传

##### 前台页面

​		在做文件上传的时候，会有一个上传文件的界面，首先我们需要一个表单， 并且表单的请求方式为**POST**；其次我们的form表单的**enctype**必须设为`"multipart/form-data"`，即`enctype="multipart/form-data"`,意思是设置表单的类型为文件上传表单。默认情况下这个表单类型是`"application/x-www-form-urlencoded"`，不能用于文件上传。只有使用了`multipart/form-data`才能完整地传递文件数据。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>文件上传</title>
</head>
<body>
<!--
    文件上传
    1.准备表单
    2.设置表单提交类型为post
    3.设置enctype="multipart/form-data"
    4.设置文件提交的地址
    5.准备表单元素
        1.普通的表单项： type="text"
        2.文件项：  type="file"
    6.设置表单元素的name属性值
-->
    <form method="post" enctype="multipart/form-data" action="uploadServlet">
        姓名<input type="text" name="uname"><br>
        文件<input type="file" name="myfile"><br>
        <button>提交</button>
    </form>
</body>
</html>
```

##### 后台代码

使注解 **@MultipartConfig** 将一个Servlet标识为支持文件上传，Servlet将`multipart/form-data`的**post**请求封装成Part，通过Part对上传的文件进行操作。

```java
@WebServlet("/uploadServlet")
@MultipartConfig   //文件上传表单必须要该注解
public class uploadServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("文件上传...");
        //设置请求编码格式
        req.setCharacterEncoding("UTF-8");
        //获取普通表单项
        String uname = req.getParameter("uname");
        System.out.println("uname:"+uname);
        //上传文件：获取part对象
        Part part = req.getPart("myfile");
        String fileName = part.getSubmittedFileName();
        System.out.println("fileName:"+fileName);
        //得到文件存放路径
        String filePath = req.getServletContext().getRealPath("/");
        System.out.println("文件存放的路径："+filePath);
        //上传文件
        part.write(filePath+"/"+fileName);
    }
}
```

```
文件上传...
uname:祝金
fileName:天选.txt
文件存放的路径：D:\IDEA\Cookies\out\artifacts\Cookies_war_exploded\
```

#### 文件下载

将服务器上资源下载到本地，有两种下载方式：超链接下载、代码下载

##### 超链接下载

在HTML或JSP使用a标签时，原本是跳转，但遇到浏览器不识别的资源时就会下载，也可通过download属性规定浏览器下载

默认下载

```html
<a href="text.zip">超链接下载</a>
```

指定download下载

```html
<a href="text.zip" download>超链接下载</a>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>文件下载</title>
</head>
<body>
    <a href="download/天选.txt">文本文件</a>
    <a href="download/zfb.JPG">下载图片</a>
    <a href="download/账号本.xlsx">不能识别的文件</a>
</body>
</html>
```

注意：在web文件夹下新建download文件夹，在服务器打开时不会识别和加载，需要在IDEA中配置add configuration -->deployment-->add-->library-->选择download文件夹，并且修改application context为`/Cookies/download`（/当前项目/文件夹）

##### 后台实现加载

实现步骤：

1. 需要通过 response.setContentType 方法设置 Content-type 头字段的值，为浏览器无法使用某种方式或激活某个程序来处理MIME类型，例如"application/octct-stream" 或 "application/x-msdownload"等。
2. 需要通过 response.setHeader 方法设置Content-Disposition 头的值为"attachment;filename=文件名"
3. 读取下载文件，调用response.getOutputStream  方法向客户端写入附件内容

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>文件下载</title>
</head>
<body>
    <a href="download/天选.txt">文本文件</a>
    <a href="download/zfb.JPG">下载图片</a>
    <a href="download/账号本.xlsx">不能识别的文件</a>
    <hr>
    <form action="downloadServlet">
        文件名：<input type="text" name="fileName" placeholder="请输入要下载的文件名"><!-- 实现后台下载-->
        <button>下载</button>
    </form>
</body>
</html>
```

```java
/*
	具体步骤：
	1.设置请求编码
	2.获取文件下载路径
	3.获取要下载的文件名
	4.通过路径得到file对象
	5.判断file对象是否存在，且是否是一个标准文件
		1.设置相应类型
		2.设置头信息
		3.得到输入流
		4.得到输出流
		5.定义byte数组
		6.定义长度
		7.循环输出
		8.关闭流，释放资源
*/
```

```java
@WebServlet("/downloadServlet")
public class DownLoadServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("文件下载...");
        req.setCharacterEncoding("UTF-8");
        resp.setContentType("text/html;charset=UTF-8");//注意这两个不同！
        String fileName = req.getParameter("fileName");
        //参数非空判断
        if(fileName==null||"".equals(fileName.trim())){
            resp.getWriter().write("失败");
            resp.getWriter().close();
            return;
        }
        //得到路径
        String path = req.getServletContext().getRealPath("/download/");//这里最后已经有个斜杠了，不用在file的pathname里补充
        //通过路径得到对象
        File file = new File(path+fileName);
        //判读文件是否存在且是标准文件
        if(file.exists()&&file.isFile()){
            //1. 需要通过 response.setContentType 方法设置 Content-type 头字段的值，为浏览器无法使用某种方式或激活某个程序来处理MIME类型，例如"application/octct-stream" 或 "application/x-msdownload"等。
            //2. 需要通过 response.setHeader 方法设置Content-Disposition 头的值为"attachment;filename=文件名"
            //3. 读取下载文件，调用response.getOutputStream  方法向客户端写入附件内容
            resp.setContentType("application/x-msdownload");
            resp.setHeader("Content-Disposition","attachment;filename="+fileName);
            //得到输入流
            InputStream in = new FileInputStream(file);
            //得到的是文件，字符是无法输出的，需要得到字节输出流
            ServletOutputStream out = resp.getOutputStream();
            //定义Byte数组
            byte[] bytes = new byte[1024];
            int len = 0;
            //循环输出
            while ((len=in.read(bytes))!=-1){
                //输出内容
                out.write(bytes,0,len);
            }
            //关闭流
            out.close();
            in.close();
        }else {
            resp.getWriter().write("文件不存在！");
            resp.getWriter().close();
        }
    }
}

```

## 用户登入实验

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>用户登入</title>
</head>
<body>
<div style="text-align: center">
    <form actionnn="/login" method="post" id="loginForm">
        姓名：<input type="text" name="uname" id="uname"><br>
        密码：<input type="password" name="upwd" id="upwd"><br>
        <span id="msg" style="font-size: 12px;color: red"></span><br>
        <button type="button" id="loginBtn">登入</button>
        <button type="button">注册</button>
    </form>
</div>
</body>
<!--引入js-->
<script type="text/javascript" src="/js/jquery-3.5.1.min.js"></script>
<script type="text/javascript">
    /***
     *  js校验
     1.给登入按钮绑定点击事件
     2.获取用户名和密码的值
     3.判断是否为空：提示使用span标签
     4.如果不为空，则手动提交表单
     */
    $("#loginBtn").click(function (){
        //获取用户名和密码值
        var uname = $("#yname").val();//使用id选择器找到变量
        var upwd = $("#upwd").val();
        if(isEmpty(uname)){
            //如果检测到为空，提示用户 span 标签
            $("#span").html("用户姓名不能为空");
        }
        if(isEmpty(upwd)){
            //如果检测到为空，提示用户 span 标签
            $("#msg").html("用户密码不能为空");
        }
        $("#loginForm").submit();
    });

    function isEmpty(str){
        if(str==null|| str.trim()==""){
            return true;
        }
        return false;
    }
</script>
</html>
```

分层思想

> Controller层：接受请求（调用service层返回结果）
>
> ​						响应结果
>
> Service层：业务逻辑判断
>
> mapper层（DAO）：接口类，
>
> ​							MaBatis和数据库操作
>
> util ：一些工具类
>
> entity ( PO )： JavaBean 实体类
>
> 

<font color="yellow">是的</font>

## 过滤器和监听器

### 处理请求乱码问题

```java
/**
Post 请求在tomcat8以上或7以下都有乱码问题：
	request.setCharacterEncoding("UTF-8");
GET 请求在tomcat7及以下出现乱码，所以需要先得到服务器版本号再处理
*/
@WevFilter("/*")
public class AEncodingFilter implements Filter{
    public AEcondingFilter(ServletRequest arg0, ServletResponse arg1, filterChain chain) throws Exceotion{}
    public void destroy(){}
    public void doFilter(){
        //先基于Http请求
        HttpServletRequest requset = (HttpServletRequest) arg0;
        HttpServletResponse reponse = (HttpServletResponse) arg1;
        request.setCharacterEncoding("UTF-8");//Post请求直接处理
        String method = request.getMethod();//获取是否是Get请求
        if("GET".equalsIgnoreCase(method)){
            String serverInfo = request.getServletContext().getServerInfo();//服务器信息 Apache Tomcat/8.0.45
            String versionStr = serverInfo.substring(serverInfo.indexOf("/")+1,serverInfo.indexOf("."));//获取大版本号
            if(Integer.parseInt(versionStr)<8){
                //得到自定义内部类，（MyWapper继承的类实现了HttpServletRequest接口）因此myrequest也是request对象
                HeepServletRequset myRequest = new MaWapper(request);
                chain.doFilter(myRequest, reponse);
                return;
            }
        }
        chain.doFilter(myRequest, response);
        return;
    }
}

class MyWapper extends HttpServletRequestWrapper{
    private HttpServletRequest request;
    public MyWapper(HttpServeletRequest request){//因此需要带参构造来传递request对象
        super(request);
        this.request = request;
    }
    //重写getParameter方法
    @override
    public String getParameter(String name){
        String value = request.getParameter(name);//方法用到了request对象
        if(value != null && !"".equals(value.trim())){
            try{
                value = new String(value.getBytes("ISO-8859-1"),"UFT-8");//这是get方法处理参数乱码的地方
            }catch(UnsupportedEncodingException e){
				e.printStackTrace();                
            }
        }
        return value;
    }
}
```

### 用户非法访问拦截

```java
/**
	不能所有页面都拦截，比如登入，注册页面,静态资源（img,js,css）！！！！操作
*/
@WebFilter("/*")
public class LoginAccessFilter implements Filter{
    
    //生命周期方法省略
    @override
    public void doFilter(ServletRequest servletRequest,ServletResponse servletResponse,FilterChain filterChain) throws Exception{
        HttpServletRequest requset = (HttpServletRequest) servletRequest;
        HttpServletResponse reponse = (HttpServletResponse) servletResponse;
        //获取请求路径
        String url = request.getRequestURI();
        if(url.contains("/login.jsp")){
            filterChain.doFilter(request, response);
            return;
        }
        if(url.contains("/js")||url.contains("/css")||url.contains("/img")){//这些都是指定目录
            filterChain.doFilter(request, response);
            return;
   		}
         if(url.contains("login")){//比如login.jsp中提交的表单含有login，即可放行
            filterChain.doFilter(request, response);
            return;
        }
    }
}
```

## 监听器

​		web监听器是Servlet中一种的特殊的类, 能帮助开发者监听web中的特定事件，比如`ServletContext`,`HttpSession,` `ServletRequest` 的创建和销毁;变量的创建、销毁和修改等。可以在某些动作前后增加处理， 实现监控。例如可以用来统计在线人数等。

监听器有三类8种：

(1)监听生命周期:
	ServletRequestListener
	HttpSessionListener|
	ServletContextListener
(2)监听值的变化:
	ServletRequestAttributeListener
	HttpSessionAttributeListener
	ServletContextAttributeListener
(3)针对session中的对象:



### 在线人数监控

```java
@WebListener
public class onlineListener implements HttpSessionListener{
    private Integer onlineNumber = 0;
    @override
    public void sessionCreated(HttpSessionEvent httpSessionEvent){
        //人数+1
        onlineNumber+1;
        //将人数设置到session作用域中
        httpSessionEvent.getSession().setAttribute("onlineNumber",onlineNumber);//
        //应该改成
        httpSessionEvent.getServletContext().setAttribute("onlineNumber",onlineNumber);
    }
    @override
    public void sessionDestroyed(HttpSessionEvent httpSessionEvent){
        //人数-1
        onlineNumber-1;
    }  
}
```

```java
@WebServlet("/online")
public class OnlineServlet extends HttpServlet{
    @override
    protected void service(HttpServletRequest req,HttpServletResponse resp) throws ServletException, IOException{
        HttpSession session = req.getSession();
        Integer onlineUnmber = (Integer) session.getAttribute("onlineNumber");
        resp.setContentType("text/html;charset=UTF-8");
        resp.getWriter().write("当前在线人数"+onlineNumber);
        //但是更改浏览器后页面不会改变,需要改用Application的对象
    }
}
```

# Maven

用于项目管理：统一jar包依赖，构建多模块项目，

瀑布式开发、敏捷开发

### Maven四大特性

#### 依赖管理系统

```xml
<dependency>
	<groupId>javax.servlet</groupId> com.baidu
    <artifactId>javax.servlet-api</artifactId> ueditor echars
    <version>3.0</version>
</dependency>
```

**坐标属性的理解**

Maven坐标为各种组件引入了秩序，任何一个组件都必须明确定义自己的坐标。
**groupld**
定义当前Maven项目隶属的实际项目公司名称。(jar包所在仓库路径) 由于Maven中模块的概念, 因此一个实际项目往往会被划分为很多模块。比如spring是一个实际项目， 其对应的Maven模块会有很多，如spring-core,spring-webmvc等。
**artifactld**
该元素定义实际项目中的一一个Maven模块项目名，推荐的做法是使用实际项目名称作为artifactld的前缀。比如: spring bean, spring-webmvc等。
**version**
该元素定义Maven项目当前所处的版本。

#### 多模块构建

​		项目复查时dao service controller层分离将一个项目分解为多个模块已经是很通用的一种方式。

​		在Maven中需要定义一个parent POM作为一组module的聚合POM。在该POM中可以使用`<modules>`标签来定义一组子模块。parent POM不会有什么实际构建产出。而parent POM中的build配置以及依赖配置都会自动继承给子module。

#### 一致的项目结构

Ant时代大家创建Java项目目录时比较随意，然后通过Ant配置指定哪些属于source，那些属于testSource等。而Maven在设计之初的理念就是Conversion over configuration (约定大于配置)。其制定了一套项目目录结构作为标准的Java项目结构，解决不同ide带来的文件目录不一致问题。

#### 一致的构建模型和插件机制

```xml
<plugin>
	<groupId>org.mortbay.jetty</groupId> com.baidu
    <artifactId>maven-jetty-plugin</artifactId> ueditor echars
    <version>6.1.25</version>
    <configuration>
    	<scanIntervalSecond>10</scanIntervalSecond>
        <contextPath>/test</contextPath>
    </configuration>
</plugin>
```

### maven命令

需要在pom.xml的目录地址下运行

`mvn [plugin-name]:[goal-name]`

| 命令                   | 描述                                                    |
| ---------------------- | ------------------------------------------------------- |
| mvn -version           | 查看版本                                                |
| mvn clean              | 清理项目生成的零时文件，一般是模块下的target目录        |
| mvn compile            | 编译源代码，一般编译src/main/java目录                   |
| mvn package            | 项目打包工具，会在target模块下生成jar或war等文件        |
| mvn test               | 测试命令，或执行sec/test/java下的junit测试用例          |
| mvn install            | 将打包的jar/war文件复制到你的本地仓库中，供其他模块使用 |
| mvn deploy             | 将打包的文件发布到远程参考，供其他人员进行下载依赖      |
| mvn site               | 生成项目相关信息的网站                                  |
| mvn eclipse:eclipse    | 将项目转化为Eclipse项目                                 |
| mvn dependency:tree    | 打印出项目的整个依赖树                                  |
| mvn archetype:generate | 创建Maven普通jiava项目                                  |
| mvn tomcat7:run        | 在tomcat容器中运行web应用                               |
| mvn jetty:run          | 调用jetty插件Run目录在jetty servlet容器中启动web应用    |

#### 命令参数

###### -D 传入属性参数

例如:
`mvn package -Dmaven. test. ski p=true`
以`-D`开头,将`maven. test. skip`的值设为true ,就是告诉maven打包的时候跳过单元测试。
同理，`mvn deploy - Dmaven. test. skip=true`代表部署项目并跳过单元测试。

###### -P 使用指定的Profile配置



### IDEA配置maven

#### 普通java项目

创建java项目，选择maven，勾选，添加`maven-archetype-quickstart`

在file>new project setup >setting for new projects 配置好后

如果初次编译出现plugin错误：在pom.xml 添加：

```xml
    <dependencies>
        <dependency>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-install-plugin</artifactId>
            <version>2.4</version>
            <type>maven-plugin</type>
        </dependency>

        <dependency>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-deploy-plugin</artifactId>
            <version>2.7</version>
            <type>maven-plugin</type>
        </dependency>

        <dependency>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>2.12.4</version>
            <type>maven-plugin</type>
        </dependency>

        <dependency>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-site-plugin</artifactId>
            <version>3.3</version>
            <type>maven-plugin</type>
        </dependency>
</dependencies>
```

随后生成src目录,包含main和test目录

然后add configuration > maven 一般添加compile命令，和package命令

campile后生成target目录

package 运行后再target生成jar包

#### IDEA配置web项目

1. 创建Maven项目:模板选择`maven-archetype-webapp`
2. 自动下载
3. 在pom.xml 中修改jdk为1.8
   删除plugin相关（33-54行）
   使用单元测试的化junit改成4.12
4. 需要将服务器插件部署
   在build中添加plugins标签，jetty和tomcat

```xml
	<plugin>
        <groupId>org.mortbay.jetty</groupId>
        <artifactId>maven-jetty-plugin</artifactId>
        <version>6.1.25</version>
        <configuration>
          <!--热部署，每10秒扫描一次-->
          <scanIntervalSeconds>10</scanIntervalSeconds>
          <!-- 可指定当前项目的站点名 -->
          <contextPath>/test</contextPath>    <!--用于浏览器访问站点-->
          <connectors><!--如果要随机分配端口，把下面三行注释掉，在add configuration中添加 jetty:run -Djetty.port=8899 -->
            <connector implementation="org.mortbay.jetty.nio.SelectChannelConnector">
              <port>9090</port> <!-- 设置启动的端口号-->
            </connector>
          </connectors>
        </configuration>
      </plugin>
```

```xml
<!-- 设置在p1ugins标签中-->
<plugin>
	<groupId>org.apache.tomcat.maven</groupId>
	<artifactId>tomcat7-maven-plugin</artifactId>
	<version>2.1</version>
	<configuration>
		<port>8081</port> <!-- 启动端口默认:8080 -->
		<path>/test</path> <!-- 项目的站点名，即对外访问路径-->
		<uriEncoding>UTF-8</uriEncoding> <!-- 字符集编码默认: IS0-8859-1 -->
		<server>tomcat7</server> <!-- 服务器名称-->
	</configuration>
</plugin>
```

### maven仓库

​		当第一次运行Maven命令的时候，你需要Internet链接， 因为它需要从网上下载一些文件。 那么它从哪里下载呢?它是从Maven默认的远程库下载的。这个远程仓库有Maven的核心插件和可供下载的jar文件。

​		对于Maven来说，仓库只分为两类: **本地仓库**和**远程仓库**。

​		当Maven根据坐标寻找构件的时候，它首先会查看本地仓库，如果本地仓库存在，则直接使用；如果本地没有，Maven就会去远程仓库查找，发现需要的构件之后，下载到本地仓库再使用。如果本地仓库和远程仓库都没有, Maven就会报错。

​		远程仓库分为三种:*中央仓库*, *私服*，*其他公共库*。

​		中央仓库是默认配置下，Maven下载jar包的地方。

​		私服是另一种特殊的远程仓库，为了节省带宽和时间，应该在局域网内架设一个私有的仓库服务器，用其代理所有外部的远程仓库。内部的项目还能部署到私服上供其他项目使用。
​		一般来说， 在Maven项目目录下，没有诸如lib/这样用来存放依赖文件的目录。当Maven在执行编译或测试时，如果需要使用依赖文件,它总是基于坐标使用本地仓库的依赖文件。
​		默认情况下，每个用户在自己的用户目录下都有一个路径名为`.m2/repository/`的仓库目录。有时候， 因为某些原因(比如c盘空间不足) ,需要修改本地仓库目录地址。
​		对于仓库路径的修改，可以通过maven配置文件conf目录下`settings.xml`来指定仓库路径

### 打包

1、建立对应的目录结构

![image-20220515090438701](D:\typora_mds\2022！\Resources\maven打包目结构.png)

2、在pom.xml添加profiles配置

```xml
<profiles>
    <profile>
      <id>dev</id>
      <properties>
        <env>dev</env>
      </properties>
      <!--未指定环境时默认打包dev环境-->
      <activation>
        <activeByDefault>true</activeByDefault>
      </activation>
    </profile>
    <profile>
      <id>test</id>
      <properties>
        <env>test</env>
      </properties>
    </profile>
    <profile>
      <id>product</id>
      <properties>
        <env>product</env>
      </properties>
    </profile>
  </profiles>
```

3、设置资源文件配置

在pom.xml的build里面添加：

```xml
    <resources>
      <resource>
        <directory>src/main/resources/${env}</directory>
      </resource>
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
```

4、执行打包操作

在add configuration 添加maven命令：

```
clean compile package -Pdev -Dmaven.test.skip=true
```

-P选取profiles的内容，参数为dev，则打包开发文件

-D 表示测试代码不打包

5、打包完成：在target目录会生成war包



Bean：符合规范的java类：

```
所有属性为private
提供默认构造方法
提供getter和setter
实现serializable接口
```



# SPRING

[(18条消息) Spring-全面详解（学习总结）_策谋本天成的博客-CSDN博客_spring](https://blog.csdn.net/weixin_44207403/article/details/106736102?ops_request_misc=%7B%22request%5Fid%22%3A%22161443766616780357241220%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=161443766616780357241220&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_click~default-1-106736102.first_rank_v2_pc_rank_v29&utm_term=Spring)

开源的javaEE程序，基于分布式的应用程序、轻量级框架，主要核心：

- IOC：控制反转/依赖注入  

  ```java
  /**IOC:使程序组件或类之间尽量形成一种松耦合结构，开发者在使用类的实例之前，先创建对象的实例，但是IOC将创建的任务交给IoC容器，这样开发应用代码时只需要直接	使用类的实例。
  依赖注入有三种实现类型，spring实现后两种：
  	1.接口注入
  	2.Setter注入（最广泛）:*/
  	public class User{
  		private String name;
  		public String getName(){
              return name;
          }        
          public void setName(String name){
              this.name = name;
          }
  		/**
  		3.构造器注入：基于构造方法为属性赋值，好处是对象的实例化的同时也完成了属性的实例化
  		*/
  	}
  ```

- AOP：面向切面编程   动态代理

主要：配置管理

​		Bean对象的实例化-IOC

​		继承第三方框架

​		Spring Security

​		Quartz 时钟框架

​	自带服务

​	Mail  邮件发送

​	定时任务处理，定时调度。

​	消息处理（异步）

### Spring框架

1. 创建Maven 的java项目

2. 在pom.xml导入spring配置(在 mvn官网)

   ```xml
       <!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
       <dependency>
         <groupId>org.springframework</groupId>
         <artifactId>spring-context</artifactId>
         <version>5.3.18</version>
       </dependency>
   ```
3. src/main/ava包创建bean类，在src/main/下创建resources，创建spring.xml文件

4. 将类的参数配置到spring.xml文件中（文件模板在spring官方网站找到）
   将bean 的id 和class写入

5. 

   ```xml
   <?xml version="1.0" encoding="UTF-8"?><!--第一行是必须的，自己写也要会-->
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
           https://www.springframework.org/schema/beans/spring-beans.xsd">
           <!--bean标签的唯一标识，class为路径--><!--命名空间一般在官方文档中给出-->
       
       <bean id="userServices" class="com.xxxx.services.UserServices">
           <!-- collaborators and configuration for this bean go here -->
       </bean>
       <!-- more bean definitions go here -->
   
   </beans>
   ```
   
6. 随后在测试类可以实例化

   ```java
   package com.xxxx.test;
   
   import com.xxxx.services.UserServices;
   import org.springframework.context.ApplicationContext;
   import org.springframework.context.support.ClassPathXmlApplicationContext;
   
   public class Starter01 {
       public static void main(String[] args) {
           //得到spring上下文环境
           ApplicationContext ac = new ClassPathXmlApplicationContext("spring.xml");
           //通过id属性值到指定bean对象
           UserServices userServices = (UserServices)ac.getBean("userServices");
           userServices.test();
       }
   }
   ```

### Spring IOC 容器

`IoC：将对象的实例化交给外部容器（IoC容器，工厂角色）负责；属性赋值的擦操作`

#### Bean对象实例化模拟

定义Bean属性对象

思路：

1. 定义Bean工厂接口，提供获取bean方法
2. 定义Bean工厂接口实现类，计息 

###### 1.定义Bean属性对象

用来接受配置文件中Bean标签的id和class属性值

```java
package com.xxxx.spring;

/**
 * 用来存放配置文件中id和class
 */
public class MyBean {
    private String id;
    private String clazz;

    public MyBean() {
    }

    public MyBean(String id, String clazz) {
        this.id = id;
        this.clazz = clazz;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getClazz() {
        return clazz;
    }

    public void setClazz(String clazz) {
        this.clazz = clazz;
    }
}

```

###### 2.引入dom4j依赖和xPath(jaxen)

```xml
<!-- https://mvnrepository.com/artifact/org.dom4j/dom4j -->
    <dependency>
      <groupId>org.dom4j</groupId>
      <artifactId>dom4j</artifactId>
      <version>2.1.3</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/jaxen/jaxen -->
    <dependency>
      <groupId>jaxen</groupId>
      <artifactId>jaxen</artifactId>
      <version>1.1.6</version>
    </dependency>
```

###### 3.自定义配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans>
    <!--设置javaBean对应的bean标签-->
    <bean id="UserDao" class="com.xxxx.dao.UserDao"></bean>
    <bean id="userService" class="com.xxxx.service.UserService"></bean>
</beans>
```

###### 4.定义Bean工厂

```java
package com.xxxx.spring;
/**
 * 工厂的目的是提供规范
 * Bean工厂接口：
 *          通过id属性值获取变量
 */
public interface MyFactory {
    public Object getBean(String id);
}

```

###### 5.定义Bean接口实现类

```java
package com.xxxx.spring;

import org.dom4j.*;
import org.dom4j.io.SAXReader;
import java.net.URL;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

/**   这是MyFactory工厂的具体实现类
 * 模拟spring实现：
 *      1、通过带参构造器获得对应的配置文件
 *      2、通过dom4j解析配置文件 ，得到list集合（存放bean标签的id和class属性）
 *      3、通过反射得到对应的实例化对象，存放在map对象中（通过遍历list集合，获取对应的class属性） class.forName(class).newInstance();
 *      4、通过id获取指定的实例化对象
 */
public class MyClassPathApplicationContext implements MyFactory{

    private List<MyBean> beanList;//存放从配置文件中获得到的bean标签的消息（myBean代表的就是每一个bean标签）
    private Map<String,Object> beanMap = new HashMap<>();

    public MyClassPathApplicationContext(String fileName) {
        /*通过dom4j解析配置文件 ，得到list集合（存放bean标签的id和class属性）*/
        this.parseXml(fileName);
        /*通过反射得到对应的实例化对象*/
        this.instanceBean();
    }


    /**
     * 通过dom4j解析配置文件 ，得到list集合（存放bean标签的id和class属性）
     *      1、获取解析器
     *      2、获取配置文件的url
     *      3、解析配置文件xml
     *      4、通过Xpath语法解析，获取beans标签下所有的bean标签
     *      5、通过指定的语法解析文档对象，返回元素集合
     *      6、判断元素集合是否为空
     *          不为空：遍历集合
     *      7、获取bean标签元素的属性，id和class
     *      8、获取MyBean对象，再将id和class属性值设置到对象中，再将对象设置为MyBean的集合中
     * @param fileName
     */
    private void parseXml(String fileName) {
        //获取解析器
        SAXReader saxReader = new SAXReader();
        //获取配置文件和url
        URL url = this.getClass().getClassLoader().getResource(fileName);
        //学习Xpath语法
        try {
            Document document = saxReader.read(url);
            XPath xPath = document.createXPath("beans/bean");
            //通过指定的语法解析文档对象，返回元素集合
            List<Node> elementList = xPath.selectNodes(document);
            //判断元素集合是否为空
            if(elementList!=null && elementList.size()>0){
                //实例化beanList
                beanList = new ArrayList<>();
                for(Node e : elementList){
                    String id = e.valueOf("id");
                    String clazz = e.valueOf("class");
                    MyBean myBean = new MyBean(id,clazz);
                    beanList.add(myBean);
                }
            }

        } catch (DocumentException e) {
            e.printStackTrace();
        }
    }

    /**
     * 通过反射得到对应的实例化对象，放置在map对象
     *  1.判断对象集合是否为空，如果不为空，则遍历集合，获取对象的id和class属性
     *  2.通过类的全路径名，反射得到实例化对象 Class.forName(class).newInstance();
     *  3.将bean对象放入map对象中
     */
    private void instanceBean() {
        if(beanList!=null&& beanList.size()>0){
            for(MyBean bean : beanList){
                String id = bean.getId();
                String clazz = bean.getClazz();
                try {
                    Object object = Class.forName(clazz).newInstance();
                    beanMap.put(id,object);
                } catch (Exception e) {
                    e.printStackTrace();
                }

            }
        }
    }

    @Override
    public Object getBean(String id) {
        return beanMap.get(id);
    }
}
```

### Spring核心技术

使用的到技术：

1. 工厂设计模式（简单工厂  工厂方法  抽象工厂）
2. XML解析（dom4j）
3. 反射技术（实例化对象   反射获取方法，获取属性，构造器）
4. 策略模式（加载资源）
5. 单例模式（IoC实例化对象）

#### 多配置文件时

当有两个XML文件时`service.xml`    `dao.xml`想让两文件都加载

1.可变参数，可以传入多个文件名

```java
ApplicationContext ac = new ClassPathXmlApplicationContext("spring.xml","dao.xml");
```

2.将两个文件import至一个总配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<bean>
<import resource="service.xml"/>
<import resource="dao.xml"/>
</bean>
```

Bean对象实例化方法 

1. 构造器实例化
2. 静态工厂实例化
3. 实例化工厂实例化

### Spring IoC注入

A类对B类的依赖，通过在A类实例化B类，或者在A类中定义B类，在构造器中传入B

支持四种注入：**setter注入、构造器注入、静态工厂注入、实例化工厂注入**

#### 自动装配

**注解方式注入Bean**

对于bean的注入，除了使用xml配置以外，可以使用注解配置。注解的配置，可以简化配置文件，提高开发的速度，使程序看上去更简洁。对于注解的解释，Spring对于注解有专门的解释器，对定义的注解进行解析，实现对应bean对象的注入。通过反射技术实现。

**准备环境**

1.修改配置文件

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">
    <context:annotation-config/><!--开启自动化装配-->

    <bean id="userService" class="com.xxxx.service.UserService"></bean>
    <bean id="userDao" class="com.xxxx.dao.UserDao"></bean>


</beans>
```

2.开启自动化注入

```xml
<context:annotation-config/>
```

3.给注入的bean对象添加注解

```java
package com.xxxx.service;

import com.xxxx.dao.UserDao;
import javax.annotation.Resource;

public class UserService {
    @Resource//只需添加注解
    UserDao userDao ;

    public void setUserDao(UserDao userDao) {//Setter方法其实可以不用
        this.userDao = userDao;
    }

    public void test(){
        System.out.println("UserService test...");
        userDao.test();
    }
}
/**
	@Resource 实现自动注入
	1、注解默认通过属性字段名称查找对应的bean对象
	2、如果属性字段不一样，则会通过类型查找
	3、属性字段可以提供setter方法或者不要
	4、注解可以声明在属性字段上，或setter方法级别
	5、可以设置注解的name属性，name属性值要与bean标签属性值一样		@Resource(name="userDao")
			当一个接口具有多个实现类时，需要使用name
*/
```

@Resource注解



@Autowired注解（用法和Resource大致类似）

- 通过默认类型（Class类型）查找bean对象、与属性字段名无关
- 属性可以提供set方法，也可不提供
- 注解可以声明在属性级别也可以setter级别
- 可以添加@Qualifier 结合使用，通过value属性查找bean对象（name属性值要与bean标签属性值一样）

### Spring IoC 扫描器

实际开发中，bean的数量非常多。通过注解来简化

#### 扫描器配置 

```
Spring IoC配置
	作用：bean对象统一进行管理，简化开发配置
1、设置自动化扫描范围
	如果bean对象未在指定包范围，即使声明了注解，也无法实例化
2、使用指定的注解（声明在类级别） bean对象的id属性默认是 类（首字母小写）
	Dao层：
		@Repository
	Service层：
		@Service
	Controller层：
		@Controller
	任意类：
		@Component
```

###### 例子：

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">
    <context:component-scan base-package="com.xxxx"/><!--只需这一个标签就能将com.xxxx的类使用注解注入-->

</beans>
```

新建Dao层`TypeDao`和Service层`TypeService`，通过注解注入：

```java
package com.xxxx.dao;

import org.springframework.stereotype.Repository;
//注解声明在类级别
@Repository
public class TypeDao {
    public void test(){
        System.out.println("Test Type...");
    }
}
```

```java
package com.xxxx.service;

import com.xxxx.dao.TypeDao;
import org.springframework.stereotype.Service;

import javax.annotation.Resource;

@Service
public class TypeService {
    @Resource
    TypeDao typeDao = new TypeDao();
    public void test(){
        System.out.println("Test TypeService...");
        typeDao.test();
    }
}
```

```java
//测试
public class App 
{
    public static void main( String[] args )
    {
        ApplicationContext ac = new ClassPathXmlApplicationContext("spring02.xml");
        TypeService typeService = (TypeService) ac.getBean("typeService");//只需实例化Service层就能调用Dao层
        typeService.test();
    }
}
//能运行
```

### bean作用域

什么对象适合作为单例对象？（什么对象适合交给IoC容器实例化？）

​		<u>无状态对象</u>：不存在会改变当前对象状态的成员变量，如Controller，Service，Dao层

​		实际上对象状态的变化往往均是由于属性值得变化而引起的，比如user类姓名属性会有变化，属性姓名的变化一般会引起user对象状态的变化。对于我们的程序来说，无状态对象没有实例变量的存在，保证了线程的安全性，service 层业务对象即是无状态对象。线程安全的。

### bean生命周期

包含4个阶段

Bean定义：
				在配置文件中定义bean
				通过bean标签定义bean对象

Bean初始化：
				IoC容器启动时，自动实例化Bean对象
				1、在配置文档中指定 `init-method`属性来完成
				2、实现 `org.springframework.beans.factory.InitializationBean` 接口

Bean的使用：

​			BeanFactory
​			ApplicationContext

Bean的销毁：

​			在配置文档中指定`destory-method`属性

## AOP

### 代理模式

为某一个对象提供一个代理，用来控制对这个对象的访问。

> ​		代理模式在Java开发中是一种比较常见的设计模式。设计目的旨在为服务类与客户类之间插入其他功能，插入的功能对于调用者是透明的，起到伪装控制的作用。如租房的例子:房客、中介、房东。对应于代理模式中即:客户类、代理类、委托类(被代理类)。
> ​		为某一个对象(委托类)提供以个代理(代理类)，用来控制对这个对象的访问。委托类和代理类有一个共同的父类或父接口。代理类会对请求做预处理、过滤，将请求分配给指定对象。

1. 委托类和代理类需要有共同的父接口/类（具有相同的行为）
2. 代理类可以增强委托类的行为

代理类会对请求做预处理、过滤、将请求分配给指定对象

#### 静态代理

​		某个对象提供一个代理，代理角色固定，以控制对这个对象的访问。代理类和委托类有共同的父类或父接口，这样在任何使用委托类对象的地方都可以用代理对象替代。代理类负责请求的预处理、过滤、将请求分派给委托类处理、以及委托类执行完请求后的后续处理。

代理三要素：

1. 有共同的行为（定义接口）
2. 目标角色（实现接口）
3. 代理角色（实现接口+增强用户行为）

静态代理特点：

1. 目标角色固定
2. 在应用程序之前就知道目标角色
3. 代理对象会增强目标对象的行为
4. 有可能存在多个代理，产生“类爆炸”

#### 动态代理

​		相比于静态代理，动态代理在创建代理对象上更加的灵活，动态代理类的字节码在程序运行时，由Java反射机制动态产生。它会根据需要，通过反射机制在程序运行期，动态的为目标对象创建代理对象，无需程序员手动编写它的源代码。动态代理不仅简化了编程工作，而且提高了软件系统的可扩展性，因为反射机制可以生成任意类型的动态代理类。代理的行为可以代理**多个方法**，**即满足生产需要的同时又达到代码通用的目的**。动态代理的两种实现方式:
1. JDK动态代理
2. CGLIB动态代理

动态代理特点：

1. 目标对象不固定
2. 在应用程序执行时动态创建目标对象
3. 代理对象会增强目标对象的行为

##### JDK动态代理

```java
/**
 * 获取动态代理需要三个参数，返回代理类的实例
 * public static Object newProxyInstance(ClassLoader loader,
 *                                       Class[] interface,
 *                                       InvocationHandler h)
 *        loader：类加载器
 *        interface：目标对象的接口数组:由于目标对象不确定，所以使用带参构造器传递
 *        h：调度方法调用的调用处理函数：
 * 每一个动态代理类，如果想要获取其代理对象的话，必须实现InvocationHandler接口
 * @return
 */
public class JdkHandler implements InvocationHandler{
    private Object target ;
    public JdkHandler(Object target) {
        this.target = target;
    }
    //获取代理对象方法
    public Object getProxy(){
        Object object = Proxy.newProxyInstance(this.getClass().getClassLoader(), target.getClass().getInterfaces(),this);
        return object;
    }

    /**
     * 1、调用目标对象的方法，返回Object
     * 2、增强目标对象的行为
     *
     * @param proxy 调用该方法的代理实例
     * @param method 目标对象的方法
     * @param args  目标对象的方法所需要参数
     * @return
     * @throws Throwable
     */
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        //调用目标对象的方法
        Object object = method.invoke(target,args);
        //用户增强行为
        System.out.println("用户增强行为");
        return object;

    }
}
```

本例接口：

```java
public interface Marry {
    public void toMarry();
}
```

本例实现类：

```java
public class You implements Marry{
    @Override
    public void toMarry() {
        System.out.println("运行：实现类重写接口方法");
    }
}
```

运行测试：

```java
public static void main( String[] args )
    {
        You you = new You();
        JdkHandler jdkHandler  = new JdkHandler(you);
        Marry marry = (Marry) jdkHandler.getProxy();
        marry.toMarry();
    }
```

```
运行：实现类重写接口方法
用户增强行为（来自动态代理）
com.sun.proxy.$Proxy0	//这一行是加了输出Proxy.getClass().getName()
```



##### CGLIB动态代理

实现原理：**继承思想**

JDK动态代理：基于**接口方式**（代理类和目标类要实现同一接口）

​     	JDK的动态代理机制只能代理实现了接口的类，而不能实现接口的类就不能使用JDK的动态代理，cglib是针对类来实现代理的，它的原理是对指定的目标类生成一个子类，并覆盖其中方法实现增强，但因为采用的是继承，所以不能对fina修饰的类进行代理。

```xml
<!-- https://mvnrepository.com/artifact/cglib/cglib -->
<dependency>
    <groupId>cglib</groupId>
    <artifactId>cglib</artifactId>
    <version>3.3.0</version>
</dependency>

```

```java
public class CglibInterceptor implements MethodInterceptor {
    Object target = null;

    public CglibInterceptor(Object target) {
        this.target = target;
    }

    /**
     * 获取代理对象
     *          通过Enhancer对象
     * @return
     */
    public Object getProxy(){
        Enhancer enhancer = new Enhancer();//通过Enhancer 对象的create方法生成一个类
        enhancer.setSuperclass(target.getClass());//设置父类(父类由构造器传入)
        enhancer.setCallback(this);//设置拦截器，回调对象为本身对象
        //生成代理类对象并返回
        return enhancer.create();
    }

    /**
     * 拦截器：
     *          1、目标对象的方法调用
     *          2、增强行为
     * @param o cglib动态生成的实例
     * @param method    实体类中所调用的被调用方法的引用
     * @param objects   数组（参数列表）
     * @param methodProxy   生成的代理类对方法的代理引用
     * @return
     * @throws Throwable
     */
    @Override
    public Object intercept(Object o, Method method, Object[] objects, MethodProxy methodProxy) throws Throwable {
        Object object = methodProxy.invoke(target, objects);
        //增加增强行为
        System.out.println("增强行为");
        return object;
    }
}
//调用和JDK类似：目标对象可以没有实现接口
```

### AOP

<font size=4px>能做什么</font>：应用于日志记录，性能统计，安全控制，事务处理（实现公共功能性的重复使用）

<font size=4px>特点</font>：

1. 降低了模块之间的耦合度，提高业务代码的聚合度
2. 提高代码的复用性
3. 提高系统的扩展性
4. 可以在不影响原有功能的基础上添加新的功能

#### 搭建

坐标引入，注意还要spring的依赖

```xml
<!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.9.1</version>
    <scope>runtime</scope>
</dependency>

```

添加spring.xml的配置

添加命名空间

```
xmlns:aop="http://www.springframework.org/schema/aop"
```

```
http://www.springframework.org/schema/aop
http://www.springframework.org/schema/aop/spring-aop.xsd
```

#### 注解实现

```java
/** 切面  = 切入点 + 通知
 *          切入点：定义类要拦截哪些类的哪些方法
 *          通知：定义拦截值后要做什么
 *
 */
@Aspect
@Component//将对象交给IoC容器来实例化
public class LogCut {
    /**
     * 切入点：定义类要拦截哪些类的哪些方法
     *         :匹配规则：拦截什么方法
     *         @Pointcut("匹配规则")
     *              *表示修饰范围（public,private,protected）：所有范围
     *              com.xxxx.service.*.* : 第一个* ：表示包下的所有类
     *                                      第二个* ：表示类的所有 方法
     *                                      (..)： 表示方法参数
     *         Aop常用表达式：
     *              1、执行所有公共方法：
     *                  execution(public *(..))
     *              2、执行任意的set方法
     *                  execution(* set*(..))
     *              3、设定指定包下的任意类的任意方法
     *                  execution(* com.xxxx.service.*.*(..))
     *              4、设定指定包及子包(比如service下还有包)
     *                  execution(* com.xxxx.service..*.*(..))
     */
    @Pointcut("execution(* com.xxxx.service..*.*(..))")
    public void cut(){
    }

    /**
     * 目标类方法执行前，执行该通知
     */
    @Before(value = "cut()")//指向切面
    public void before(){
        System.out.println("前置通知");
    }

    /**
     * 目标类方法在无异常执行后执行
     */
    @AfterReturning(value = "cut()")
    public void afterReturn(){
        System.out.println("返回通知");
    }

    /**
     * 目标类方法执行后执行（有异常和无异常）
     */
    @After(value = "cut()")
    public void after(){
        System.out.println("最终通知...");
    }

    /**
     * 出现异常通知
     */
    @AfterThrowing(value = "cut()")
    public void afterThrow(){
        System.out.println("异常通知...");
    }

    /**
     * 环绕通知：将通知声明到指定的切入点上
     *         目标类的方法执行前后，都可以通过环绕通知响应处理
     *         需要通过显式调用的方法，否则无法访问所指定方法
     *              pjp.proceed()
     * @Param pjp
     * @return
     */
    @Around(value = "cut()")
    public Object around(ProceedingJoinPoint pjp) {
        System.out.println("环绕通知--前置通知...");
        Object object = null;
        try{
            object = pjp.proceed();
            System.out.println(pjp.getTarget());
            System.out.println("环绕通知--返回通知...");
        }catch (Throwable throwable){
            System.out.println("环绕通知--异常通知...");
        }
        System.out.println("环绕通知--最终通知...");
        return object;
    }
}
```

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop.xsd">
    <context:component-scan base-package="com.xxxx"/>
<!--配置Aop自动代理-->
    <aop:aspectj-autoproxy/>

</beans>
```

#### XML实现

所有相关注解删掉就行

```java
@Component
public class Logcut02 {

    /**
     * 切入点：定义类要拦截哪些类的哪些方法
     *         :匹配规则：拦截什么方法
     *         @Pointcut("匹配规则")
     *              *表示修饰范围（public,private,protected）：所有范围
     *              com.xxxx.service.*.* : 第一个* ：表示包下的所有类
     *                                      第二个* ：表示类的所有 方法
     *                                      (..)： 表示方法参数
     *         Aop常用表达式：
     *              1、执行所有公共方法：
     *                  execution(public *(..))
     *              2、执行任意的set方法
     *                  execution(* set*(..))
     *              3、设定指定包下的任意类的任意方法
     *                  execution(* com.xxxx.service.*.*(..))
     *              4、设定指定包及子包(比如service下还有包)
     *                  execution(* com.xxxx.service..*.*(..))
     */
    @Pointcut("execution(* com.xxxx.service..*.*(..))")
    public void cut(){

    }

    /**
     * 目标类方法执行前，执行该通知
     */
   
    public void before(){
        System.out.println("前置通知");
    }

    /**
     * 目标类方法在无异常执行后执行
     */

    public void afterReturn(){
        System.out.println("返回通知");
    }

    /**
     * 目标类方法执行后执行（有异常和无异常）
     */
   /* @After(value = "cut()")
    public void after(){
        System.out.println("最终通知...");
    }*/

    /**
     * 出现异常通知
     */

    public void afterThrow(){
        System.out.println("异常通知...");
    }

    /**
     * 环绕通知：将通知声明到指定的切入点上
     *         目标类的方法执行前后，都可以通过环绕通知响应处理
     *         需要通过显式调用的方法，否则无法访问所指定方法
     *              pjp.proceed()
     * @Param pjp
     * @return
     */

    public Object around(ProceedingJoinPoint pjp) {
        System.out.println("环绕通知--前置通知...");
        Object object = null;
        try{
            object = pjp.proceed();
            System.out.println(pjp.getTarget());
            System.out.println("环绕通知--返回通知...");
        }catch (Throwable throwable){
            System.out.println("环绕通知--异常通知...");
        }
        System.out.println("环绕通知--最终通知...");
        return object;
    }

}

```

```xml
<aop:config>
        <aop:aspect ref="logcut02">
            <aop:pointcut id="cut" expression="execution(* com.xxxx.service..*(..))"/>
            <aop:before method="before" pointcut-ref="cut"/>
            <aop:after-returning method="afterReturn" pointcut-ref="cut"/>
            <aop:after method="after" pointcut-ref="cut"/>
            <aop:around method="around" pointcut-ref="cut"/>
        </aop:aspect>
</aop:config>
```

### 配置类*

[(18条消息) Spring学习笔记_code_java_zqy的博客-CSDN博客](https://blog.csdn.net/sinat_41847122/category_10845774.html)

主配置
xml文件配置的方式
先按照我们以前配置的方式来使用Spring，给出主配置XML：
首先有一个Person类：



```java
public class Person {
    private String name;
    private Integer age;
public Person() {
}

public Person(String name, Integer age) {
    this.name = name;
    this.age = age;
}

public String getName() {
    return name;
}

public void setName(String name) {
    this.name = name;
}

public Integer getAge() {
    return age;
}

public void setAge(Integer age) {
    this.age = age;
}

@Override
public String toString() {
    return "Person{" +
            "name='" + name + '\'' +
            ", age=" + age +
            '}';
}
}
主配置文件
```
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	   xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
<bean id="person" class="com.ldc.bean.Person">
	<property name="age" value="18"></property>
	<property name="name" value="张三"></property>
</bean>
</beans>
```

测试

```java
public class MainTest {
    public static void main(String[]args){
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("beans.xml");
        Person person = (Person) applicationContext.getBean("person");
        System.out.println(person);
    }
}
```


输出结果为：

```
Person{name=‘张三’, age=18}
```


注解的方式：主配置类@Configuration
首先我们先写一个配置类：其作用与xml配置文件相同，均是给Spring做出一些配置和导入一些组件

```java
/**

 * 配置类就等同以前的配置文件
   */
   @Configuration //告诉Spring这是一个配置类
   public class MainConfig {

   //相当于xml配置文件中的<bean>标签，告诉容器注册一个bean
   //之前xml文件中<bean>标签有bean的class类型，那么现在注解方式的类型当然也就是返回值的类型
   //之前xml文件中<bean>标签有bean的id，现在注解的方式默认用的是方法名来作为bean的id
   @Bean
   public Person person() {
       return new Person("lisi",20);
   }

}
```


测试：

```java
public class MainTest {
    public static void main(String[]args){
        /**
         * 这里是new了一个AnnotationConfigApplicationContext对象，以前new的ClassPathXmlApplicationContext对象
         * 的构造函数里面传的是配置文件的位置，而现在AnnotationConfigApplicationContext对象的构造函数里面传的是
         * 配置类的类型
         */
        ApplicationContext applicationContext = new AnnotationConfigApplicationContext(MainConfig.class);
        Person person = applicationContext.getBean(Person.class);
        System.out.println(person);
    }
}
```


输出结果为：

```
Person{name=‘张三’, age=18}
```


@Configuration源码

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Component
public @interface Configuration {
/**
 * Explicitly specify the name of the Spring bean definition associated
 * with this Configuration class. If left unspecified (the common case),
 * a bean name will be automatically generated.
 * <p>The custom name applies only if the Configuration class is picked up via
 * component scanning or supplied directly to a {@link AnnotationConfigApplicationContext}.
 * If the Configuration class is registered as a traditional XML bean definition,
 * the name/id of the bean element will take precedence.
 * @return the specified bean name, if any
 * @see org.springframework.beans.factory.support.DefaultBeanNameGenerator
 */
String value() default "";
    }
```


从@Configuration 这个注解点进去就可以发现这个注解上也标注了 @Component 的这个注解，说明被他标注的主配置类也纳入到IOC容器中作为一个组件

组件扫描：@ComponentScan
作用：自动扫描注册组件并可以指定特定的扫描规则

XML配置文件方式
在xml文件配置的方式，我们可以这样来进行配置：

```xml
<!-- 包扫描、只要标注了@Controller、@Service、@Repository，@Component 均可以将其作为组件扫描进来-->
<context:component-scan base-package="com.ldc"/>
```
@ComponentScan注解方式
以前是在xml配置文件里面写包扫描，现在我们可以在配置类里面写包扫描：

```java
/**

 * 配置类就等同以前的配置文件
   */
   @Configuration //告诉Spring这是一个配置类
   @ComponentScan(value = "com.ldc")//相当于是xml配置文件里面的<context:component-scan base-package="com.ldc"/>
   public class MainConfig {

   //相当于xml配置文件中的<bean>标签，告诉容器注册一个bean
   //之前xml文件中<bean>标签有bean的class类型，那么现在注解方式的类型当然也就是返回值的类型
   //之前xml文件中<bean>标签有bean的id，现在注解的方式默认用的是方法名来作为bean的id
   @Bean(value = "person")//通过这个value属性可以指定bean在IOC容器的id
   public Person person01() {
       return new Person("lisi",20);
   }

}
```


测试：
我们创建BookController、BookService、BookDao这几个类，分别添加了@Controller、@Service、@Repository注解：

```java
@Controller
public class BookController {
}
```

```java

@Service
public class BookService {
}
```

```java
   @Test
    public void test01() {
        ApplicationContext applicationContext = new AnnotationConfigApplicationContext(MainConfig.class);
        String[] definitionNames = applicationContext.getBeanDefinitionNames();
        for (String name : definitionNames) {
            System.out.println(name);
        }
    }
```


结果如下：除开IOC容器自己要装配的一些组件外，还有是我们自己装配的组件

```
org.springframework.context.annotation.internalConfigurationAnnotationProcessor
org.springframework.context.annotation.internalAutowiredAnnotationProcessor
org.springframework.context.annotation.internalRequiredAnnotationProcessor
org.springframework.context.annotation.internalCommonAnnotationProcessor
org.springframework.context.event.internalEventListenerProcessor
org.springframework.context.event.internalEventListenerFactory
mainConfig
bookController
bookDao
bookService
person
```


从上面的测试结果我们可以发现主配置类 MainConfig 也是IOC容器里面的组件，也被纳入了IOC容器的管理。

@ComponentScan源码：


```java
@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.TYPE})
@Documented
@Repeatable(ComponentScans.class)
public @interface ComponentScan {
    @AliasFor("basePackages")
    String[] value() default {};
@AliasFor("value")
String[] basePackages() default {};

Class<?>[] basePackageClasses() default {};

Class<? extends BeanNameGenerator> nameGenerator() default BeanNameGenerator.class;

Class<? extends ScopeMetadataResolver> scopeResolver() default AnnotationScopeMetadataResolver.class;

ScopedProxyMode scopedProxy() default ScopedProxyMode.DEFAULT;

String resourcePattern() default "**/*.class";

boolean useDefaultFilters() default true;

ComponentScan.Filter[] includeFilters() default {};
	//这个是要排除的规则：是按注解来进行排除还是按照类来进行排除还是按照正则表达式来来进行排除
ComponentScan.Filter[] excludeFilters() default {};

boolean lazyInit() default false;

@Retention(RetentionPolicy.RUNTIME)
@Target({})
public @interface Filter {
    FilterType type() default FilterType.ANNOTATION;

    @AliasFor("classes")
    Class<?>[] value() default {};

    @AliasFor("value")
    Class<?>[] classes() default {};

    String[] pattern() default {};
    }
 }
```
这个时候，我们就可以这样来配置：

```java
@Configuration
@ComponentScan(value = "com.ldc",excludeFilters = {
        //这里面是一个@Filter注解数组，FilterType.ANNOTATION表示的排除的规则 ：按照注解的方式来进行排除
        //classes = {Controller.class,Service.class}表示的是标有这些注解的类给排除掉
        @Filter(type = FilterType.ANNOTATION,classes = {Controller.class,Service.class})
})
public class MainConfig {
@Bean(value = "person")
public Person person01() {
    return new Person("lisi",20);
}
}
```

