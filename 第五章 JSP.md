###### 第五章 JSP

```html
1.JSP简介
	全称：Java Server Pages，Java的服务页面
	JSP必须要运行在服务器上，不能脱离服务器单独运行
	JSP是可以写Java代码的Html；还是披着Html外衣的Servlet
	JSP本质上就是一个Servlet

2.JSP运行原理 😀
	当我们访问jsp页面时会经历以下步骤：
		1）JSP引擎将jsp页面翻译成java文件
		2）Java虚拟机将java文件编译成class文件
		3）JSP容器根据对应的类创建对象并调用_jspService()方法处理用户的请求
		以访问index.jsp页面为例：
			第一次访问index.jsp页面
				1）JSP引擎将index.jsp页面翻译成index_jsp.java文件
				2）Java虚拟机将index_jsp.java文件编译成index_jsp.class文件
				3）JSP容器根据index_jsp这个类创建对象并调用_jspService()方法处理用户的请求
			以后再访问index.jsp页面（前提是没有改变页面中的内容）
				直接使用JSP容器根据index_jsp这个类创建对象并调用_jspService()方法处理用户的请求

3.JSP基本语法
	1）模板元素
		就是HTML标签，在HTML中怎么用，在JSP中就怎么用
		<a href="/Web08_JSP/index.jsp">我是一个超链接</a>
	2）JSP脚本片段
		格式：<% 里面写Java代码 %>
		JSP脚本片段是用来写Java代码的
		在JSP页面中可以有多个脚本片段，但是要保证多个脚本片段拼接之后的完整性
		<%
        	for(int i = 0 ; i < 100 ; i ++){
            	//out.print("对于修宪你怎么看？");
    	%>  
        	<h1>对于修宪你怎么看？</h1>
    	<%  
        	}
    	%>
	3）JSP表达式
		格式：<%= 对象 %>
		JSP表达式是用来向浏览器输出一个对象
	4）JSP中可以写的注释
		<!--
        	第一种是HMTL注释
        	第二种是Java注释
        	第三种是JSP注释
     	-->
     	<%-- 我是JSP注释 --%>
            
4.JSP指令 😀
	格式：<%@ 指令名 属性名1="属性值1" 属性名2="属性值2" %>
	常用指令
	1.page指令：用来告诉服务器如何解析当前页面
		属性：
		language：用来设置开发语言，默认值是java，可选值也是java
		contentType：设置内容的类型，用来告诉浏览器使用什么字符集进行解码，对应的java文件的_jspService()方法中会有以下内容：
		response.setContentType("text/html; charset=UTF-8");😀
		pageEncoding：用来设置当前页面使用的字符集
                
		errorPage：用来设置当当前页面出现异常要转发到的页面          
		isErrorPage：用来设置当前页面是否是一个错误页面。默认是false，
			如果该为true,则可以通过exception对象获取异常信息
		import：用来导包，通常会重新创建一个page指令并通过import属性进行导包     
     
     2.include指令：用来将其他页面包含到当前页面中
     	file：用来设置要包含的页面的地址
     	通过这种方式实现的包含只翻译、编译当前页面，不翻译、编译被包含的页面，这种包含称为静态包含
     	<%@ include file="/include.jsp" %>
         
5.JSP动作标签
	格式：<jsp:标签名 属性名="属性值"></jsp:标签名>
	常用的动作标签
	forward标签
	1.forward标签：用来进行请求的转发
		page：用来设置要转发的请求
		<!-- 不带请求参数的转发，注意：标签体重不能包含任何内容 -->
			<jsp:forward page="/index.jsp"></jsp:forward>
    	<!-- 带请求参数的转发 -->
    		<jsp:forward page="/index.jsp">
        		<jsp:param value="superAdmin" name="username"/>
    		</jsp:forward> 
	2.include标签：用来将其他页面中的内容包含到当前页面中
    	page：用来设置要包含的页面的地址
    	通过这种方式实现的包含既翻译、编译当前页面也翻译、编译被包含的页面，这种包含我们称为动态包含
    	<!-- 如果被包含的页面是一个静态页面，通常我们使用静态包含；如果被包含的页面是一个动态页面，通常我们使用动态包含 -->
    	<jsp:include page="/include2.jsp"></jsp:include>
         
6.JSP中九大隐含对象 😀
	JSP的隐含对象即在jsp页面中不用声明就可以直接使用的对象
	JSP的隐含对象之所以可以直接使用是因为在对于的Java类的_jspService()方法中已经声明了这些对象
	九大隐含对象：😀
		pageContext
			类型：
         		PageContext
			作用：
         		一个顶九个，通过它可以获取其他八个隐含对象
			它还是一个域对象
		request
			类型：
         		HTTPServletRequest
			作用：
         		与Servlet中的request的作用一样
			它还是一个域对象
		session
			类型：
         		HttpSession
			在Servlet中通过以下方式获取
				HttpSession session = request.getSession();
			它还是一个域对象
		application
			类型：
         		ServletContext
			在Servlet中通过以下方式获取
				ServletContext application = this.getServletContext();
			它还是一个域对象
		response
			类型：
         		HTTPServletResponse
			作用：
         		与Servlet中的response作用一样
		config
			类型：
         		ServletConfig
			作用：
         		获取配置信息
		out
			类型：
         		JspWriter
			作用：
         		与PrintWriter的作用类似，可以向浏览器响应一些数据
		page
			类型：
         		Object
			作用：
         		相当于this，代表当前对象（在jsp中几乎不用）
		exception
			类型：
         		Throwable
			作用：
         		获取异常信息。前提是jsp页面是一个错误页面，即jsp页面的page指令中的isErrorPage属性值为true
         
7.四个域对象 😀
	域指区域或者说是范围，在JavaWeb中指不同的Web资源（Servlet、jsp页面）
	由于不同的Web资源之间需要共享数据，所以就有了域对象
	四个域对象中都维护着一个Map，用来存、取要共享的数据
	四个域对象都有以下三个方法：😀
		void setAttribute(String key , Object value)
			向域对象中添加属性（设置要共享的数据）
		Object getAttribute(String key)
			根据属性名从域对象中获取属性值（获取要共享的数据）
		void removeAttribute(String key)
			根据属性名从域对象中移除属性值
	四个域 😀
		page域
			范围：当前页面
			对应的域对象：pageContext
		request域
			范围：当前请求（一次请求）
			对应的域对象：request
		session域
			范围：当前会话（一次会话）
			对应的域对象：session
		application域
			范围：当前Web应用
			对应的域对象：application
	四个域的使用规则 😀
		能用小的就不用大的
		Servlet与Jsp的分工
		Servlet负责处理请求；Jsp负责显示页面
```

