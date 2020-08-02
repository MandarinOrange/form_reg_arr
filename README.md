# form_reg_arr
表单验证、正则表达式、数组使用示例

# 字符串的使用
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020080221222395.png)
字符串常用方法：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200802212247868.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N0YXJfb2Zfc2NpZW5jZQ==,size_16,color_FFFFFF,t_70)

Substr(index,length)：字符串截取方法，index表示从哪个索引位置开始截取，length表示截取多少个字符

# 为什么要使用表单验证
在登录、注册页面中经常会用到表单，用户可以输入相关信息，然后提交表单到服务器处理，但是在用户输入的信息中往往会有一些不符合要求，这时候这些无意义的数据提交给服务器只是增加服务器的压力，所以我们引入表单基本验证，使用JavaScript验证用户输入的信息，如果不符合要求就不提交，只有输入的信息正确时才将表单提交给服务器处理。

# 表单验证的常用步骤
1、创建一个函数
2、在函数中对表单数据进行验证
3、如果数据验证都成功，函数返回true，否则返回false
4、表单中加上onsubmit事件，例如：onsubmit="return check()"  其中check就是函数名

# 提交表单的2种方式
1、点击type=”submit”的按钮可以提交表单(该提交方式会触发表单的onsubmit事件)，例如：
    <input  type="submit" value="注册"/>
2、在JavaScript代码中调用表单的submit()方法也可以提交表单(该提交方式不会触发表单的onsubmit事件)，例如：
    document.表单名称.submit(); 或 document.getElementById("表单id").submit();

注册表单验证：
```javascript
<script type="text/javascript">
        /*需求：
            邮箱：不能为空、必须包含@、必须包含. 最后一个.必须在@符号后面并且中间要有字符   a.bc@qq.com
            密码：不能为空、必须大于等于6位
            确认密码：二次密码要一致
            姓名：不能为空、不能包含数字    张三123  charAt(i)
         */
        //验证邮箱
        function checkEmail(){
            var email = document.getElementById("email").value;//获取邮箱文本框中的字符串
            if(email.length == 0){
                alert("email不能为空！");
                return false;
            }else if(email.indexOf("@")<0){
                alert("email中必须包含@符号！");
                return false;
            }else if(email.indexOf(".")<0){
                alert("email中必须包含.符号！");
                return false;
            }else if(email.lastIndexOf(".")-email.indexOf("@")<=1){
                alert("最后一个.必须在@符号后面并且中间要有字符");
                return false;
            }
            return true;
        }
        //验证密码
        function checkPwd(){
            var pwd = document.getElementById("pwd").value;//获取密码文本框的值
            if(pwd.length == 0){
                alert("密码不能为空！");
                return false;
            }else if(pwd.length<6){
                alert("密码必须大于等于6位！");
                return false;
            }
            return true;
        }
        //验证确认密码
        function checkConfirmPwd(){
            var pwd = document.getElementById("pwd").value;//密码
            var confirmPwd = document.getElementById("repwd").value;//确认密码
            if(pwd!=confirmPwd){
                alert("二次输入密码不一致！");
                return false;
            }
            return true;
        }
        //验证姓名
        function checkName(){
            var name = document.getElementById("user").value;//获取姓名文本框中的值
            if(name.length == 0){
                alert("姓名不能为空！");
                return false;
            }else{
                for(var i=0;i<name.length;i++){
                    var s = name.charAt(i);
                    if(!isNaN(s)){
                        alert("用户名不能包含数字！");
                        return false;
                    }
                }
            }
            return true;
        }
        //表单验证函数
        function checkForm(){
            if(checkEmail()&&checkPwd()&&checkConfirmPwd()&&checkName()){
                return true;
            }else{
                return false;
            }
        }

    </script>
```

