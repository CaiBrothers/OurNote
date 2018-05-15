### 表格标签

**视频源：** 15 _ 基本表格.avi，16_ 表格的属性.avi，17_ 表格的结构标签.avi ，18_ 行和列的删除.avi，19_单元格的合并.avi

**知识点：** 

1. 表格标签的基本使用
2. 表格结构标签 
3. 表格行列删除 
4. 单元格合并

**概念：**

1. 表格标签的基本使用< table >  < tr > < td >
2. 表格结构标签 < thead > < tbody > < tfoot > 
3. 表格行列删除：删除表格的一行或一列 
4. 单元格合并 ：将表格的某些单元格合并为一个单元格

**需求：** 

**代码:**

```
//普通表格
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
	</head>
	<body>
		
		<table>
			<tr>
				<th>ID</th>
				<th>name</th>
				<th>age</th>
			</tr>
			<tr>
				<td>001</td>
				<td>尼古拉斯赵四</td>
				<td>16</td>
			</tr>
			<tr>
				<td>002</td>
				<td>尼古拉斯贤</td>
				<td>25</td>
			</tr>
		</table>
		
		
		//表格结构标签thead tbody
		<table>
			<caption>会员等级</caption>
			<thead>   
				<tr>
					<th>ID</th>
					<th>name</th>
					<th>age</th>
				</tr>	
			</thead>
			
			<tbody>
				<tr>
					<td>001</td>
					<td>尼古拉斯赵四</td>
					<td>16</td>
				</tr>
				
				<tr>
					<td>002</td>
					<td>西门吹雪</td>
					<td>25</td>
				</tr>
			
			</tbody>
			
		</table>
		
	</body>
</html>
```

**运行结果**

```

```

**小细节（注意事项）**

表格可以嵌套表格

```

```

**总结**

普通表格标签：
< table >表格  

* 子标签：
  * < tr > 行标签   
  * < caption >标题标签，必须是table的第一个子标签
* 子子标签：
  * < td > 单元格标签  
  * < th > 表头标签

table及子标签属性：	

* border  边框
* align 对齐方式
* width 宽度
* cellpadding 内边距
* cellspacing 外边距， 其默认值是1px，可以设置为0取消边距



表格结构标签

由于表格加载时会作为一个整体，效率不高，为了提高用户体验，表格应该使用结构标签
< thead > 表头
< tbody > 表内容
< tfoot > 表尾
三者改变位置不影响

tips：表格可以嵌套表格







### 框架标签

**视频源：** 20_框架集.avi

**知识点：** 框架标签及其用法

**概念：**

1. 框架标签的使用场景：主要用在后端界面
2. 框架标签的使用方法：< frameset > 和< frame >

**需求：** 

**代码:**

```
//创建一个框架集
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	
	<frameset rows="20%, 70%, 10%">
		<frame src=""/>
		<frameset cols="20%, *">
			<frame src="" />
			<frame src="" />
		</frameset>
		<frame />
		
		
	</frameset>
	
</html>
```

**运行结果**

```

```

**小细节（注意事项）**

框架标签不能和body标签共存

```

```

**总结**

框架标签（有框架标签就不能有body标签）

* 属性： 
  * src 指定引用路径，可以是html页面，被引用的页面不需要完整结构，只需要页面内容即可








### 表单标签

**视频源：**21_ 基本表格.avi，22_ 下拉框和文本域.avi ，23_ 常用属性和默认值.avi，24_ 表单的属性.avi

**知识点：** 表单使用方法

**概念：**

1. 几种常用的表单使用
2. 表单中的主要属性

**需求：** 

**代码:**

```
<!DOCTYPE html>
<html>

	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	
	<body>
	
		//input表单
	
		账号<input type="text" name="acount" id="" value="" /> <br /> 
		密码<input type="password" name="password" id="" value="" /><br /> 
		性别 <input type="radio" name="gender" id="" value="男" />男
		<input type="radio" name="gender" id="" value="女" />女 <br /> 
		兴趣爱好 <input type="checkbox" name="hobby" id="" value="" />
		篮球<input type="checkbox" name="hobby" id="" value="" />
		足球<input type="checkbox" name="hobby" id="" value="" />
		羽毛球<br />
		<input type="submit" name="submit" id="" value="提交" />
	
		//select下拉表单
		家乡 <select name="city">
			<option value=""> 北京</option>
			<option value=""> 上海</option>
			<option value=""> 深圳</option>
			<option value=""> 广州</option>
		</select>
		
		//文本域表单
		自我介绍 <textarea></textarea>
	
	</body>

</html>
```



**运行结果**

```

```

**小细节（注意事项）**

```

```

**总结**

表单标签

* < form >标签
  * 属性：	
    * action  ：规定当提交表单时向何处发送表单数据。
    * method ：两种数据传递给后台的方式
      * get 请求，在原地址后面以? 拼接参数，传递给后台，key = value的形式去拼接，多个参数用&连接，传输数据大小最大一般是1kb
      * post请求，数据隐藏起来，相对来说更加安全，传文件一定要用post，其传输大小由后台服务器决定



* 子标签< input >（普通输入框）
  * 通用属性：
    * name 数据要传输给后台，必须指定该属性
    * value 指定按钮上的文本，以及指定选择框（单选和复选）传递给后台的数据
  * 属性：
    * type 指定输入框类型
      * 默认text 文本输入框
      * password密码输入框（不可见）
      * radio单选框（通过name将单选框分组）
      * checkbox复选框
      * file 文件选择框
      * submit 提交框
      * reset 情况框
      * button 自定义按钮
      * hidden 隐藏域
      * image 图片提交 ，不常用
      * placeholder 指定框内显示的提示文本

​		

* 子标签select（下拉框）   嵌套  < optgroup > < option > 
* 子标签textarea (文本域)







