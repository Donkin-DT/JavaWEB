###### 第十章 Listener

```java
1.Listener简介
	Listener翻译过来叫监听器，是服务器端的三大组件之一
	服务器端的三大组件：Servlet、Filter、Listener
	服务器端三大组件的特点：
        它们都需要运行在服务器上
        它们都需要实现某个接口
        它们都需要在web.xml中注册
        
    生活中的监听器
        监听器：朝阳群众
        监听的对象：明星
        监听的事件：干坏事
        回调函数：报警
        
    JavaWeb中的监听器
        监听器：自己创建
        监听的对象：ServletRequest、HttpSession、ServletContext
        监听的事件：生命周期的变化、属性的变化
        回调函数：自己声明
        
2.监听的分类
    监听器分为三大类八种（八个）😀
        生命周期监听器（3个）
        属性变化监听器（3个）
        session域中的属性变化监听器（2个）
        
    生命周期监听器
    ServletRequest的生命周期监听器
    ServletRequestListener
    方法：
        void	
        requestDestroyed(ServletRequestEvent sre)
           -ServletRequest对象被销毁时调用
         void	
        requestInitialized(ServletRequestEvent sre)
            -ServletRequest对象被创建时调用
            参数sre的作用
            获取ServletRequest对象
                                ServletRequest servletRequest = sre.getServletRequest();
            获取ServletContext对象
                                ServletContext servletContext = sre.getServletContext();

    HttpSession的生命周期监听器
        HttpSessionListener
        方法：
            void	
            sessionCreated(HttpSessionEvent se)
               -HttpSession对象被创建时调用
             void	
            sessionDestroyed(HttpSessionEvent se)
                -HttpSession对象被销毁时调用
            参数se的作用
            获取HttpSession对象
            
    ServletContext的生命周期监听器 😀
        ★ServletContextListener
        方法：
            void	
            contextDestroyed(ServletContextEvent sce)
               -ServletContext对象被销毁时调用
             void	
            contextInitialized(ServletContextEvent sce)
                -ServletContext对象被创建调用
            参数sce的作用
            获取ServletContext对象
            
    属性变化监听器
        属性的变化值
        属性的添加
        属性的替换
        属性的移除
        ServletRequest的属性变化监听器
        ServletRequestAttributeListener
        方法：
             void	
            attributeAdded(ServletRequestAttributeEvent srae)
                -向request域中添加属性时调用
             void	
            attributeRemoved(ServletRequestAttributeEvent srae)
                -将request域中的属性移除时调用
             void	
            attributeReplaced(ServletRequestAttributeEvent srae)
                -request域中的属性被替换时调用
                参数srae的作用
                获取属性名
                获取属性值
                获取ServletRequest对象
                获取ServletContext对象
                
        HttpSession的属性变化监听器
        HttpSessionAttributeListener
        方法：
        void	
        attributeAdded(HttpSessionBindingEvent se)
            -向session域中添加属性时调用
         void	
        attributeRemoved(HttpSessionBindingEvent se)
             -将session域中的属性移除时调用
         void	
        attributeReplaced(HttpSessionBindingEvent se)
             -session域中的属性被替换时调用
            参数se的作用
                获取属性名
                 //获取属性名
                 String name = se.getName();
                获取属性值
                         //获取属性值
                         Object value = se.getValue();
                         System.out.println("session域中的属性名是："+name);
                         System.out.println("session域中的被替换之前的属性值是："+value);
                获取HttpSession对象
                         //获取session域中被替换之后的属性值
                         //获取Session对象
                         HttpSession session = se.getSession();
                         Object newValue = session.getAttribute("user");
                         System.out.println("session域中的被替换之后的属性值是："+newValue);

        ServletContext的属性变化监听器
        ServletContextAttributeListener
        方法：
            void	
            attributeAdded(ServletContextAttributeEvent scab)
               -向application域中添加时调用
             void	
            attributeRemoved(ServletContextAttributeEvent scab)
               -将application域中的属性移除时调用
             void	
            attributeReplaced(ServletContextAttributeEvent scab)
                -application域中的属性被替换时调用
                参数scab的作用
                    获取属性名
                    获取属性值
                    获取ServletContext对象
                    
        session域中的属性变化监听器
        通过以下两个接口创建的监听器不需要在web.xml中注册
        以下两个接口是由JavaBean来实现，然后JavaBean实例下session域中的变化将会被自动监听
        HttpSessionBindingListener
        用来监听JavaBean实例在session域中的添加和移除
        方法：
            void	
            valueBound(HttpSessionBindingEvent event)
                -JavaBean实现被添加到session域中时调用
             void	
            valueUnbound(HttpSessionBindingEvent event)
                -JavaBean实例从session域中移除时调用
                参数event的作用
                    获取属性名
                    获取属性值
                    获取HttpSession对象
                    
        HttpSessionActivationListener
        用来监听Session与session域中的JavaBean实例的活化和钝化
        方法：
             void	
            sessionDidActivate(HttpSessionEvent se)
                -JavaBean实例与Session对象活化时调用
             void	
            sessionWillPassivate(HttpSessionEvent se)
                 -JavaBean实例与Session对象钝化时调用
                参数se的作用
               		获取HttpSession对象
```

