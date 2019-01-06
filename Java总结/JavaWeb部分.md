## Java web部分

### 1. http中get和post请求 的区别
#### 1.1 共同点：
都是http的请求方式。URL全称是资源描述符，我们可以这样认为：一个URL地址，它用于描述一个网络上的资源，而HTTP中的GET，POST，PUT，DELETE就对应着对这个资源的查，改，增，删4个操作。大家应该有个大概的了解了，GET一般用于获取/查询资源信息，而POST一般用于更新资源信息。但是一种操作也可以完成这些操作，因为他们本质上就是TCP链接，只是都有自己的语义环境，使用时最好区分一下。
#### 1.2 区别：
- **url参数可见性**，Get请求提交的数据会在地址栏中显示，通过拼接url进行传递参数；而post请求通过request body体传输参数不会在地址栏中显示出来。<br/>从这个方面讲，post的安全性要比get安全性高一些。如果没有加密，他们安全级别都是一样的，随便一个监听器都可以把所有的数据监听到。
- **传输数据大小**。由于浏览器或服务器的限制，Get传送的数据量较小，一般不能大于2KB。post传送的数据量较大，一般被默认为不受限制。
- **缓存性**，GET请求会被浏览器主动cache，而POST不会，除非手动设置。
- **后退页面的反应**，GET在浏览器回退时是无害的，POST会再次提交请求。
- **编码**，GET请求只能进行url编码，而POST支持多种编码方式。
- GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留。
- GET只接受ASCII字符的参数的数据类型，而POST没有限制。

### 2. 说说你对servlet的理解或者 servlet 是什么？
> Servlet（Servlet Applet），全称Java Servlet,是**用Java编写的服务器端程序。而这些Servlet都要实现Servlet这个接口**。其主要功能在于交互式的浏览和修改数据，生成动态Web内容。Servlet运行于支持Java的应用服务器中。<br/>
HttpServlet 重写doGet 和 doPost 方法或者你也可以重写service方法完成对get和post请求响应。

### 3. 简单说一下Servlet的生命周期
Servlet运行在Servlet容器中，其生命周期由容器来管理。Servlet的生命周期通过`javax.servlet.Servlet`接口中的`init()、service()`和`destroy()`方法来表示。

Servlet的生命周期包含了下面4个阶段：
- 1.加载
- 2.实例化
- 3.初始化
- 4.请求处理
- 5.服务终止

Servlet启动时，开始加载Servlet生命周期开始，Servlet被服务器实例化后，容器运行其init方法，请求到达时运行期service方法，service方法自动运行与请求对应的doXXX方法（doGet、doPost）等，当服务器决定是将实例销毁的时候，调用其destroy方法。
加载Servlet的class===》实例化Servlet===》调用Servlet的init方法完成初始化===》响应请求（调用Servlet的service方法）===》Servlet容器关闭（调用Servlet的destroy方法）：