# 文本框对象
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200802212410788.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N0YXJfb2Zfc2NpZW5jZQ==,size_16,color_FFFFFF,t_70)
制作文本框输入验证提示信息：

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
        "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=gb2312"/>
    <title>休闲网注册页面</title>
    <link href="login.css" rel="stylesheet" type="text/css">
    <script type="text/javascript">
        //验证邮箱
        function checkEmail(){
            var email = document.getElementById("email").value;//获取邮箱文本框中的字符串
            if(email.length == 0){
                document.getElementById("DivEmail").innerHTML = "email不能为空！";
                document.getElementById("email").style.borderColor = "red";
                return false;
            }else if(email.indexOf("@")<0){
                document.getElementById("DivEmail").innerHTML = "email中必须包含@符号！";
                document.getElementById("email").style.borderColor = "red";
                return false;
            }else if(email.indexOf(".")<0){
                document.getElementById("DivEmail").innerHTML = "email中必须包含.符号！";
                document.getElementById("email").style.borderColor = "red";
                return false;
            }else if(email.lastIndexOf(".")-email.indexOf("@")<=1){
                document.getElementById("DivEmail").innerHTML = "最后一个.必须在@符号后面并且中间要有字符!";
                document.getElementById("email").style.borderColor = "red";
                return false;
            }
            document.getElementById("DivEmail").innerHTML = "";
            document.getElementById("email").style.borderColor = "";
            return true;
        }
        //验证密码
        function checkPwd(){
            var pwd = document.getElementById("pwd").value;//获取密码文本框的值
            if(pwd.length == 0){
                document.getElementById("DivPwd").innerHTML = "密码不能为空！";
                document.getElementById("pwd").style.borderColor="red";
                return false;
            }else if(pwd.length<6){
                document.getElementById("DivPwd").innerHTML = "密码必须大于等于6位！";
                document.getElementById("pwd").style.borderColor="red";
                return false;
            }
            document.getElementById("DivPwd").innerHTML = "";
            document.getElementById("pwd").style.borderColor="";
            return true;
        }
        //验证确认密码
        function checkConfirmPwd(){
            var pwd = document.getElementById("pwd").value;//密码
            var confirmPwd = document.getElementById("repwd").value;//确认密码
            if(pwd!=confirmPwd){
                document.getElementById("DivRepwd").innerHTML="二次输入密码不一致！";
                document.getElementById("DivRepwd").style.borderColor = "red";
                return false;
            }
            document.getElementById("DivRepwd").innerHTML="";
            document.getElementById("DivRepwd").style.borderColor = "";
            return true;
        }
        //验证姓名
        function checkName(){
            var name = document.getElementById("user").value;//获取姓名文本框中的值
            if(name.length == 0){
                document.getElementById("DivUser").innerHTML = "姓名不能为空！";
                document.getElementById("user").style.borderColor = "red";
                return false;
            }else{
                for(var i=0;i<name.length;i++){
                    var s = name.charAt(i);
                    if(!isNaN(s)){
                        document.getElementById("DivUser").innerHTML = "用户名不能包含数字！";
                        document.getElementById("user").style.borderColor = "red";
                        return false;
                    }
                }
            }
            document.getElementById("DivUser").innerHTML = "";
            document.getElementById("user").style.borderColor = "";
            return true;
        }
        //表单验证函数
        function checkForm(){
            //&&(短路与)   &(逻辑与)
            if(checkEmail()&checkPwd()&checkConfirmPwd()&checkName()){
                return true;
            }else{
                return false;
            }
        }
    </script>
</head>

<body>
<div id="header" class="main">
    <div id="headerLeft"><img src="images/logo.gif"/></div>
    <div id="headerRight">注册 | 登录 | 帮助</div>
