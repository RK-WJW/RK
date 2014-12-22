###div

> <div> 可定义文档中的分区或节（division/section）。
> <div> 标签可以把文档分割为独立的、不同的部分。它可以用作严格的组织工具，并且不使用任何格式与其关联。
如果用 id 或 class 来标记 <div>，那么该标签的作用会变得更加有效。

div标签中内容相当于一个独立的逻辑部分，属于块级元素。

###table

> <table> 标签定义 HTML 表格。
> 简单的 HTML 表格由 table 元素以及一个或多个 tr、th 或 td 元素组成。
> tr 元素定义表格行，th 元素定义表头，td 元素定义表格单元。
> 更复杂的 HTML 表格也可能包括 caption、col、colgroup、thead、tfoot 以及 tbody 元素。

* `<table>` 相当于整个表格的根标签
* `<caption>` 表格标题，必须紧跟table开始标签之后
* `<thead>` 表头内容
* `<tbody>` 表格主体，用于组合HTML表格的主体内容，应与`<thead>`和`<tfoot>`结合起来使用
* `<tfoot>` 表注（页脚）内容
* `<tr>` 表格的一行
* `<td>` 标准单元格
* `<th>` 表头单元格

*thead、tbody、tfoot标签使用的话必须全部使用，并且出现的次序是：thead、tbody、tfoot，在table内部使用。*

###a

```
<a href="链接" title="标题" target="方式" ></a>
```

`<a>`标签定义超链接，用于从一个页面跳到另一个页面，跳到的页面由属性`href`设定，重要属性还有`target`设置何处打开链接文档，如`_self`当前页面打开，`_blank`新页面打开，`title`文本内容，用于描述链接地址的内容，鼠标停留在链接文字上时，会显示该文本内容，实际网页开发中作用很大，方便搜索引擎了解所链接地址的内容，语义化更友好。另外还可以链接Email地址，使用mailto，详细如图：
![`<a>`标签mailto详细用法<br>图片来源：慕课网](http://7sbq8j.com1.z0.glb.clouddn.com/images/mkTag.png)


###img

```
<img src="图像地址" alt="替代描述文字" title="图像描述文字" />
```

图片标签，使用`<img>`向网页中插入图片。主要属性有：

* src 标识图像的位置
* alt 图像的描述性文本，当图片不可见时，将显示该文本
* title 图像的描述，当鼠标停留图像上是显示

###form

```
<form action="提交的地址" method="提交方式">
...
</form>
```

`<form>`标签用于为用户输入创建 HTML 表单，用于向服务器传输数据。主要属性：

* action 数据将被传送的地方，一个服务端地址。
* method 数据传输的方式，分GET和POST。

表单的所有控件必须放在<form></form>标签之间，常用控件有文本框、文本域、单选框、复选框等。

####input
主要属性：
* type 指定input框类型。
  `type="text"` --> 文本输入框
  `type="password"` --> 密码输入框
  `type="radio"` --> 单选框
  `type="checkbox"` --> 复选框
  `type="submit"` --> 提交按钮，提交表单信息
  `type="reset"` --> 重置按钮，重置表单信息到初始时的状态
  
* name 为文本框命名，备后台程序使用。
* value 设置默认值

当type为radio/checkbox时，可设置checked属性，控制是否默认选中。同一组单选按钮，name取值一定要一致。

####textarea

文本域，多行文本输入。语法：

```
<textarea name="名称" row="行数" cols="列数">文本...</textarea>
```

####select

```
<select>
    <option value="提交值">选项</option>
    <option value="提交值2" selected="selected">选项2</option>
    ...
</select>
```

下拉列表选择框，`selected="selected"`设置默认选中。在select标签中设置multiple="multiple"属性，可实现多选功能，但基本上没人使用。

####label

```
<form>
  <label for="male">Male</label>
  <input type="radio" name="sex" id="male" />
  <br />
  <label for="female">Female</label>
  <input type="radio" name="sex" id="female" />
</form>
```

> `<label>` 标签为 input 元素定义标注（标记）.
> label 元素不会向用户呈现任何特殊效果。不过，它为鼠标用户改进了可用性。如果您在 label 元素内点击文本，就会触发此控件。就是说，当用户选择该标签时，浏览器就会自动将焦点转到和标签相关的表单控件上。
> `<label>` 标签的 for 属性应当与相关元素的 id 属性相同。

###其他
* `<p>`  文章的段落，一个p标签就是一个段落。
* `<hx>` 文章的标题，h1~6六个，分别为一到六级标题，并且重要性递减。
* `<em>` 表示强调语气，浏览器中默认斜体样式。
* `<strong>` 表示强调语气，比em更强烈，浏览器默认粗体样式显示。
* `<span>` 没有语义
* `<q>` 短文本引用
* `<blockquote>` 长文本引用
* `<br>` 换行
* `<hr>` 用于分隔的水平横线
* `<address>` 地址信息
* `<code>` 行级代码
* `<pre>` 段级代码
* `<ul>/<li>` 无序列表
* `<ol>/<li>` 有序列表