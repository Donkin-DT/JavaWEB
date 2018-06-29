###### 第七章 JSTL

```html
1.JSTL简介
	全称：JSP Standard Tag Library，翻译过来叫JSP的标准标签

2.标签库
	c：核心标签库，我们又称为c标签
	fn：函数标签库，需要结合EL表达式使用，里面定义了一些对字符串的操作（对字符串的截取、替换等）
	fmt：格式化标签库，主要用来对日期、时间、数字进行国际化的操作

3.核心标签库
	使用标签库需要导入以下jar包😀
    	taglibs-standard-impl-1.2.5.jar
    	taglibs-standard-spec-1.2.5.jar
	使用标签需要通过taglib指令将标签导入到页面中
	<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>😀
	常用的标签
		set标签
		<!-- set标签：用来向域中添加属性，默认添加到page域中 -->
    	<!--
        	var：用来设置向域中添加属性的属性名
        	value：用来设置向域中添加属性的属性值
        	scope：用来设置将属性添加到那个域中，可选值有page、request、session、application
     	-->
    	<c:set var="hello" value="JSTL" scope="request"></c:set>
    		page域中的属性值是：${pageScope.hello }<br>
    		request域中的属性值是：${requestScope.hello }<br>
    		session域中的属性值是：${sessionScope.hello }<br>
    		application域中的属性值是：${applicationScope.hello }<br>
		remove标签
		<hr>
    	<!-- 向其他三个域中也分别添加一个属性 -->
    		<c:set var="hello" value="JSTL" scope="page"></c:set>
    		<c:set var="hello" value="JSTL" scope="session"></c:set>
    		<c:set var="hello" value="JSTL" scope="application"></c:set>
    	<!-- remove标签：用来移除域中的属性，默认全域移除 -->
    	<!--
        	var：用来设置要移除的域中的属性名
        	scope：用来设置要移除那个域中的属性，可选值有page、request、session、application
     	-->
    	<c:remove var="hello" scope="page"/>
    		page域中的属性值是：${pageScope.hello }<br>
    		request域中的属性值是：${requestScope.hello }<br>
    		session域中的属性值是：${sessionScope.hello }<br>
    		application域中的属性值是：${applicationScope.hello }<br>
		if标签 😀
		<!-- if标签：相当于Java中的if条件判断 -->
    	<!-- test：用来接收一个布尔类型的值，当值为true时才执行标签体中的内容 -->
    		<c:if test="${empty param.username }">
        	请输入用户名：
    		</c:if>
    		<c:if test="${not empty param.username }">
        		欢迎您，${param.username }
    		</c:if>
		choose标签
		<%
        	int age = 12;
        	//将年龄放到page域中
        	pageContext.setAttribute("age", age);
    	%>
		<!-- choose标签：相当于Java中的if...else if...else... -->
		<!-- when标签需要作为choose的子标签来使用，只要有一个条件满足将不再执行下面的，所以一定要注意多个when标签中条件的先后顺序 -->
    		<c:choose>
        		<c:when test="${age > 30 }">
            		大龄剩女
        	</c:when>
        	<c:when test="${age > 20 }">
            	青春靓女
        	</c:when>
        	<c:when test="${age > 16 }">
            	豆蔻年华
        	</c:when>
        	<c:when test="${age > 14 }">
            	这是一个界限
        	</c:when>
        	<c:otherwise>
            	小屁孩儿
        	</c:otherwise>
    	</c:choose>
		forEach标签😀
		<!-- forEach标签：相当于Java中的for循环 -->
    	<!--
        	begin:设置循环的开始，该值必须是一个大于等于0的数，否则会抛出异常
        	end：设置循环的结束
        	var：设置一个变量来接收遍历到的数，并且会以该变量值为key放到page域中
        	step：设置步长，默认值是1
     	-->
    	<c:forEach begin="1" end="20" var="index" step="1">
        <a href="#">${pageScope.index }</a>
    	</c:forEach>
    	<hr>
    	<%
        	List list = new ArrayList();
        	list.add("马蓉");
        	list.add("白百何");
        	list.add("陈思诚");
        	list.add("林丹");
        	list.add("李小璐");
        	list.add("文章");
        	//将list放到page域中
        	pageContext.setAttribute("stars", list);
    	%>
    
    	<!-- items：设置一个要遍历的集合 -->
    	<c:forEach items="${pageScope.stars }" var="star">
        	<a href="#">${star }</a>
		</c:forEach>
```