</div>
<div class="main">
    <table id="center" border="0" cellspacing="0" cellpadding="0">
        <tr>
            <td class="bold" colspan="2">注册休闲网</td>
        </tr>
        <form action="success.html" method="post" name="myform" onsubmit="return checkForm()">
            <tr>
                <td class="left">您的Email：</td>
                <td><input id="email" type="text" class="inputs" onblur="checkEmail()"/>

                    <div class="red" id="DivEmail"></div>
                </td>
            </tr>
            <tr>
                <td class="left">输入密码：</td>
                <td><input id="pwd" type="password" class="inputs" onblur="checkPwd()"/>

                    <div class="red" id="DivPwd"></div>
                </td>
            </tr>
            <tr>
                <td class="left">再输入一遍密码：</td>
                <td><input id="repwd" type="password" class="inputs" onblur="checkConfirmPwd()"/>

                    <div class="red" id="DivRepwd"></div>
                </td>
            </tr>
            <tr>
                <td class="left">您的姓名：</td>
                <td><input id="user" type="text" class="inputs" onblur="checkName()"/>

                    <div class="red" id="DivUser"></div>
                </td>
            </tr>
            <tr>
                <td class="left">性别：</td>
                <td><input name="sex" type="radio" value="1"/> 男
                    <input name="sex" type="radio" value="0"/> 女
                </td>
            </tr>
            <tr>
                <td class="left">出生日期：</td>
                <td><select name="year">
                    <script type="text/javascript">
                        for (var i = 1900; i <= 2009; i++) {
                            document.write("<option value=" + i + ">" + i + "</option>");
                        }
                    </script>
                </select>年
                    <select name="month">
                        <script type="text/javascript">
                            for (var i = 1; i <= 12; i++) {
                                document.write("<option value=" + i + ">" + i + "</option>");
                            }
                        </script>
                    </select>月
                    <select name="day">
                        <script type="text/javascript">
                            for (var i = 1; i <= 31; i++) {
                                document.write("<option value=" + i + ">" + i + "</option>");
                            }
                        </script>
                    </select>日
                </td>
            </tr>
            <tr>
                <td>&nbsp;</td>
                <td><input name="btn" type="submit" value="注册" class="rb1"/></td>
            </tr>
        </form>
    </table>

</div>
<div id="footer" class="main"><a href="#">关于我们</a> | <a href="#">诚聘英才</a> |<a href="#"> 联系方式</a> | <a href="#">帮助中心</a>
</div>
</body>
</html>

```

# 为什么要使用正则表达式
平时验证一个字符串的是否符合要求(例如：email格式的验证)，我们需要写很多代码来验证，但是如果使用正则表达式来验证，可以使代码变得非常简洁。

==关于正则表达式的语法可以参考我的另一篇博客==：[正则表达式语法](https://blog.csdn.net/star_of_science/article/details/107748798)
下面介绍正则表达式的使用方法：

# 正则表达式的两种创建方法
方法一：构造函数
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200802212533596.png)

方法二：普通方法，又称perl风格（==用的比较多==）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200802212538903.png)


注意：常用的附加参数有g和i，g代表可以进行全局匹配，i代表不区分大小写

# 正则表达式的模式
简单模式：是指通过普通字符的组合来表达的模式，例如：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200802212553981.png)
简单模式只能表示具体的匹配，如果要匹配一个邮箱或者电话号码，就不能使用具体的匹配，这就要用到复合模式。

==复合模式：复合模式是指含有通配符来表达的模式==，例如：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200802212607357.png)
# 正则表达式常用的方法
1、test：判断字符串中是否匹配正则表达式，返回一个boolean值
2、exec：每调用一次可以获取一个匹配的字符，并确定其位置(lastIndex)

```javascript
<script type="text/javascript">
        //验证字符串是否包含abc
        /*var reg = /abc/;//创建正则表达式
        var str = "sdfsdfabcdfdf";
        var result = reg.test(str);
        document.write(result);*/

        //验证是否包含abc，忽略大小写
        /*var reg = /abc/i;//创建正则表达式   i表示忽略大小写
        var str = "sdfsdfaBcdfdf";
        var result = reg.test(str);
        document.write(result);*/

        //验证是否以abc开头
        /*var reg = /^abc/;//创建正则表达式   ^表示开头
        var str = "abcdfdf";
        var result = reg.test(str);
        document.write(result);*/

        //验证是否以abc结尾
        /*var reg = /abc$/i;//创建正则表达式   $表示结尾
        var str = "sdfsdfabc";
        var result = reg.test(str);
        document.write(result);*/

        //exec()方法的使用
        var reg = /a/g;  //g表示全局匹配
        var str = "dsadfadaffd";
        var result = reg.exec(str);
        //lastIndex用于获取下次匹配的开始索引(注意：附件参数要用g，否则lastIndex持续为0)
        document.write(result+"-"+reg.lastIndex);
        result = reg.exec(str);
        document.write(result+"-"+reg.lastIndex);

    </script>
