###### 第六章 EL

```jsp
1.EL简介
	全称：Expression Language，翻译过来叫表达式语言
	格式：${表达式}
	EL表达式主要用来将域对象中的属性值输出到页面
	EL表达式默认进行全域查找
		先从page域中开始查找，找到后直接返回，不再去其他域中查找，如果找不到再去request域中查找，以此类推
		如果最终在application域中也找不到将返回一个空串
	如何精确获取指定域中的属性值？
		EL给我们提供了四个Scope对象，用来精确获取指定域中的属性值，这四个Scope对象相当于将四个域对象中的域单独拿了出来
		pageScope
			获取page域中的属性值
		requestScope
			获取request域中的属性值
		sessionScope
			获取session域中的属性值
		applicationScope
			获取application域中的属性值
		<%
        	Date date = new Date();
        	//将date放到域对象中
        	pageContext.setAttribute("date", date+"-");
        	request.setAttribute("date", date+"--");
        	session.setAttribute("date", date+"---");
        	application.setAttribute("date", date+"----");
    	%>
    	通过JSP表达式输出现在的时间：<%=request.getAttribute("date") %><br>
    	通过EL表达式输出现在的时间：${date }<br>
    	通过EL表达式输出request域中现在的时间：${requestScope.date }<br>
		如果域对象中的属性名比较特殊，通过以下方式获取属性值
		request.setAttribute("hello-kitty", "我是一只猫");
		获取request域中的属性名比较特殊的属性值：${requestScope['hello-kitty'] }
	获取JavaBean的属性值
		通过对象.属性名的方式获取JavaBean的属性值，其实调用的是属性对应的get方法
		例如：${requestScope.t.name}，调用的是request域中的t对象所对应的类中的getName()方法
		只要域中对象所对象的类中有getXxx方法，我们就可以通过对象.xxx(get后面单词的首字母小写)的方式获取该方法的返回值
		例如：${requestScope.t.gender }，request域中的t对象所对应的类只要有getGender()方法就可以获取getGender()方法的返回值，不需要有gender这个属性
		如果域中对象的属性还是一个对象，可以通过一直点的方式获取属性值
		<!-- 获取JavaBean中的属性值 -->
    	<%
        	Teacher t = new Teacher(1,"韩总","宏福苑",new Student(1,"章登"));
        	//将t放到request域中
        	request.setAttribute("t", t);
    	%>
    	<!-- 通过EL表达式输出Teacher对象中的name属性值 -->
    	通过EL表达式输出Teacher对象中的name属性值：${requestScope.t.name }<br>
    	通过getGender()方法获取方法的返回值：${requestScope.t.gender }<br>
    	通过EL表达式获取Teacher对象中的stu属性中的name属性值：${requestScope.t.stu.name }

2.EL中的11个隐含对象
	一个我们比较熟悉的
		pageContext
			类型：PageContex
				它既是JSP的隐含对象，也是EL的隐含对象
			作用：通过它可以获取JSP中其他8个隐含对象
				通过EL表达式中获取request对象
            		${pageContext.request }
				通过EL表达式获取项目的虚拟路径
            		${pageContext.request.contextPath }
	四个Scope对象
		pageScope
			类型：Map<String , Object>
			作用：获取page域中的属性值
		requestScope
			类型：Map<String , Object>
			作用：获取request域中的属性值
		sessionScope
			类型：Map<String , Object>
			作用：获取session域中的属性值
		applicationScope
			类型：Map<String , Object>
			作用：获取application域中的属性值
	其他六个隐含对象
		param
			类型：Map<String , String>
			作用：获取请求参数
		paramValues
			类型：Map<String , String[]>
			作用：获取请求参数中一个键对应多个值的情况
		header
			类型：Map<String , String>
			作用：获取请求头中的信息
		headerValues
			类型：Map<String , String[]>
			作用：获取请求头中一个键对应多个值的情况
		cookie
			类型：Map<String , Cookie>
			根据Cookie对象的名字获取对应的Cookie对象
		initParam
			类型：Map<String , String>
			作用：获取当前Web应用的初始化参数
                
3.EL中的运算
	在EL表达式中可以直接进行加、减、乘、除等运算
	在EL中有一个我们常用的运算符：empty 😀 
	我们通常通过empty运算符来判断一个字符串或者一个集合是否为空
	empty与null的区别 😀
		空串时：null返回false;empty返回true
		空集合时：null返回false；empty返回true
		非空使用!empty或者not empty表示
```



