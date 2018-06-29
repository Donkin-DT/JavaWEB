###### 第四章 Servlet

```java
1.创建Servlet的HelloWorld的步骤：😀
	1）创建一个动态的Web工程，并创建一个类实现Servlet接口
		public class HelloServlet implements Servlet {
			@Override
			public void init(ServletConfig config) throws ServletException {
    		}
    		
    		@Override
			public ServletConfig getServletConfig() {
				return null;
			}
		
			//service()方法就是处理用户请求的方法
			@Override
			public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
				System.out.println("你的请求我已经收到……");
				//设置字符集：
				res.setContentType("text/html;charset=UTF-8");
				PrintWriter writer = res.getWriter();
				//给浏览器响应一个字符串
				//获取一个打印流
				PrintWriter writer = res.getWriter();
				writer.print("Response Success!");
    		}
    	
			@Override
			public String getServletInfo() {
				return null;
			}
		
			@Override
			public void destroy() {
            }
		}
		
	2）在web.xml配置文件中注册实现类 😀
		<?xml version="1.0" encoding="UTF-8"?>
		<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 			xmlns="http://java.sun.com/xml/ns/javaee" xsi:schemaLocation="http://java.sun.com/xml/ns/javaeehttp://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" id="WebApp_ID" version="2.5">
  		<!-- 注册Servlet 😀 -->
  		<servlet>
    		<!-- 给Servlet起一个名字，名字可以任意指定，不过我们通常以实现类的类名作为名字 -->
    		<servlet-name>HelloServlet</servlet-name>
    		<!-- 设置实现类的全类名，Servlet容器会根据全类名利用反射实例化该对象 -->
      		<servlet-class>com.atguigu.servlet.helloworld.HelloServlet</servlet-class>
  		</servlet>
  		
  		<!-- 映射Servlet -->
  		<servlet-mapping>
    		<servlet-name>HelloServlet</servlet-name>
    		<!-- 映射请求地址，映射的请求地址可以任意指定，但是这儿指定的是什么，那么浏览器地址栏就得写什么 -->
    		<url-pattern>/MyFirstServlet</url-pattern>
  		</servlet-mapping>
		</web-app>
		
	3）在浏览器地址栏输入地址：
		http://localhost:8080/Web05_Servlet/MyFirstServlet
		
	4）当发送MyFirstServlet这个请求之后，服务器会去web.xml中寻找对应的请求地址的映射，然后创建引用的Servlet实现类的实例并调用service()方法处理用户的请求
		//service()方法就是处理用户请求的方法
    	@Override
		public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
        	System.out.println("你的请求我已经收到……");
        	//给浏览器响应一个字符串
        	//获取一个打印流
        	PrintWriter writer = res.getWriter();
        	writer.print("Response Success!");
    	}
    	
2.Servlet的生命周期 😀
	Servlet的生命周期即Servlet对象从被创建到被销毁的一个过程
	Servlet的生命周期主要体现在以下方法中：
	构造器
		第一次发送请求时被调用，用来创建对象
		在整个生命周期过程中只被调用一次，说明Servlet是单例的 😀
		
	init()
		第一次发送请求时被调用，用来初始化对象
		在整个生命周期过程中只被调用一次
		
	service()
		每次发送请求都会被调用，用来处理用户的请求
		在整个生命周期过程中会被调用多次
		
	destory()
		服务器关闭时调用，用来销毁对象
		在整个生命周期过程中只被调用一次
		
3.ServeltConfig与ServletContext 😀
	ServletConfig
		// ServletConfig代表了当前Servlet的配置信息，它有以下三个作用：
        // 1.获取当前Servlet的名称
        	String servletName = config.getServletName();
        	System.out.println(servletName);
        // 2.获取当前Servlet的初始化参数（只能是当前的Servlet才能获取，其他Servlet不能得到）
        	String initParameter = config.getInitParameter("user");
        	System.out.println(initParameter);
        // 3.获取ServletContext对象
        	ServletContext servletContext = config.getServletContext();

	ServletContext
		//ServletContext代表了当前Web应用，它也有以下三个作用：
        //1.获取当前Web应用的初始化参数（web.xml中注册的所有的Servlet都可以获取）
        	String initParameter2 = servletContext.getInitParameter("encoding");
        	System.out.println(initParameter2);
        //2.获取服务器端资源的真实路径（文件的上传下载时需要用到）
        	String realPath = servletContext.getRealPath("/index.html");
        	System.out.println(realPath);
        //3.它是一个域对象（下回分解）

4.请求和响应
	HttpServletRequest request
	request代表了浏览器发送给服务器的请求报文，该对象由服务器创建并以参数的形式传入到doGet和doPost方法中，在这两个方法中可以直接使用
	//request的作用：
        //1.获取请求参数
        	String username = request.getParameter("username");
        	String password = request.getParameter("password");
        	System.out.println(username);
        	System.out.println(password);
        //2.获取项目的虚拟路径
        	String contextPath = request.getContextPath();
        	System.out.println(contextPath);
        //3.转发
        	//获取转发器
        	RequestDispatcher requestDispatcher = request.getRequestDispatcher("success.html");
        	//转发请求
        	requestDispatcher.forward(request, response);
        //4.它还是一个域对象（下回分解）

	HttpServletResponse response
	response代表了服务器发送给浏览器的响应报文，该对象由服务器创建并以参数的形式传入到doGet和doPost方法中，在这两个方法中可以直接使用
	//response的作用：
        //1.给浏览器响应一个页面或者页面的一个片段
		//PrintWriter writer = response.getWriter();
		//writer.print("<h1>Response Success!</h1>");
        //2.重定向
        response.sendRedirect("success.html");

5.Web中路径问题 😀
	在转发的情况下，由于地址栏地址无变化，此时如果用相对路径就可能导致浏览器解析地址出现异常，所以相对路径不靠谱，建议使用绝对路径
	什么是绝对路径？
		以 / 开头的路径即为绝对路径
	那么 / 代表什么意思呢：
		如果路径由浏览器解析，那么 / 就代表当前服务器，即 http://localhost:8080
		以下路径由浏览器解析 😀
			1）html标签中的路径：如img标签、script标签中的src中的路径；a标签、link标签中href中的路径；form标签中action中的路径等
			
			2）重定向中的路径 😀
				如果路径由服务器解析，那么 / 就代表当前Web应用，即 		http://localhost:8080/Web06_Servlet_Ex
				
	以下路径由服务器解析 😀
		1）web.xml配置文件中url-pattern标签中的路径
		2）转发中的路径
		
6.中文乱码问题 😀
	编码：
		将字符转换为二进制数的过程称为编码
		
	解码：
		将二进制数转换为字符的过程称为解码
	
	乱码：
		编码和解码使用的字符集不一致就会导致乱码
		
	请求乱码：😀
		浏览器→服务器
		
		浏览器编码
			浏览器编码使用的字符集就是html页面中meta标签中指定的字符集<meta charset="UTF-8">
		 
		服务器解码 😀
			服务器默认的字符集是ISO-8859-1
			编码和解码使用的字符集不一致导致乱码
			解决方案：
			对于POST请求
				//设置字符集为UTF-8，该操作一定要在第一次获取请求参数之前进行
        		request.setCharacterEncoding("UTF-8");

			对于GET请求
				在Tomcat服务器的server.xml中的第一个Connector标签中添加属性URIEncoding="UTF-8"
				<Connector connectionTimeout="20000" port="8080" protocol="HTTP/1.1" redirectPort="8443" URIEncoding="UTF-8"/>
				
	响应乱码：😀
		服务器→浏览器
		
		服务器编码
			服务器默认的字符集为ISO-8859-1
                
		浏览器解码
			浏览器解码使用的字符集为GBK
			编码和解码使用的字符集不一致导致乱码
			解决方案：
			//方式一：
        		response.setContentType("text/html;charset=UTF-8");
        	//方式二：
				//response.setHeader("Content-Type", "text/html;charset=UTF-8");
```