```
正则表达式验证邮编和电话号码：

```javascript
<script type="text/javascript">
        //验证邮编
        var reg = /^[0-9]{6}$/;
        var str = "515006";
        document.write(reg.test(str));

        //验证电话号码
        var reg2 = /^1\d{10}$/;
        var str2 = "13522823123";
        document.write(reg2.test(str2))
    </script>
```
正则表达式验证邮箱：

```javascript
<script type="text/javascript">
        //验证邮箱  ****@**.com cn
        var reg = /^\w+@\w+.[a-z]{2,3}$/;
        var email = "zhangsan@163.cn";
        document.write(reg.test(email));
    </script>
```

# 下拉列表框常用事件、方法和属性
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200802212645494.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N0YXJfb2Zfc2NpZW5jZQ==,size_16,color_FFFFFF,t_70)
下拉列表框的使用：
```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <script type="text/javascript">
        function addOption(){
            var op = new Option("广东","gd");//参数一：显示的文本   参数二：值
            var sel = document.getElementById("selPro");//获取下拉列表框
            sel.options.add(op);//将创建的选项添加到下拉列表框中
        }

        function showOption(){
            var sel = document.getElementById("selPro");//获取下拉列表框
            var v = sel.value;//获取选中的值
            var index = sel.selectedIndex;//获取选中项的缩影
            alert(v+"-"+index);
        }
    </script>
</head>
<body>
<select id="selPro" onchange="showOption()">
    <option value="hn">湖南</option>
    <option value="hb">湖北</option>
</select>
<input type="button" value="添加一个option" onclick="addOption()" />
</body>
</html>
```

# 数组的使用
创建数组：
var 数组名称 = new Array(数组长度);
注意：数组长度可以不写

给数组赋值：(有多种方法)
方法一：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200802212707673.png)

方法二：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020080221271146.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N0YXJfb2Zfc2NpZW5jZQ==,size_16,color_FFFFFF,t_70)

方法三：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200802212715267.png)


遍历数组：
方法一：普通循环
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200802212721722.png)
方法二：增强型for循环
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200802212724855.png)

注意：遍历出来的v是索引

数组的常用属性和方法
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200802212741432.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N0YXJfb2Zfc2NpZW5jZQ==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200802212745139.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N0YXJfb2Zfc2NpZW5jZQ==,size_16,color_FFFFFF,t_70)

```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <script type="text/javascript">
        var arr = new Array();
        arr[0] = "张三";
        arr[1] = 23;
        arr["one"] = 25.6;
        document.write(arr[1]+"<br>");
        document.write(arr["one"]+"<br>");

        document.write("================数组遍历===============<br>");
        //数组循环(方法一：普通循环)
        for(var i=0;i<arr.length;i++){
            document.write(arr[i]+"<br>");
        }
        //数组循环(方法二：增强型for循环  注意：遍历出来的不是元素，而是下标)
        for(var i in arr){
            document.write(arr[i]+"<br>");
        }


        var arr2 = new Array();
        arr2["hn"] = ["长沙","株洲","湘潭"];
        document.write(arr2["hn"][1]);
    </script>
</head>
<body>

</body>
</html>
```
省市级联：

```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <script type="text/javascript">
        var arr = new Array();
        arr["hn"] = ["长沙","株洲","湘潭"];
        arr["gd"] = ["广州","深圳","东莞"];

        function addCity(){
            //获取选中省份的值
            var pro = document.getElementById("selPro").value;
            var citys = arr[pro];
            //先清空城市下拉列表的选项
            document.getElementById("selCity").length = 0;
            for(var i=0;i<citys.length;i++){
                var c = citys[i];
                var op = new Option(c,c);
                document.getElementById("selCity").options.add(op);
            }
        }

        window.onload = addCity;
    </script>
</head>
<body>
    省份：<select id="selPro" onchange="addCity()">
        <option value="hn">湖南</option>
        <option value="gd">广东</option>
    </select><br>
    城市：<select id="selCity">

    </select>
</body>
</html>
```
