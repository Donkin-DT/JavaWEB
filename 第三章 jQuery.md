###### 第三章 jQuery

```html
1.四个核心函数的作用 😀
	$(function(){})
		当整个文档加载完成之后再执行函数中的内容
	
	$("选择器字符串")
		根据选择器字符串获取元素节点对象

	$("html字符串")
		根据html字符串创建元素节点对象

	$(DOM对象)
		将DOM对象转换为jQuery对象

2.DOM对象与jQuer对象之间的转换 😀
	DOM对象转jQuery对象：
		用核心函数进行包装
		例如：var $btnEle = $(btnEle);

	jQuery对象转DOM对象：
		使用数组下标
		例如：var btnEle = $btnEle[0];

3.选择器 😀
	基本选择器 😀
		id选择器：
			#id属性值

		类选择器：
			.class属性值

		元素选择器：
			html标签

		获取所有的元素：
			*符号

		分组选择器：
			将各个选择器之间使用逗号分隔

	层级选择器：😀
		获取后代元素：
			空格

		获取子元素：
			>

		获取后面紧邻的兄弟：
			+

		获取后面所有的兄弟：
			~

	基本过滤选择器 😀
		:first
			获取第一个元素

		:last
			获取最后一个元素

		:not(selector)
            获取不含有某些元素的元素

		:even
			获取索引值为偶数的元素，索引从0开始

		:odd
			获取索引值为奇数的元素

		:eq(index)
			获取索引值为某个值的元素，索引从0开始

		:gt(index)
			获取索引值大于某个值的元素

		:lt(index)
			获取索引值小于某个值的元素

	内容过滤选择器 😀
		:contains(text)
			获取包含某个文本的元素

		:has(selector)
			获取含有某些元素的元素

		:empty
			获取没有子元素或文本的元素

		:parent
			获取含有子元素或者文本的元素

	可见性过滤选择器 😀
		:hidden
			获取不可见的元素
			不可见有两种情况：
				①元素的display属性值为none②input元素中的type属性值为hidden（隐藏域）

		:visible
			获取可见的元素

	表单对象属性过滤选择器 😀
		:enabled
			获取可用的元素

		:disabled
			获取不可用的元素

		:checked
			获取选中的单选按钮或复选框

		:selected
			获取下拉列表中选中的option

4.常用方法
	each()
		用来遍历元素

	attr() 😀
		获取或设置元素的属性值
			对象.attr("属性名")：获取属性值
			对象.attr("属性名","属性值")：设置属性值
			对象.attr({"属性名1":"属性值1","属性名2":"属性值2"})：设置多个属性值

	css()方法跟attr()类似

	text()
		获取或设置成对出现的标签中的文本值
			对象.text()：获取文本值
			对象.text("新值")：设置文本值

	html()也可以实现text()方法能实现的功能，但是html()方法还可以解析html标签 😀

	val() 😀
		获取或设置元素的value属性值
			对象.val()：获取value属性值
			对象.val("新值")：设置value属性值

	append()
		向元素中追加内容

	remove()
		删除元素对象

	children()
		获取子元素

	find()
		获取后代元素

	parent()
		获取父元素

	parents()
		获取祖先元素

5.常用的事件
	click()
		单击事件

	change()
		元素中的内容改变的事件
```



