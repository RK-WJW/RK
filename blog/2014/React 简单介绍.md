###why React？

React是Facebook开发的一款JS库，那么Facebook为什么要建造React呢，主要为了解决什么问题，通过这个又是如何解决的？

从这几个问题出发我就在网上搜查了一下，有这样的解释。

Facebook认为MVC无法满足他们的扩展需求，由于他们非常巨大的代码库和庞大的组织，使得MVC很快变得非常复复杂，每当需要添加一项新的功能或特性时，系统的复杂度就成级数增长，致使代码变得脆弱和不可预测，结果导致他们的MVC正在土崩瓦解。认为MVC不适合大规模应用，当系统中有很多的模型和相应的视图时，其复杂度就会迅速扩大，非常难以理解和调试，特别是模型和视图间可能存在的双向数据流动。

解决这个问题需要“以某种方式组织代码，使其更加可预测”，这通过他们(Facebook)提出的Flux和React已经完成。

>`Flux`是一个系统架构，用于推进应用中的数据单向流动。`React`是一个JavaScript框架，用于构建“可预期的”和“声明式的”Web用户界面，它已经使Facebook更快地开发Web应用

对于Flux，目前还没怎么研究，不怎么懂，这里就先把Flux的图放上来，有兴趣或者了解的可以再分享下，这里主要说下React。

