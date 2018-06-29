###### 第十二章 Ajax

```java
1.Ajax简介
    Asynchronous JavaScript And Xml，翻译过来叫异步的JavaScript和Xml
    JavaScript用来发送请求；Xml作为一种响应数据
    Ajax主要就是用来增强用户体验的
    
2.异步和同步的区别 😀
    同步请求
    	当我们向服务器发送请求时，必须等到响应成功之后才能发送其他请求，有一个等待的过程，而且响应成功之后刷新整个页面
    	
    异步请求
    	当我们向服务器发送请求时，不需要等到响应成功就可以发送其他请求，没有等待的过程，而且响应成功之后局部刷新页面
    	
3.通过JavaScript发送Ajax请求
    1）创建XMLHttpRequest对象
        Ajax的一切操作都由该对象完成
        //1.创建XMLHttpRequest对象
         var xhr = new XMLHttpRequest();

    2）设置请求信息
      //2.设置请求信息
      /*open(method,url,async)
        method参数：设置请求方式，GET或者POST
        url参数：设置请求地址
        async参数：设置该请求是一个异步请求还是同步请求，默认是true，发送的是一个异步请求，一般不改
        */
        xhr.open("GET","${pageContext.request.contextPath}/AjaxServlet");

    3）发送请求
    	GET请求
        //3.发送请求
        /*send(Object body)
          send方法中传入一个请求体，由于GET请求没有请求体，所以可以不传
          */
          xhr.send();

    	POST请求
    	//3.发送请求
        //POST请求在发送请求前需要设置一个请求头对请求体中的数据进行URL编码
          xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
          xhr.send("username=admin&password=123456");

    4）接收响应
    	响应数据是字符串
    	//4.接收响应
         //给xhr绑定onreadystatechange事件
         	xhr.onreadystatechange = function(){
         	//当xhr的readState的值为4时再接收响应数据
         		if(xhr.readyState == 4 && xhr.status == 200){
                    //接收响应数据
                        var text = xhr.responseText;
                    //获取显示响应信息的span元素
                        var spanEle = document.getElementById("msg");
                    //将响应信息设置到span元素中
                        spanEle.innerHTML = text;
                 }
             };

    	响应数据是Xml
		//给xhr绑定onreadystatechange事件
         	xhr.onreadystatechange = function(){
            //当xhr的readState的值为4时再接收响应数据
                if(xhr.readyState == 4 && xhr.status == 200){
                    //接收响应数据
                    var xmlDoc = xhr.responseXML;
                    //获取name元素节点
                    var nameEle = xmlDoc.getElementsByTagName("name")[0];
                    //获取name元素节点的子节点文本节点
                    var textNode = nameEle.firstChild;
                    //获取文本节点的节点值
                    var text = textNode.nodeValue;
                    //获取显示响应信息的span元素
                    var spanEle = document.getElementById("msg2");
                    //将响应信息设置到span元素中
                    spanEle.innerHTML = text;
                }
            };
        };

4.JSON简介
	全称：JavaScript Object Notation，翻译过来叫JavaScript的对象表示法，是一种轻量级的数据交换格式
		JSON是一种跨平台、跨语言的数据交换格式 😀
		由于XML的响应数据解析复杂、性能差，现在基本已经被JSON所替代
		
	XML格式的数据：
        <student>
            <name>章登</name>
            <age>22</age>
        </student>
        
    JSON格式的数据：
        {"name":"章登","age":22}

	JSON格式：😀
		JSON对象
			{"属性名1":属性值,"属性名2":属性值2,"属性名3":属性值3}
			属性名必须使用双引号括起来；属性名和属性值之间使用冒号分隔；多个属性之间使用逗号分隔 😀
			
		JSON数组
			[属性值1,属性值2,属性值3]
			多个属性值之间使用逗号分隔
			
    JSON中属性值能接受的类型 😀
        字符串
        数字
        null
        布尔类型
        数组
        对象
        
    //创建JSON对象
    	var jsonObj = {"name":"唐僧","age":18};
    //JSON格式的字符串（JSON字符串）
    	var jsonStr = '{"name":"江流儿","age":8}';
    //JSON数组
    	var jsonArray = [1,null,jsonObj,false];
    //稍微复杂的JSON对象
    	var fzJsonObj = {"name":"金蝉子",
                     	"age":18,
                     	"sons":[
                             {"name":"孙悟空","age":520},
                             {"name":"小白龙","age":5201314},
                             {"name":"猪八戒","age":5211314,"wives":[
                                                                    {"name":"嫦娥","age":13141314},
                                                                    {"name":"高翠兰","age":16},
                                                                    {"name":"秀琴","age":18}
                                                                  ]},
                             {"name":"沙悟净","age":18}
                            ]
                    };
    //获取猪八戒的第二个夫人的年龄
		alert(fzJsonObj.sons[2].wives[1].age);

	JSON对象与JSON字符串之间的转换 😀
	//将JSON对象转换为JOSN字符串
    	var objToStr = JSON.stringify(jsonObj);

    //将JSON字符串转换为JSON对象
    	var strToObj = JSON.parse(jsonStr);

	对象与JSON字符串之间的转换 😀
        @Test
        void testObj() {
            //创建Student对象
            Student student = new Student(1, "章登", 22);
            //创建Gson对象
            Gson gson = new Gson();
            //将Student对象转换我JSON字符串
            String json = gson.toJson(student);
            System.out.println(json);
            //将JSON字符串转换为Student对象
            Student fromJson = gson.fromJson(json, Student.class);
            System.out.println(fromJson);
        }
    
        @Test
        void testList() {
            //创建List<Student>
            List<Student> list = new ArrayList<>();
            list.add(new Student(1, "刘备", 35));
            list.add(new Student(2, "关羽", 30));
            list.add(new Student(3, "张飞", 25));
            list.add(new Student(4, "赵云", 20));
            list.add(new Student(5, "黄忠", 45));
            list.add(new Student(6, "马超", 20));
        
            //创建Gson对象
            Gson gson = new Gson();
            //将List转换为JSON字符串
            String json = gson.toJson(list);
            System.out.println(json);
        }
        @Test
        void testMap() {
            Map<String , Student> map = new HashMap<>();
            map.put("stu01", new Student(1, "晁盖", 40));
            map.put("stu02", new Student(2, "宋江", 50));
            map.put("stu03", new Student(3, "卢俊义", 45));
            map.put("stu04", new Student(4, "吴用", 40));
            map.put("stu05", new Student(5, "林冲", 35));

            //创建Gson对象
            Gson gson = new Gson();
            //将Map转换为JSON字符串
            String json = gson.toJson(map);
            System.out.println(json);
        }

5.通过jQuery发送Ajax请求 😀
	通过$.ajax()方法发送Ajax请求 
		//给按钮绑定单击事件 😀
        $("#btnId").click(function(){
            //通过jQuery发送Ajax的GET请求（响应数据是文本）
            /*
                url：用来设置请求地址，默认发送是一个GET请求
                type：用来设置请求方式，GET或POST，如果不指定type属性，默认是GET请求
                data：用来设置要携带的请求参数，值可以是JSON对象
                success：用来设置一个回调函数，当响应成功之后系统会调用该函数，并且响应数据会以参数的形式传入到该函数中
                dataType：用来设置响应数据的类型，text或者json，默认是text
            */
            $.ajax({
                url:"${pageContext.request.contextPath}/JQueryServlet",
                type:"GET",
                data:{"username":"admin","password":123456},
                success:function(res){
                    //弹出响应数据
                    alert(res);
                },
                dataType:"text"
            });
        });

        //给按钮绑定单击事件 😀
        $("#btnId2").click(function(){
            //通过jQuery发送Ajax的GET请求（响应数据是文本）
            /*
                url：用来设置请求地址，默认发送是一个GET请求
                type：用来设置请求方式，GET或POST，如果不指定type属性，默认是GET请求
                data：用来设置要携带的请求参数，值可以是JSON对象
                success：用来设置一个回调函数，当响应成功之后系统会调用该函数，并且响应数据会以参数的形式传入到该函数中
                dataType：用来设置响应数据的类型，text或者json，默认是text
            */
            $.ajax({
                url:"${pageContext.request.contextPath}/JQueryServlet",
                type:"POST",
                data:{"username":"admin","password":123456},
                success:function(res){
                    //弹出响应数据
                    alert(res.id+"--"+res.name+"--"+res.age);
                },
                dataType:"json"
            });
        });

    通过$.get()发送Ajax请求 😀
    	$("#btnId3").click(function(){
                //通过jQuery的$.get()方法发送Ajax的GET请求（响应数据是文本）
                /*
                        $.get(url, [data], [callback], [type])
                        url：必须的。用来设置请求地址
                        data：可选的。用来设置请求参数
                        callback：可选的。用来设置一个回调函数，响应成功之后系统会调用该函数并且响应数据会以参数的形式传入到该函数中
                        type：可选的。用来设置响应数据的类型，text、json等，默认是text。
                */
                //设置请求地址
                var url = "${pageContext.request.contextPath}/JQueryServlet";
                //设置请参数
                var params = {"username":"admin","password":123456};
                //设置回调函数
                var fun = function(res){
                    alert(res);
                }
                //设置响应数据的类型
                var type = "text";
                $.get(url,params,fun,type);
            });

    通过$.post()发送Ajax请求 😀
    	$("#btnId4").click(function(){
                //通过jQuery的$.post()方法发送Ajax的POST请求（响应数据是JSON）
                /*
                    $.post(url, [data], [callback], [type])
                        url：必须的。用来设置请求地址
                        data：可选的。用来设置请求参数
                        callback：可选的。用来设置一个回调函数，响应成功之后系统会调用该函数并且响应数据会以参数的形式传入到该函数中
                        type：可选的。用来设置响应数据的类型，text、json等，默认是text。
                */
                //设置请求地址
                var url = "${pageContext.request.contextPath}/JQueryServlet";
                //设置请参数
                var params = {"username":"admin","password":123456};
                $.post(url,params,function(res){
                    alert(res.id+"--"+res.name+"--"+res.age);
                },"json");
            });

    😀 另外，通过$.getJSON()方法发送的Ajax请求也是一个GET请求，而且默认接收的响应数据是JSON格式的响应数据
```