![Servlet的生命周期](http://img.my.csdn.net/uploads/201211/06/1352204684_1548.jpg)

### 4.forward（转发）与redirect（重定向）的区别
#### 4.1 区别
- **forward** 是**服务器的转向**，用request对象调用；而**redirect** 是**客户端的跳转**，用response对象调用。
- 使用**forward**浏览器地址不会发生改变，而**redirect** 会发生改变。
- **forward**是一次请求中完成，而**redirect** 是重新发起请求。
- **forward**是在服务端完成，而不用在客户端重新发起请求，效率较高。
#### 4.2 转发过程 
- **forward** 是**服务器的转向，是服务器行为**。
> **转发过程**：客户浏览器发送http请求——》web服务器接受此请求——》调用内部的一个方法在容器内部完成请求处理和转发动作——》将目标资源发送给客户；<br/>

- 在这里，转发的路径必须是同一个web容器下的url，其不能转向到其他的web路径上去.<br/>
- *中间传递的是自己的容器内的request*。客户端浏览器只发出一次请求，Servlet把请求转发给Servlet、HTML、JSP或其它信息资源，由第2个信息资源响应该请求，两个信息资源共享同一个request对象。<br/>
- 在客户浏览器路径栏显示的仍然是其第一次访问的路径，也就是说客户是感觉不到服务器做了转发的。<br/>
- 转发行为是浏览器只做了一次访问请求。
> `request.getRequestDispatcher("new.jsp").forward(request, response);   //转发到new.jsp`

#### 4.3 重定向过程
- **redirect** 是**客户端的跳转，是客户端行为**。
 
  > **重定向过程**：客户浏览器发送http请求——》web服务器接受后发送302状态码响应及对应新的location给客户浏览器——》客户浏览器发现是302响应，则自动再发送一个新的http请求，请求url是新的location地址——》服务器根据此请求寻找资源并发送给客户。
- 在这里location可以重定向到任意URL，既然是浏览器重新发出了请求，则就没有什么request传递的概念了。因此它本质上是两次HTTP请求，对应两个request对象。
- 在客户浏览器路径栏显示的是其重定向的路径，客户可以观察到地址的变化的。
- 重定向行为是浏览器做了至少两次的访问请求的。
> `response.sendRedirect("new.jsp");   //重定向到new.jsp`

### 5. JSP与Servlet的区别与联系
#### 5.1 相同点：
- 1.Jsp 是Servlet技术的拓展，所有的JSP文件都会被翻译成一个继承HttpServlet的类，也就是说JSP最终也是一个Servlet，这个Servlet对外提供服务。
- 2. (JSP的本质就是Servlet，JVM只能识别java的类，不能识别JSP的代码,Web容器将JSP的代码编译成JVM能够识别的java类)。

#### 5.2 不同点：
- 1. jsp更擅长表现于页面显示,servlet更擅长于逻辑控制.
- 2. Servlet中没有内置对象，Jsp中的内置对象都是必须通过HttpServletRequest对象，HttpServletResponse对象以及HttpServlet对象得到.
- 3. Jsp是Servlet的一种简化，JSP在静态HTML内容中嵌入Java代码组合成一个扩展名为.jsp的文件，Java代码被Jsp容器动态执行后生成HTML内容。<br/>
Servlet是个完整的Java类，这个类的Service方法用于生成对客户端的响应。在Java代码中通过HttpServletResponse对象中的获取Write对象动态输出HTML内容。

### 6. Session与Cookie的区别？

#### 6.1 共同点：
Session和Cookie都是会话跟踪技术。Cookie是通过在**客户端**记录信息确定用户身份，Session是通过在**服务端**记录信息确定用户身份。但是Session的实现依赖于Cookie，sessionId（Session的唯一标识需要存放在客户端）。
#### 6.2 区别：
- 1.cookie 数据存放在客户的浏览器上，session数据存放在服务器上。
- 2.cookie不是很安全，别人可以分析存放在本地的cookie并进行cookie欺骗，考虑到安全应当使用session。
- 3.session会在一定时间内保存在服务器上。当访问增多是，会比较占用服务器的性能，考虑到减轻服务器性能方面的负担，应当使用cookie。
- 4.单个cookie保存的数据不能超过4k,很多浏览器限制一个站点最多保存20个cookie。
- 5.所以建议：
  - 将登录等重要信息存放在session，
  - 其他信息如果需要保留一可以放在cookie中，
  - 比如购物车：购物车最好使用cookie，但是cookie是可以在客户端被禁用的，这个时候我们要使用cookie+数据库的方式实现，当从cookie中不能取出数据时，就从数据库获取。

### 7.JSP中九大内置对象和作用域
#### 7.1 九大内置对象
1. **request** 对象代表的是 **来自客户端的请求**
   > 例如我们在FORM表单中填写的信息等，是最常用的对象
   > 常用的方法有：getParameter、getParameterNames 和getParameterValues 通过调用这几个方法来获取请求对象中所包含的参数的值。

2. **response** 对象代表的是**对客户端的响应**

   > 也就是说可以通过response 对象来组织发送到客户端的数据。但是由于组织方式比较底层，所以不建议普通读者使用，需要向客户端发送文字时直接使用

3. **pageContext** 代表的是**当前页面运行的一些属性**，对象直译时可以称作“页面上下文”对象
    > 常用的方法有 ：findAttribute、getAttribute、getAttributesScope 和getAttributeNamesInScope
    一般情况下pageContext对象用到得也不是很多，只有在项目所面临的情况比较复杂的情况下，才会利用到页面属性来辅助处理。
4. **session**对象代表**服务器与客户端所建立的会话**
	> 当需要在不同的JSP页面中保留客户信息的情况下使用，
	>- 比如在线购物、客户轨迹跟踪等。
	>- “session” 对象建立在cookie的基础上，所以使用时应注意判断一下客户端是否打开了cookie。常用的方法包括getId、 getValue、 getValueNames和putValue等。
	>- **概要**:
	>>- HTTP是无状态（stateless）协议；
	>>- Web Server 对每一个客户端请求都没有历史记忆；
	>>- Session用来保存客户端状态信息；
	>>- 由Web Server 写入；存于客户端；
	>>- 客户端的每次访问都把上次的session记录传递给Web Server；
	>>- Web Server读取客户端提交的session来获取客户端的状态信息

5. **application** 对象负责**提供应用程序在服务器中运行时的一些全局信息,表示Servlet正在执行的内容**

   > 常用的方法有getMimeType和getRealPath等。

6. **out** 对象代表了**向客户端发送数据的对象**
   >用来传送会有的输出，与“response” 对象不同，通过“out” 对象发送的内容将是浏览器需要显示的内容，是文本一级的，可以通过“out” 对象直接向客户端写一个由程序动态生成HTML文件。<br/><br/>
   > 常用的方法除了pirnt和println之外，还包括clear、clearBuffer、flush、getBufferSize和getRemaining，这是因为“out” 对象内部包含了一个缓冲区，所以需要一些对缓冲区进行操作的方法

7. **config** 对象**提供一些配置信息**

   > Servlet的架构部件，常用的方法有getInitParameter和getInitParameterNames，以获得Servlet初始化时的参数。

8. **page** 对象代表了**正在运行的由JSP文件产生的类对象**

   > 不建议一般读者使用。

9. **exception** 对象则代表了**JSP文件运行时所产生的例外对象**

    > 针对错误网页，未捕捉的例外，此对象不能在一般JSP文件中直接使用，而只能在使用了`<%@ page isErrorPage="true "%>`的JSP文件中使用。
#### 7.2 四大作用域

**pageContext**、**request**、**session**、**application**，可以通过jstl表达式从四大作用域中取值。

| 编号 | 对象            | 所属作用域      | 作用域描述               |
| ---- | --------------- | --------------- | ------------------------ |
| 1    | **request**     | **request**     | 在当前**请求**中有效     |
| 2    | **response**    | **page**        | 在当前**页面**有效       |
| 3    | **out**         | **page**        | 在当前**页面**有效       |
| 4    | **session**     | **session**     | 在当前**会话**中有效     |
| 5    | **application** | **application** | 在所有**应用程序**中有效 |
| 6    | **config**      | **page**        | 在当前**页面**有效       |
| 7    | **pageContext** | **page**        | 在当前**页面**有效       |
| 8    | **page**        | **page**        | 在当前**页面**有效       |
| 9    | **Exception**   | **page**        | 在当前**页面**有效       |


### 8. MVC模式和mvc各部分的实现
- Model 模型    JavaBean（dao）
- View  视图    HTML、jsp等
- Controller 控制器 Servlet、Action、Controller

最经典的Model2：jsp +  servlet + service + dao;<br/>
Model1:Jsp + service + dao;

- Model 表示应用程序核心，是应用程序中用于处理应用程序数据逻辑的部分通常模型对象负责在数据库中存取数据。 
- View（视图） 相当于前台，是应用程序中处理数据显示的部分。 通常视图是依据模型数据创建的。
- Controller（控制器）相当于控制页面跳转，是应用程序中处理用户交互的部分。 通常控制器负责从视图读取数据，控制用户输入，并向模型发送数据。