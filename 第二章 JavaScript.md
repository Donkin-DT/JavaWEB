###### 第二章 JavaScript

```html
1.变量 😀	
	在JavaScript中通过var关键字声明一个变量，在使用变量的过程中可以给变量赋任意值
		var a; 
		a = 123;    
		a = "hello";   
		a = 'js';    
		a = true;    
		a = 对象;

2.函数 😀	
	在JavaScript中通过function关键字声明一个函数，在声明函数时不需要指定函数的返回值的类型和形参的类型
	//方式一：
		function fun(a , b){
		//函数体
		}

	//方式二：
		var fun2 = function(a , b , c){
    	//函数体
		}

	调用函数：
		函数名/函数的引用 + ()，在调用函数时不检查实参的类型及实参的个数
		在JavaScript中函数也是对象

3.事件 😀	
	声明一个函数：函数不执行
	将函数绑定到指定的控件上：函数也不执行
	触发控件的事件：函数才执行

	//声明一个函数：函数不执行
		function fun(){
    		alert("函数要执行了……");
		}

	//将函数绑定到元素的单击事件上：函数也不执行
		element.onclick = fun;

	//单机element元素之后：函数执行

4.嵌入方式
	1）写在标签的事件属性中：结构与行为相耦合，不建议使用
		<!-- 1.写到标签的事件属性中：结构与行为相耦合，不建议使用 -->
    	<button id="btnId" onclick="alert('Hello JS')">SayHello</button>

	2）写在script标签中，script标签放到head标签中：无法获取按钮对象
        <head>
        <meta charset="UTF-8">
        <title>load02</title>
        <!-- 2.写到script标签中，script标签放到head标签中：无法获取按钮对象 -->
        <script type="text/javascript">
            //1.获取按钮对象
            var btnEle = document.getElementById("btnId");
            alert(btnEle);
            //2.给按钮绑定单击事件
            btnEle.onclick = function(){
                //3.弹出提示框
                alert("Hello JS");
            };
        </script>
        </head>

	3）写在script标签中，script标签放到body标签后面：可以获取到按钮对象，但是不符合我们的习惯
        <body>
            <button id="btnId">SayHello</button>
        </body>
        <!-- 3.写到script标签中，script标签放到body标签后面：不符合我们的习惯 -->
        <script type="text/javascript">
            //1.获取按钮对象
            var btnEle = document.getElementById("btnId");
            alert(btnEle);
            //2.给按钮绑定单击事件
            btnEle.onclick = function(){
                //3.弹出提示框
                alert("Hello JS");
            };
        </script>

	4）写在script标签中，script标签放到head标签中并且使用window.onload：符合我们的习惯而且也可以获取到按钮对象
        <!-- 4.使用window.onload：完美解决问题 -->
        <script type="text/javascript">
            window.onload = function(){
                //1.获取按钮对象
                var btnEle = document.getElementById("btnId");
                alert(btnEle);
                //2.给按钮绑定单击事件
                btnEle.onclick = function(){
                    //3.弹出提示框
                    alert("Hello JS");
                };
            };
        </script>
        </head>

5）引入外部的js文件，但是要注意外部的js文件中也需要使用window.onload
    <!-- 5.引入外部的js文件 --> 😀	
    <script type="text/javascript" src="script.js"></script>
    </head>

5.DOM操作 😀	
    根据id属性值得到唯一的一个元素节点对象
    	document.getElementById("id属性值");

    根据标签名得到一个节点数组
    	document.getElementsByTagName("标签名");

    根据name属性值得到一个节点数组
    	document.getElementsByName("name属性值");

    innerHTML：用来获取或设置成对出现的标签中起始位置到终止位置（包括HTML标签）的全部内容
    	对象.innerHTML：获取
    	对象.innerHTML = 新的内容：设置
```

