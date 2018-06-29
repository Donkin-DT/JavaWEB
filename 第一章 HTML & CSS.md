###### 第一章 HTML & CSS

```html

创建时间：	2018/2/6 8:46
更新时间：	2018/2/6 9:22
作者：	韩延兵

1.网页的组成
结构（HTML）：超文本标记语言
表现（CSS）：层叠样式表
行为（JavaScript）
一个良好的网页要求结构、表现、行为三者分离
2.HTML的基本语法
HTML中的标签分为成对出现的标签和自结束标签
标签不区分大小写，但建议小写
成对出现的标签必须正确关闭
标签可以嵌套，但不能交叉嵌套
属性必须有值且值必须加引号
注释不能嵌套
3.HTML中常用的标签
标题标签（一共6个）
<h1></h1> ~ <h6></h6>
div标签
<div>我是div标签，我主要用来布局，我默认要占用浏览器的一整行</div>
段落标签
<p>我是一个段落，我默认也要占用浏览器的一整行，而且前后要空一行</p>
转义字符（实体）
小于号：&lt;     大于号：&gt;   空格：&nbsp;    版权符号；&copy;
无序列表（主要用来做导航栏）
<ul>
    <li>网页</li>
    <li>新闻</li>
    <li>视频</li>
</ul>
4.插入图片
使用img标签向网页中插入一张图片
<img alt="" src="" />
    -alt属性：用来设置当图片无法显示时的描述性的文字
    -src属性：用来设置要引入的图片的路径
        -在相对路径中使用 ../ 返回上一级目录，返回多级目录使用多个 ../
5.超链接
使用a标签创建一个超链接
<a href="" target="">我是一个超链接</a>
    -href属性：用来设置要跳转的页面的路径
    -target属性：用来设置要跳转的页面在何处打开
        -_self:默认值，在当前标签页打开
        -_blank:在新的标签页打开
如果想要同样设置页面中所有的超链接在何处打开可以使用base标签
6.表格
掌握
<!-- 使用table标签创建一个表格 -->
    <table border="1">
        <!-- 表格中的行使用tr标签来表示 -->
        <tr>
            <!-- 表格中的表头使用th标签表示 -->
            <th>姓名</th>
            <th>阵营</th>
            <th>职业</th>
            <th>武器</th>
        </tr>
        <tr>
            <!-- 每行中的列（单元格）使用td表示 -->
            <td>刘备</td>
            <!-- 跨行合并单元格使用rowspan属性 -->
            <td rowspan="4" align="center">蜀</td>
            <td>蜀汉集团董事长</td>
            <td>双股剑</td>
        </tr>
        <tr>
            <!-- 每行中的列（单元格）使用td表示 -->
            <td>诸葛亮</td>
<!--            <td>蜀</td> -->
            <!-- 跨列合并单元格使用colspan属性 -->
            <td colspan="2" align="center">蜀汉集团CEO</td>
<!--            <td>羽扇</td> -->
        </tr>
        <tr>
            <!-- 每行中的列（单元格）使用td表示 -->
            <td>关羽</td>
<!--            <td>蜀</td> -->
            <td>荆襄总裁</td>
            <td>青龙偃月刀</td>
        </tr>
        <tr>
            <!-- 每行中的列（单元格）使用td表示 -->
            <td>张飞</td>
<!--            <td>蜀</td> -->
            <td>阆中销售经理</td>
            <td>丈八蛇矛</td>
        </tr>
    </table>
7.表单
必须掌握
<!-- 使用form标签来创建一个表单 -->
    <!-- action属性：用来设置服务器的地址 -->
    <!-- method属性：用来设置请求方式
            get：默认值，发送的是一个GET请求，此时表单中的数据会显示到地址栏中
            post：发送的是一个POST请求，此时表单中的数据不会在地址栏中显示，而是通过请求体将数据发送到服务器
     -->
    <form action="success.html" method="post">
        <!-- 表单中的表单项使用input标签来表示，不同的表单项通过input中的type属性来指定 -->
        <!--
            1.必须为每一个表单项设置name属性值，name属性值可以任意指定
            2.用户输入的数据通过name属性值进行携带，并以键值对的形式发送到服务器，多个键值对之间通过 & 符号进行分割
                    如：username=admin&pwd=123456
         -->
        用户名：<input type="text" name="username"><br>
        密码：<input type="password" name="pwd"><br>
        <!--
            1.要保证单选按钮单选，必须将它们分为一组，即将它们的name属性值设置为同一个值
            2.单选按钮提交的是value属性值，所以必须设置value属性值
            3.通过属性checked="checked"设置默认被选中
         -->
        性别：<input type="radio" name="gender" value="man">男
            <input type="radio" name="gender" value="woman" checked="checked">女<br>
        <!--
            1.必须将所用的复选框分为一组，即将它们的name属性值设置为同一个值
            2.复选框提交的也是value属性值，所以必须设置value属性值
            3.通过属性checked="checked"设置默认被选中
         -->
        你的爱好：
            <input type="checkbox" name="hobby" value="basketball" checked="checked">篮球
            <input type="checkbox" name="hobby" value="football">足球
            <input type="checkbox" name="hobby" value="pingpang">乒乓球<br>
        你喜欢的女明星：
            <select name="star">
                <option>林志玲</option>
                <option>林青霞</option>
                <option>贾静雯</option>
                <!-- 通过属性selected="selected"设置默认被选中 -->
                <option selected="selected">迪丽热巴</option>
                <option>小泽玛利亚</option>
                <!-- 如果option中没有指定value属性值，提交的是option中的文本值
                       如果option中指定了value属性值，提交的是value属性值
                 -->
                <option value="xxoo">苍井空</option>
                <option>吉泽明步</option>
                <option value="ppp">波多野结衣</option>
            </select><br>
        <!-- 重置按钮 -->    
        <input type="reset">
        <input type="submit">
    </form>
8.CSS的基本语法
CSS由选择器和声明组成，声明由属性和值组成。属性和值之间使用冒号分割；多个属性之间使用分号分割。
    p{
        color: green;
        font-size: 60px
    }
添加CSS样式的方式：
1）写在标签的style属性中：结构与表现相耦合，不建议使用
<!-- 1.写在标签的style属性中：结构与表现相耦合，不建议使用 -->
    <!-- 字体的大小使用像素px表示 -->
    <p style="color: red;font-size: 50px">师傅领进门，修行在个人</p>
2）写在style标签中：开发环境中使用
<!-- 2.写到style标签中：开发环境时使用 -->
<style type="text/css">
    p{
        color: green;
        font-size: 60px
    }
</style>
3）引入外部的css文件：生成环境中使用
<!-- 3.使用link标签引入外部的css文件中的样式：生产环境中使用 -->
<link rel="stylesheet" type="text/css" href="css.css">
CSS中的基本选择器
标签选择器：即HTML标签
p{color:red}
    -将p标签中的内容的颜色设置为红色  
ID选择器：#id属性值
#p1{color:green}
    -将id属性值为p1的标签中的内容设置为绿色
类选择器：.class属性值
.p2{color:blue}
    -将class属性值为p2的标签中的内容设置为蓝色
分组选择器：将各个选择器中间使用逗号分隔，然后统一设置样式
p,#p1,.p2{font-size:60px}
    -将段落，id属性值为p1,class属性值为p2的标签中的内容的字体大小设置为60像素
CSS中颜色的表示方式
1）使用英语单词
红色：red
2）使用RGB值
红色：rgb(255,0,0)
3）使用十六进制数
红色：#FF0000=#ff0000=#F00=#f00
```