![Flux](http://upload-images.jianshu.io/upload_images/35008-614667368b68ec5b.png)

那么React是解决什么问题的，在官网可以找到这样一句话：

>We built React to solve one problem: building large applications with data that changes over time. 

构建那些数据会随时间改变的大型应用，做这些，React有两个主要的特点：
1. 简单    
   简单的表述任意时间点你的应用应该是什么样子的，React将会自动的管理UI界面更新当数据发生变化的时候。
2. 声明式    
   在数据发生变化的时候，React从概念上讲与点击了F5一样，实际上它仅仅是更新了变化的一部分而已。
React是关于构造可重用组件的，实际上，使用React你做的仅仅是构建组建。通过封装，使得组件代码复用、测试以及关注点分离更加容易。

另外在React官网上，通过《[Why did we build React?][WhyDidReact]》为什么我们要建造React的文档中还可以了解到以下四点：
- React不是一个MVC框架
- React不使用模板
- 响应式更新非常简单
- HTML5仅仅是个开始

具体也可以看我前面一篇文章《[为什么我们要造React？][WhyDidReact2]》。

###React主要的原理
__Virtual DOM 虚拟DOM__    
传统的web应用，操作DOM一般是直接更新操作的，但是我们知道DOM更新通常是比较昂贵的。而React为了尽可能减少对DOM的操作，提供了一种不同的而又强大的方式来更新DOM，代替直接的DOM操作。就是`Virtual DOM`,一个轻量级的虚拟的DOM，就是React抽象出来的一个对象，描述dom应该什么样子的，应该如何呈现。通过这个Virtual DOM去更新真实的DOM，由这个Virtual DOM管理真实DOM的更新。

为什么通过这多一层的Virtual DOM操作就能更快呢？ 这是因为React有个diff算法，更新Virtual DOM并不保证马上影响真实的DOM，React会等到事件循环结束，然后利用这个diff算法，通过当前新的dom表述与之前的作比较，计算出最小的步骤更新真实的DOM。

![virtual DOM](http://upload-images.jianshu.io/upload_images/35008-0f4e9a2fb5c19485.png)

__Components 组件__    
在DOM树上的节点被称为元素，在这里则不同，Virtual DOM上称为commponent。Virtual DOM的节点就是一个完整抽象的组件，它是由commponents组成。
>component 的使用在 React 里极为重要, 因为 components 的存在让计算 DOM diff 更高效。

__State 和 Render__
React是如何呈现真实的DOM，如何渲染组件，什么时候渲染，怎么同步更新的，这就需要简单了解下State和Render了。state属性包含定义组件所需要的一些数据，当数据发生变化时，将会调用Render重现渲染，这里只能通过提供的setState方法更新数据。

好了，说了这么多，下面看写代码吧，先看一个官网上提供的`Hello World`的示例：
```
<!DOCTYPE html>
<html>
  <head>
    <script src="http://fb.me/react-0.12.1.js"></script>
    <script src="http://fb.me/JSXTransformer-0.12.1.js"></script>
  </head>
  <body>
    <div id="example"></div>
    <script type="text/jsx">
      React.render(
        <h1>Hello, world!</h1>,
        document.getElementById('example')
      );
    </script>
  </body>
</html>
```
这个很简单，浏览器访问，可以看到`Hello, world!`字样。`JSXTransformer.js`是支持解析JSX语法的，JSX是可以在Javascript中写html代码的一种语法。如果不喜欢，React也提供原生Javascript的方法。

再来看下另外一个例子：
```
<html>
    <head>
        <title>Hello React</title>
        <script src="http://fb.me/react-0.12.1.js"></script>
        <script src="http://fb.me/JSXTransformer-0.12.1.js"></script>
        <script src="http://code.jquery.com/jquery-1.10.0.min.js"></script>
        <script src="http://cdnjs.cloudflare.com/ajax/libs/showdown/0.3.1/showdown.min.js"></script>
        <style>
        #content{
            width: 800px;
            margin: 0 auto;
            padding: 5px 10px;
            background-color:#eee;
        }
        .commentBox h1{
            background-color: #bbb;
        }
        .commentList{
            border: 1px solid yellow;
            padding:10px;
        }
        .commentList .comment{
            border: 1px solid #bbb;
            padding-left: 10px;
            margin-bottom:10px;
        }
        .commentList .commentAuthor{
            font-size: 20px;
        }
        .commentForm{
            margin-top: 20px;
            border: 1px solid red;
            padding:10px;
        }
        .commentForm textarea{
            width:100%;
            height:50px;
            margin:10px 0 10px 2px;
        }
        </style>
    </head>
    <body>
        <div id="content"></div>
        <script type="text/jsx">
        var staticData = [
            {author: "张飞", text: "我在写一条评论~！"},
            {author: "关羽", text: "2货，都知道你在写的是一条评论。。"},
            {author: "刘备", text: "哎，咋跟这俩逗逼结拜了！"}
        ];

        var converter = new Showdown.converter();//markdown
        
        /** 组件结构：
            <CommentBox>
                <CommentList>
                    <Comment />
                </CommentList>
                <CommentForm />
            </CommentBox>
        */
        //评论内容组件
        var Comment = React.createClass({
            render: function (){
                var rawMarkup = converter.makeHtml(this.props.children.toString());
                return (
                    <div className="comment">
                        <h2 className="commentAuthor">
                            {this.props.author}:
                        </h2>
                        <span dangerouslySetInnerHTML={{__html: rawMarkup}} />
                    </div>
                );
            }
        });
        //评论列表组件
        var CommentList = React.createClass({
            render: function (){
                var commentNodes = this.props.data.map(function (comment){
                    return (
                        <Comment author={comment.author}>
                            {comment.text}
                        </Comment>
                    );
                });
            
                return (
                    <div className="commentList">
                        {commentNodes}
                    </div>
                );
            }
        });
        
        //评论表单组件
        var CommentForm = React.createClass({
            handleSubmit: function (e){
                e.preventDefault();
                var author = this.refs.author.getDOMNode().value.trim();
                var text = this.refs.text.getDOMNode().value.trim();
                if(!author || !text){
                    return;
                }
                this.props.onCommentSubmit({author: author, text: text});
                this.refs.author.getDOMNode().value = '';
                this.refs.text.getDOMNode().value = '';
                return;
            },
            render: function (){
                return (
                    <form className="commentForm" onSubmit={this.handleSubmit}>
                        <input type="text" placeholder="Your name" ref="author" /><br/>
                        <textarea type="text" placeholder="Say something..." ref="text" ></textarea><br/>
                        <input type="submit" value="Post" />
                    </form>
                );
            }
        });
        
        //评论块组件
        var CommentBox = React.createClass({
            loadCommentsFromServer: function (){
                this.setState({data: staticData});
                /*
                方便起见，这里就不走服务端了，可以自己尝试
                $.ajax({
                    url: this.props.url + "?_t=" + new Date().valueOf(),
                    dataType: 'json',
                    success: function (data){
                        this.setState({data: data});
                    }.bind(this),
                    error: function (xhr, status, err){
                        console.error(this.props.url, status, err.toString());
                    }.bind(this)
                });
                */
            },
            handleCommentSubmit: function (comment){
                //TODO: submit to the server and refresh the list
                var comments = this.state.data;
                var newComments = comments.concat([comment]);
                
                //这里也不向后端提交了
                staticData = newComments;
                
                this.setState({data: newComments});
            },
            //初始化 相当于构造函数
            getInitialState: function (){
                return {data: []};
            },
            //组件添加的时候运行
            componentDidMount: function (){
                this.loadCommentsFromServer();
                this.interval = setInterval(this.loadCommentsFromServer, this.props.pollInterval);
            },
            //组件删除的时候运行
            componentWillUnmount: function() {
                clearInterval(this.interval);
            },
            //调用setState或者父级组件重新渲染不同的props时才会重新调用
            render: function (){
                return (
                    <div className="commentBox">
                        <h1>Comments</h1>
                        <CommentList data={this.state.data}/>
                        <CommentForm onCommentSubmit={this.handleCommentSubmit} />
                    </div>
                );
            }
        });
        
        //当前目录需要有comments.json文件
        //这里定义属性，如url、pollInterval，包含在props属性中
        React.render(
            <CommentBox url="comments.json" pollInterval="2000" />,
            document.getElementById("content")
        );
        </script>
    </body>
</html>
```
乍一看挺多，主要看脚本部分就可以了。方便起见，这里都没有走后端。定义了一个全局的变量`staticData`，可权当是走服务端，通过浏览器的控制台改变`staticData`的值，查看下效果，提交一条评论，查看下staticData的值的变化。

###应用情况
国外应用的较多，facebook、Yahoo、Reddit等。在github可以看到一个列表[Sites-Using-React][]，国内的话，查了查，貌似比较少，目前知道的有一个杭州大搜车。大多技术要在国内应用起来一般是较慢的，不过React确实感觉比较特殊，特别是UI的组件化和Virtual DOM的思想，我个人比较看好，有兴趣继续研究研究。

###比较分析
和其他一些js框架相比，React怎样，比如Backbone、Angular等。
- React不是一个MVC框架，它是构建易于可重复调用的web组件，侧重于UI, 也就是view层
- 其次React是单向的从数据到视图的渲染，非双向数据绑定
- 不直接操作DOM对象，而是通过虚拟DOM通过diff算法以最小的步骤作用到真实的DOM上。
- 不便于直接操作DOM，大多数时间只是对 virtual DOM 进行编程

好了，就这些了，查看了不少资料，东拼西凑出来，权当整理吧，当然，整理的也可能很烂，哈哈
将就吧~~
###参考资料
1. [React 官网](http://facebook.github.io/react/) 
1. [React github](https://github.com/facebook/react)
1. [React中文社区](http://react-china.org/)
1. [Facebook：MVC不适合大规模应用，改用Flux](http://www.infoq.com/cn/news/2014/05/facebook-mvc-flux)
1. [Why did we build React?](http://facebook.github.io/react/blog/2013/06/05/why-react.html)
1. [Facebook 的 React 框架解析](http://www.open-open.com/lib/view/open1405409050727.html)
1. [关于从 Backbone 转向 React 的思考](http://segmentfault.com/blog/jiyinyiyong/1190000000576880)
1. [React 的 diff 算法](http://www.pg265.com/articles_4962.html)


[WhyDidReact]: http://facebook.github.io/react/blog/2013/06/05/why-react.html
[WhyDidReact2]: http://www.jianshu.com/p/dc54c5ba246d
[Sites-Using-React]: https://github.com/facebook/react/wiki/Sites-Using-React