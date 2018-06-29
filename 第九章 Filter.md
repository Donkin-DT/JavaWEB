###### 第9章 Filter

```java
1.Filter简介
	Filter翻译过来叫过滤器，是服务器端的三大组件之一，用来过滤请求
	服务器端的三大组件：Servlet、Filter、Listener 😀
	
	服务器端的三大组件都有以下特点：😀
		1）都需要运行在服务器上
		2）都需要实现某个接口
		3）都需要在web.xml中注册
		
	创建Filter的HelloWorld的步骤：😀
	1）创建一个类实现Filter
	public class HelloFilter implements Filter {
    	@Override
    	public void init(FilterConfig filterConfig) throws ServletException {
    	}
    	@Override
		public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
            throws IOException, ServletException {
    }
    	@Override
    	public void destroy() {
    	}
	}
	
	2）在web.xml中注册Filter
	<!-- 注册Filter -->
  	<filter>
    	<filter-name>HelloFilter</filter-name>
      	<filter-class>com.atguigu.filter.HelloFilter</filter-class>
    </filter>
  	<!-- 映射Filter -->
  	<filter-mapping>
    	<filter-name>HelloFilter</filter-name>
    	<!-- 映射要拦截的请求地址 -->
    	<url-pattern>/index.jsp</url-pattern>
  </filter-mapping>
  
	3）在浏览器中访问index.jsp则会调用HelloFilter的doFilter方法来拦截请求
	@Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
            throws IOException, ServletException {
        System.out.println("你的请求已经被我拦截……");
    }

	4）如果满足要求，可以在doFilter方法中通过chain.doFilter(request, response)放行请求
	@Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
            throws IOException, ServletException {
        System.out.println("你的请求已经被我拦截……");
        //放行请求
        chain.doFilter(request, response);
    }

过滤器的作用 😀
    1）请求到达目标资源之前拦截请求
    2）放行请求
    3）在响应到达浏览器之前做一些其他的操作
    
2.Filter的生命周期
	Filter的生命周期即Filter对象从被创建到被销毁的过程
	Filter的生命周期主要体现在以下方法中
	构造器
	服务器一启动就被调用，说明服务器一启动就创建了Filter对象
	在整个生命周期过程中只被调用一次，说明Filter也是单例的
	
	init()
        服务器一启动就被调用，对Filter对象进行初始化
        在整个生命周期过程中只被调用一次
        该方法中的参数FilterConfig filterConfig的作用
        1）获取Filter的名称
        2）获取Filter的初始化参数
        3）获取ServletContext对象
	doFilter()
        每次发送请求都会被调用，用来拦截请求
        在整个生命周期过程中会被调用多次
        该方法中三个参数ServletRequest request, ServletResponse  response, FilterChain chain的作用
        request和response和Servlet中的作用一样
        chain就是用来放行请求的
	destroy()
        服务器关闭时被调用，用来销毁Filter对象
        在整个生命周期过程中只被调用一次
        
3.多个Filter的执行顺序 😀
    我们可以为同一个资源设置多个Filter，多个Filte组成一个Filter链，多个Filter的执行顺序由web.xml中的filter-mapping标签来决定，在前的先拦截，在后的后拦截
     <filter>
          <filter-name>RobFilter</filter-name>
          <filter-class>com.atguigu.filter.RobFilter</filter-class>
      </filter>
      <filter>
        <filter-name>RobFilter2</filter-name>
          <filter-class>com.atguigu.filter.RobFilter2</filter-class>
       </filter>

      <filter-mapping>
        <filter-name>RobFilter2</filter-name>
        <url-pattern>/rob.jsp</url-pattern>
      </filter-mapping>
      <filter-mapping>
        <filter-name>RobFilter</filter-name>
        <url-pattern>/rob.jsp</url-pattern>
      </filter-mapping>
      
4.url-pattern的配置规则
	精确匹配
	设置一个完整的路径
	例如：<url-pattern>/index.jsp</url-pattern>
	只有访问index.jsp时才会拦截请求
	我们也可以通过servlet-name标签来配置拦截的路径
	例如：<servlet-name>UserServlet</servlet-name>
	拦截向UserServlet发送的请求
	模糊匹配
	前缀匹配
		例如：<url-pattern>/pages/*</url-pattern>
	只要访问pages目录下的资源都会被拦截
	后缀匹配
		例如：<url-pattern>*.jsp</url-pattern>
	只要访问jsp页面都会被拦截
	注意：以下配置方式是无效的
		<url-pattern>/pages/*.jsp</url-pattern
```
