## React开发流程

### 一、React  特点

​	*·声明式设计

​		采用声明式范，可以轻松地描述应用

​	*·高性能

​		操作DOM节点，最大限度的减少与DOM的交互，【真是DOM由框架实现，操作DOM是很消耗性能的】

​	*·组件化开发

​		通过React构建组件，使得代码更加得到复用 ，能够高效的应用在大项目中。

​	*·JSX扩展

​		在js中编写html

​		浏览器不支持jsx语法【既然不支持，那么就需要编译成js、html代码，通过babel来实现】

​	*·单项响应的数据流

​		React实现了单项响应的数据流，从而减少了代码的重复，这也就是它为什么比传统数据绑定更简单

​	*·灵活

​		react可以与已知的库活框架很好的配合。 

### 二、React  传统做法

##### 1、通过script标签引入三个文件

​	*react.js  ：React的核心库

​	*react-dom.js   提供与dom相关的功能，【虽然是操作虚拟dom但是实际上还是需要操作的，只是由框架去实现】

​	*babel.js  React使用es6语法和浏览器不支持的jsx语法，所以必须应用babel进行编译

​		【注意在浏览器中使用babel来编译jsx效率是非常低的】

##### 2、使用

​	*进入官网下载相应的js代码

```
https://reactjs.org
```

##### 3、例子

```
<!DOCTYPE html>
<html>
	<head>
	  <meta charset="utf-8">
	  <meta name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=no">
	  <title>第一个应用</title>
	  <script type="text/javascript">
			document.documentElement.style.fontSize = document.documentElement.clientWidth/10+'px';
	  </script>
	</head>
	<body>
		<h1>第一个应用</h1>
		<div id="app"></div>
		<!-- 注意此时script的类型是 text/bable，为了解析jsx语法-->
		
		<!--babel  jsx语法转换  react的核心库    dom相关 -->
		 <script src="../lib/babel.min.js"></script>
		 <script src="../lib/react.development.js"></script>
		 <script src="../lib/react-dom.development.js"></script>
		 
		<script type="text/babel">
			/*
				渲染方法：ReactDOM.render(template,targetDOM)【把数据渲染到挂载点】
					*template模板
					*targetDOM需要挂载到的节点
				JSX语法限制：
					*在js代码中直接编写html
					* 在jsx代码中，同为js关键字的html属性不能直接使用【class===>className】(驼峰命名法)
					* 必须有结束标签【<img src="" alt=""/> <input type="text"/>】
			*/
		   let userName='lvyunxue';
		   ReactDOM.render(
			   <div className="box">
				<input type="text" name="userName" id="name1" value={userName}/>
			   </div>,
			  document.querySelector("#app")
		   )
		</script>
	</body>
</html>

```

##### 4、元素渲染

​	ReactDOM.render(template,targetDOM)

​	是React的最基本方法，用于将模板转为HTML语言，并插入指定的DOM节点

​	template：	可以是HTML标签或 React 组件，React利用大小写来区分标签与组件
				要渲染 HTML 标签，只需在 JSX 里使用小写字母的标签名。
				要渲染 React 组件，只需创建一个大写字母开头的本地变量
	targetDOM：挂载点，必须为元素节点

### 三、jsx样式的编写

##### 1、写行内样式【以下代码不能直接执行，只是为了书写注释】

```
<body>
    <h1>第一个应用</h1>
    <div id="app"></div>
    <script src="../lib/babel.min.js"></script>
    <script src="../lib/react.development.js"></script>
    <script src="../lib/react-dom.development.js"></script>

    <script type="text/babel">
    let userName='lvyunxue';
    ReactDOM.render(
        <div className="box">
        //如果想要userName添加一些样式，则可以像下面这样书写
        //注意：驼峰命名书写方法，样式里边用对象的形式书写，注意color:'red'后边的引号
        <em style={{color:'red',fontSize:30}}>{userName}</em> 
        </div>,
        document.querySelector("#app")
    )
    </script>
</body>
```

##### 2、添加注释

```
 <script type="text/babel">
    let userName='lvyunxue';
    ReactDOM.render(
        <div className="box">
       //如果想要再此添加注释，记得不能在jsx里边直接书写注释，会报错或者不能注释，需要用变量的形式书写
        <em style={{color:'red',fontSize:30}}>{userName}</em> 
        </div>,
        document.querySelector("#app")
    )
 </script>
```

```
<body>
    <h1>第一个应用</h1>
    <div id="app"></div>
    <script type="text/babel">
    let userName='lvyunxue';
    let aa=<div className="box">
			<em style={{color:'red',fontSize:30}}>{userName}</em> 
        </div>
    ReactDOM.render(
        aa,
        document.querySelector("#app")
    )
    </script>
</body>
```

##### 3、总结以上笔记

【1】、jsx语法

​	一种特殊的js语法，是ECMAScript的扩展，可以让我们在js代码中直接使用html标签，再通过编译器（Babel）转成标准的 JavaScript 后由浏览器执行。

Babel解析规则：

> 分清html标签、组件、js代码

- 遇到 HTML 标签（以 < 开头），就用 HTML 规则解析；
- 遇到代码块（以 { 开头），就用 JavaScript 规则解析；

> 注意： *因为Javascript代码与JSX代码并不兼容，凡是使用JSX的script标签都需要加上 type=”text/babel”* 在jsx代码中，同为js关键字的html属性不能直接使用（如：class->className,for->htmlFor） *内联样式写法：style={{“backgroundColor”:”#f60”}}，react推荐我们写行内样式* 必须结束标签（如：`<input type="text"/>`） *花括号{}内为js表达式，不允许出现var,let,const等关键字* 使用js语法注释（如{`/*注释内容*/`}，`//注释内容`）

### 四、组件化开发

##### 1、定义组件【函数式的方法定义组件】

```
	<body>
		<h1>函数式组件</h1>
		<div id="app"></div>
		<!-- <img src="../img/1.jpg" /> //必须要有结束符 -->
		<script type="text/babel">
		    // 函数定义组件
		    	*页面上出现的内容取决于组件里边return后边的值
		    	*组件必须只有一个根节点，
		    	*所以return后边加上<div></div>套起来
			function MyHeader(){
				return <div>
				<header>组件化开发</header>
				<img src="../img/1.jpg" style={{width:'100px',height:'100px'}}/>
				</div>
			}
		   ReactDOM.render(
		   		//组件标签首字母需要大写，这是组件区分html标签的方法
			   <MyHeader></MyHeader>,
			  document.querySelector("#app")
		   )
		</script>
	</body>

```

##### 2、类定义组件

```
<script type="text/babel">
    // 函数定义组件
    function MyHeader(){
        return <div>
            <header>组件化开发</header>
            <img src="../img/1.jpg" style={{width:'100px',height:'100px'}}/>
        </div>
    };
	//利用类定义组件
	//主要一个render函数作为渲染内容
    class MyClass extends React.Component{
        render(){
        return <div className="main">主题内容</div>
    }
    };
    ReactDOM.render(
    //记住，jsx代码中只能有一个根节点
    <div>
        <MyHeader></MyHeader>
        <MyClass></MyClass>
    </div>,
    document.querySelector("#app")
    )
</script>

```

### 五、组件之间参数的传递

##### 1、名片制作

```
<!DOCTYPE html>
<html>
	<head>
	  <meta charset="utf-8">
	  <meta name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=no">
	  <title>名片的制作</title>
	  <style type="text/css">
		.main{
			overflow: hidden;
			width: 375px;
			height: 156px;
			border: 2px solid red;
			padding: 20px 20px;
			box-sizing: border-box;
		}
		.main .img{
			display: inline-block;
			float: left;
		}
	  	.main .info{
			display: inline-block;
			padding-left: 50px;
			float:left;
		}
		.main .info h4{
			margin-top: 0;
		}
	  </style>
	</head>
	<body>
		<h1>名片的制作</h1>
		<div id="app"></div>
		<!-- <img src="../img/1.jpg" /> //必须要有结束符 -->
		<script src="../lib/babel.min.js"></script>
		<script src="../lib/react.development.js"></script>
		<script src="../lib/react-dom.development.js"></script>
		 
		<script type="text/babel">
			let cards=[
				{
					name:'laoxie',
					age:38,
					gender:'男',
					photo:'../img/1.jpg'
				},{
					name:'lvyunxue',
					age:18,
					gender:'男',
					photo:'../img/2.jpg'
				},{
					name:'lihui',
					age:17,
					gender:'女',
					photo:'../img/3.jpg'
				}
			];
			
			class Cards extends React.Component{
				render(){
					console.log(this.props.data);
					let data=this.props.data;
					return <div className="main">
						<img src={data.photo} style={{width:'140px',height:'113px'}} className="img"/>
						<div className="info">
							<h4>姓名:{data.name}</h4>
							<h4>年龄:{data.age}</h4>
							<h4>性别:{data.gender}</h4>
						</div>
					</div>
				}
			};
			ReactDOM.render(
			//组件之间参数的传递
			*通过在组件标签里边添加参数，
			*在组件里边通过props来接收【可以先在render函数下边通过打印this来查看所有信息】
			 <Cards data={cards[0]}/>,
			  document.querySelector("#app")
			)
		</script>
	</body>
</html>

```

补充：如果在组件的标签里边传递数字，在控制台打印出来的是字符串，如何才能变成数字呢

```
class Cards extends React.Component{
    render(){
        console.log(this.props.data);
        let data=this.props.data;
            return <div className="main">
                <img src={data.photo}/>
                <div className="info">
                <h4>姓名:{data.name}</h4>
                <h4>年龄:{data.age}</h4>
                <h4>性别:{data.gender}</h4>
                </div>
            </div>
	}
};
ReactDOM.render(
    <Cards data={cards[0]} number='123'/>,//此时打印的只是字符串
    document.querySelector("#app")
)
```

```
改：
<Cards data={cards[0]} number={123}/>,//此时打印的是数字
```

##### 2、简单的点击事件【改变this指向获得数据】【强制更新】this.forceUpdate();

```
			class ShowCard extends React.Component{
				next(){
					console.log(this);
					next++;
					if(next>=cards.length){
						next=0;
					}
					console.log(next);
					//强制更新，事先必须获得this对象
					this.forceUpdate();
				}
				render(){
					return <div>
					//在此先改变this指向，然后再 原型方法里边通过this就能获得数据
					<button onClick={this.next.bind(this)}>点击切换名片</button>
					<Cards data={cards[next]}/>
				</div>
				}
			}
			ReactDOM.render(
				<ShowCard/>,
				document.querySelector("#app")
			)
```

##### 3、获得this对象的方法还有【构造函数】

```
			class ShowCard extends React.Component{
			//此处就是构造函数
			*在使用构造器时，必须先调用super();函数，否则将会报错。
			*组件的属性会自动传入构造函数
				constructor(props){
					super();
					console.log(props);//自行查看浏览器结果
					console.log("构造器:"+this);
					this.next=this.next.bind(this);
				}
				next(){
					next++;
					if(next>=cards.length){
						next=0;
					}
					this.forceUpdate();
				}
				render(){
					return <div>
					<button onClick={this.next}>点击切换名片</button>
					<Cards data={cards[next]}/>
				</div>
				}
			}
			ReactDOM.render(
				<ShowCard/>,
				document.querySelector("#app")
			)

```

##### 4、名片的升级版【利用state状态改变实现组建的自动刷新】【state状态的改变会触发render函数的重新渲染】

```
		// 组件1
			class Cards extends React.Component{
				render(){
					let data=this.props.data;
					return <div className="main">
						<img src={data.photo} className="img"/>
						<div className="info">
							<h4>姓名:{data.name}</h4>
							<h4>年龄:{data.age}</h4>
							<h4>性别:{data.gender}</h4>
						</div>
					</div>
				}
			}
            // 组件2
			class ShowCard extends React.Component{
				constructor(){
					super();
					//利用state状态改变实现组件自动刷新
                    this.state={
                        index:0
                    };
                    this.next=this.next.bind(this);
				}
				next(){
                    let index=this.state.index
					index++;
					if(index>=cards.length){
						index=0;
					}
			//改变state里边的值，需要的相应的方法中才能改变，需要在setState()方法中才能改变
                    this.setState({index})
				}
				render(){
					return <div>
					<button onClick={this.next}>点击切换名片</button>
					<Cards data={cards[this.state.index]}/>
				</div>
				}
			}
			ReactDOM.render(
				<ShowCard/>,
				document.querySelector("#app")
			)

```

补充：如果state中有多个值，

```
this.state={
    index:0，
    data：100
};
```

那么在setState里边改变state的值，它不会全部改变，例如：

```
 this.setState({index})
```

此时只会改变index的值，data的值，将会一直不会改变

##### 5、react中遍历数组

```
//方法1
ReactDOM.render(
    <ul>
    //注意：如果直接在标签里边写js代码，那么需要用花括号括起来，否则就是错的
    	{
           cards.map((item,idx)=>{
               return <li kry="idx">{irem.name}</li>
           }) 
    	}
    </ul>,
    document.querySelector("#app")
)

//方法2【采用变量的形式】
let list=cards.map((item,idx)=>{
               return <li kry="idx">{irem.name}</li>
           }) 
ReactDOM.render(
    <ul>{list}</ul>,
    document.querySelector("#app")
)
```

### 六、实例

##### 1、走动的时钟

```
<!DOCTYPE html>
<html>
	<head>
	  <meta charset="utf-8">
	  <meta name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=no">
	  <title>走动的时钟</title>
	</head>
	<body>
		<h1>走动的时钟</h1>
		<div id="app"></div>
		<script src="../lib/babel.min.js"></script>
		<script src="../lib/react.development.js"></script>
		<script src="../lib/react-dom.development.js"></script>
		 
    <script type="text/babel">
        setInterval(()=>{
          ReactDOM.render(
              <div>{new Date().toLocaleTimeString()}</div>,
              document.querySelector("#app")
          )
        })
		</script>
	</body>
</html>

```

##### 2、数据校验及其组件之间通讯

```
<!DOCTYPE html>
<html>
	<head>
	  <meta charset="utf-8">
	  <meta name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=no">
		<title>组件间通讯</title>
		<style>
			.img{
				width: 80px;
				height: 80px;
			}
		</style>
	</head>
	<body>
		<div id="app"></div>
		<script src="../lib/babel.min.js"></script>
		<script src="../lib/react.development.js"></script>
		<script src="../lib/react-dom.development.js"></script>
		 
    <script type="text/babel">
        class GoodsList extends React.Component{
					constructor(){
						super();
						this.state={
							goodsList:[
								{
									"id":"G001",
									"title":"Thermos 膳魔师 Funtainer系列水杯 12盎司（340g） 粉红色",
									"category":"shoes",
									"imgurl":"../img/1.jpg",
									"url":"#",
									"price":899,
									"off":0.2,
									"star":4,
									"commentCount":10002
								},
								{
									"id":"G002",
									"title":"Thermos 膳魔师 Funtainer系列水杯 12盎司（340g） 粉红色",
									"category":"shoes",
									"imgurl":"../img/2.jpg",
									"url":"#",
									"price":698,
									"off":0.2,
									"star":4,
									"commentCount":10002
								},
								{
									"id":"G003",
									"title":"Thermos 膳魔师 Funtainer系列水杯 12盎司（340g） 粉红色",
									"category":"shoes",
									"imgurl":"../img/3.jpg",
									"url":"#",
									"price":398,
									"off":0.2,
									"star":4,
									"commentCount":10002
								},
								{
									"id":"G004",
									"title":"Thermos 膳魔师 Funtainer系列水杯 12盎司（340g） 粉红色",
									"category":"shoes",
									"imgurl":"../img/4.jpg",
									"url":"#",
									"price":998,
									"off":0.2,
									"star":4,
									"commentCount":10002
								},
								{
									"id":"G005",
									"title":"Thermos 膳魔师 Funtainer系列水杯 12盎司（340g） 粉红色",
									"category":"shoes",
									"imgurl":"../img/5.jpg",
									"url":"#",
									"price":198,
									"off":0.2,
									"star":4,
									"commentCount":10002
								}
							]
						}
					}
					render(){
						return<div>
								<ul>
									{
										this.state.goodsList.map((goods,idx)=>{
											return <Goods data={goods} key={idx} idx={idx}/>
										})
									}
								</ul>
						</div>
					}
				}

				
				class Goods extends React.Component{
					render(){
							let goods=this.props.data;
							return <li data-idx={this.props.idx}>
										<img src={goods.imgurl} className="img"/>
										<h4>{goods.title}</h4>
										<del>原价：{goods.price}</del>
										<span>现价：{goods.price*goods.off}</span>
							</li>
						}
				}

				//给props设置静态默认值，
				// 就是当li里遍布需要属性值时，上边组件又没有给出相应的值时，此时默认值就会起作用了，当上面组件设置了值时，默认值也不会覆盖以设置的值
				Goods.defaultProps={
					idx:0
				}

				//类型校验
				Goods.propTypes={
					idx:function(props,propName,comName){
						/* {data: {…}, idx: 0}
								idx
								Goods
						console.log(props);
						console.log(propName);
						console.log(comName);*/
						/* 以下就可以对上面组件传输的值进行相关的类型限制了*/
						/*当上面<Goods data={goods} key={idx} idx={"g"+idx}/>组件里边的额idx值做了字符串拼接，那么久不属于数字类型，所以会出现报错*/
						if(typeof props[propName] !='number'){
								return new Error(propName +'must be a number');
						}
					}
				}

				ReactDOM.render(
					<div><GoodsList/></div>,
					document.querySelector("#app")
				)
		</script>
	</body>
</html>

```

补充一：设置默认值

```
Goods.defaultProps={
	idx:0
}
```

补充二：类型限制

```
idx:function(props,propName,comName){
/* 以下就可以对上面组件传输的值进行相关的类型限制了*/
/*当上面<Goods data={goods} key={idx} idx={"g"+idx}/>组件里边的额idx值做了字符串拼接，那么久不属于数字类型，所以会出现报错*/
    if(typeof props[propName] !='number'){
    	return new Error(propName +'must be a number');
    }
}
```

##### 3、组件通讯+内容传输【props.children 】

```
		<script type="text/babel">
            class GoodsList extends React.Component{
                        render(){
                        //在这里就可以获取到下面组件标签里边的内容了
                            let data=this.props.children
                            return<div>
                            <h1>下面是组件内容</h1>
                            <p>{data}</p>
                            </div>
                        }
                    }

            ReactDOM.render(
                <GoodsList>
                    <p>这是第一个组件里边的标签</p>
                    <p>这是第二个组件里边的标签</p>
                </GoodsList>,
                document.querySelector("#app")
            )
        </script>

```

### 七、模块化开发【未完待续】

##### 1、安装相关的文件

（1）、安装package.json

```
0.npm init
```

(2)、安装package-lock.json

```
npm i webpack webpack webpack-cli webpack-dev-server -D
```

### 八、生命周期

##### 1、`constructor`

​	*是组件第一个生命周期，该周期是组件（构造函数）实例化的时候，获取`props`和`state`或者执行一些初始化函数的一个周期

​	*该周期就是我作为第一个组件，演员拿剧本（props）和化妆（state），准备最好的状态去登场

补充：

​	*ES5是用`getDefaultProps()`和`getInitialState`这两个来表述该生命周期

​	*ES6是用`constructor`来表述该状态

```
constructor(props){
    super(props)
    // 父传子 老爸给我的
    this.props = props;
    // 自己拥有的 就是vue组件里面data  Model
    this.state = {
        "title":"微信"
    };
}
```

##### 2、  componentWillMount【不能操作dom节点】 

​	*在组件被渲染到页面上之前执行，所以在此不能获取到元素渲染后的节点，在组件的整个生命周期内只执行一次 ，

​	*`componentWillMount`就是演员要登场了，导演给你的剧本（props）是不能变的，能变得是的你展示给观众（view）的状态（state）

​	*这个状态告诉我们两点，演员登场前可以在这里改变自己状态，该演员也只能登场一次,我们一般在该生命周期里面更改`state`但不要更改`props`

```
// 登场前
componentWillMount(){
    this.setState({
        "title":"支付宝"
    })
}
```

##### render

​	*演员排练的时候

​	*组件的内容必须依赖该周期呈现

​	*其实就是用数据配合`html`构造虚拟的DOM，因为操作虚拟DOM性能比较高，我会构造虚拟DOM去操作，等待下一步的挂载，将虚拟DOM挂到真实DOM节点上

```
render() {
    return (<div>
        {this.state.title}
    </div>);
}
```

##### 3、componentDidMount 【可以操作dom节点了】

​	*组件被渲染到页面上后立马执行，在组件的整个生命周期内只执行一次。 

​	*演员登场的时候

​	*这一步把刚才准备好的虚拟DOM挂载到真实DOM上面,你如果想去操作真实DOM结构，必须在这一个周期之后去操作，ajax请求一般放在这个地方，
	*其实这个生命周是整个组件最稳定的周期

```js
componentDidMount(){
    1、操作dom节点
	2、ajax请求
    3、设置 setInterval、setTimeout 等计时器操作
}
```

![](C:\Users\吕运学\Desktop\React\img\生命周期1.png)



##### 4、componentWillReceiveProps(nextProps) 

​	该方法在初始化render时不会被调用，可能在以下两种情况下被调用： 

​		*组件接收到了新的属性。新的属性会通过 nextProps 获取到。

​		*组件没有收到新的属性，但是由于父组件重新渲染导致当前组件也被重新渲染。

父组件：

![](C:\Users\吕运学\Desktop\React\img\跨组件改变状态值1.png)

子组件：

![](C:\Users\吕运学\Desktop\React\img\跨组件改变状态值2.png)

##### 5、componentWillUpdate(nextProps, nextState) 

> 在初始化时不会被调用，可能在以下两种情况下被调用：

​	*当组件 shouldComponentUpdate 返回 true 且接收到新的props或者state但还没有render时被调用

​	*或者调用 forceUpdate 时将触发此函数

​	*优化性能的一环,可以自己编写一些条件，如果该周期返回true就会更新数据模型，如果返回false就停止更新

```
// 只要props和state变化，该生命周期必定触发
shouldComponentUpdate(){
    if(this.state.inputValue.length>5){
        return true
    }else{
        return false
    }
}
```

##### 6、componentDidUpdate(nextProps, nextState) ====》相当于vue中的`updated`

在组件完成更新后立即调用。在初始化时不会被调用。 

在此处是做这些事情的好时机： 

​	*执行依赖新 DOM 节点的操作。

​	*依据新的属性发起新的网络请求。

注意：一定要在确认属性变化后再发起ajax请求，否则极有可能进入死循环：DidUpdate -> ajax -> changeProps -> DidUpdate -> …） 

##### 7、componentWillUnmount ===》相当于vue中的`destoryed`销毁了

在组件从 DOM 中移除之前立刻被调用。 

此处最适合做以下操作

​	*清除定时器	

​	*终止ajax请求

以下两个可以触发销毁阶段

```js
vue-router   /react-router
v-if         /函数式编程实现v-if,来让组件从节点出现或者销毁
```

### 补充：

##### 虚拟DOM

页面展示展示的内容`真实DOM`,真的在浏览器存在的DOM就是真实DOM

`虚拟DOM`不在浏览器存在的DOM就是虚拟DOM

```js
$.ajax().done((data)=>{
    // 把后端给的数据渲染到DOM结构上
    // render
    var html = data.arr.map((item)=>{
        return `
            <li>${item}</li>
        `
    }).join("");
    // 在挂载前我需要有一个html结构，但是该html结构是我用JS解析之后存到变量里面的，html就是虚拟的DOM，挂载前有数据，有虚拟DOM，而虚拟DOM其实用JS配合数据生成的
    // JS修改变量成本低廉，但是如果操作DOM成本昂贵吗,性能低效
    // 挂载前
    $("ul").html(html);
    // 挂载后
    // componentDidMount
})
```

### 九、路由【router】（封装好的组件）

##### 1、react-router-dom 基于浏览器环境的开发。

安装：

```
npm install react-router-dom --save
```

##### 2、两个组件（封装好的组件）

```
1、BrowserRouter路由
class BrowserRouter extends React.Component{
    render(){
        
    }
}
2、HashRouter路由
class HashRouter extends React.Component{
    render(){
        
    }
}
```

##### 3、使用

（1）、引入路由配置

import  {HashRouter,Route}  from "react-router-dom";

（2）、配置【在根组件App下配置】

```
class App extends React.Component{
    render(){
        return<div>
            //如果url匹配到path对应的路径，则渲染component对应的组件；
            <Route path="/home" component={Home}/>
            <Route path="/list" component={List}/>
            <Route path="/cart" component={Cart}/>
            <Route path="/xq" component={Xq}/>
        </div>
    }
}
```

3、配置渲染到的节点处【就是像下面这样搞】

```
ReactDOM.render(
    <HashRouter>
    	<App></App>
    </HashRouter>,
    document.querySelector("#app")
)
```

4、实例

​	*在使用Link的时候应该先要引入，
        *import  {HashRouter,Route,Link,NavLink}  from "react-router-dom";
        *最终link会被解析为a标签
        *此时点击就会实现跳转了
        *整个页面只是为了演示，没有引入相关的插件，所以不能执行

```
<script type="text/babel">
			class Nav extends React.Component{
                constructor(){
                    super();
                    this.state={
                        menu:[
                            {
                                text:"首页",
                                path:"home"
                            },{
                                text:"列表",
                                path:"list"
                            },{
                                text:"详情页",
                                path:"goods"
                            },
                            {
                                text:"购物车",
                                path:"cart"
                            }]
                    }
                }
				render(){
					return <div className="main" ref="main">
                        <ul>
                            {
                                this.state.menu.map((item,idx)=>{
                                    return<Link key={idx} to={item.path}>{item.text}</Link>
                                })
                            }
                        </ul>
                    </div>
				}
			}
			class App extends React.Component{
				render(){
					return<Nav>
						<Route path="/home" component={Home}/>
						<Route path="/list" component={List}/>
						<Route path="/cart" component={Cart}/>
						<Route path="/xq" component={Xq}/>
					</Nav>
				}
			}
			ReactDOM.render(
                <HashRouter>
                    <App></App>
                </HashRouter>,
			  document.querySelector("#app")
			)
		</script>
```

5、要想一进入页面就显示主页，则：

```
class App extends React.Component{
    render(){
        return<Nav>
         	<Route path="\/" component={Home} exact/>
            <Route path="/home" component={Home}/>
            <Route path="/list" component={List}/>
            <Route path="/cart" component={Cart}/>
            <Route path="/xq" component={Xq}/>
        </Nav>
    }
}
```

此时当一进入页面就会加载首页，当点击相应的页面又会跳到相对应的页面

exact：精确的，精确匹配，一定要加上这个词

###### 以上的做法还可以这样：

```
class App extends React.Component{
    render(){
        return<Nav>
        //加上switch之后，他会精确匹配，需要跳转到相应的路由之下，它才会显示相对应的页面
        	<Switch>
        	 <Route path="\/home" render={()=><div>在这里有很多操作，可以去掉switch时，保留在每个页面本句话，此时此句话会在每个页面出现</div>} component={Home}/>
                <Route path="/home" component={Home}/>
                <Route path="/list" component={List}/>
                <Route path="/cart" component={Cart}/>
                <Route path="/xq" component={Xq}/>
            </Switch>
        </Nav>
    }
}
```

###### 能量激增：

```
class App extends React.Component{
    render(){
        return<Nav>
        //加上switch之后，他会精确匹配，需要跳转到相应的路由之下，它才会显示相对应的页面
        	<Switch>
        	 <Route path="\/" render={()=><div>现在是去除斜杠下的home，此时本句话会在每一个页面出现</div>} component={Home}/>
                <Route path="/home" component={Home}/>
                <Route path="/list" component={List}/>
                <Route path="/cart" component={Cart}/>
                <Route path="/xq" component={Xq}/>
            </Switch>
        </Nav>
    }
}
```

###### 解决去除斜杠下的home时，每个页面都会显示render里边的内容的问题

```
class App extends React.Component{
    render(){
        return<Nav>
        //加上switch之后，他会精确匹配，需要跳转到相应的路由之下，它才会显示相对应的页面
        	<Switch>
                <Route path="/home" component={Home}/>
                <Route path="/list" component={List}/>
                <Route path="/cart" component={Cart}/>
                <Route path="/xq" component={Xq}/>
                <Route path="\/" render={()=><div>把这句话放在最后边就OK了</div>} component={Home}/>
            </Switch>
        </Nav>
    }
}
```

##### 404不存在；重定向才能够

```
class App extends React.Component{
    render(){
        return<Nav>
            <Switch>
                <Route path="/home" component={Home}/>
                <Route path="/list" component={List}/>
                <Route path="/cart" component={Cart}/>
                <Route path="/xq" component={Xq}/>
                //放在最后边皆可以了
                <Route path="\/" render={()=><div></div>} component={Home}/>
                //404不存在   Bucunzai这是一个组件
                <Route component={Bucunzai}/>
                //重定向，当访问的路径页面不存在时，它就会跑到这个页面
                <Redirect to="/home">
            </Switch>
    	</Nav>
    }
}
```

##### 路由携带参数：【都可以在生命周期中通过props获取】

```
<Link to={{
      pathname: '/pay',
      search: '?sort=name',
      state: { price: 18 }
}} />
```

Navlink产生高亮的效果：

```
class App extends React.Component{
    render(){
        return<div>
        //做判断返回一个布偶值，返回true高亮
           <NavLink to="/list" isActive={()=>{return trun}}/> 
    	</div>
    }
}
```

##### 编程式导航：

![](C:\Users\吕运学\Desktop\React\img\编程式导航.png)

![](C:\Users\吕运学\Desktop\React\img\编程式导航2.png)

### 补充：

### 【1】、排他性路由`<Switch>`[](#switch)

用来包裹Route组件，只渲染出第一个与当前访问地址匹配的 `<Route>` 或 `<Redirect>`（注意顺序问题）

- 用途：
- 渲染单个组件
- 重定向
- 404页面

【2】、声明式导航

利用组件(Link或NavLink)属性实现路由跳转 

#### Link`<Link>`

为你的应用提供声明式，无障碍导航，默认解析成a标签 

to: string

- 作用：跳转到指定路径
- 使用场景：如果只是单纯的跳转就直接用字符串形式的路径。

```
   <Link to="/courses" />
```

to: object

- 作用：携带参数跳转到指定路径
- 作用场景：比如你点击的这个链接将要跳转的页面需要展示此链接对应的内容，又比如这是个支付跳转，需要把商品的价格等信息传递过去。

```
 <Link to={{
      pathname: '/pay',
      search: '?sort=name',
      state: { price: 18 }
    }} />
```

replace: bool

> 为 true 时，点击链接后将使用新地址替换掉上一次访问的地址

#### NavLink`<NavLink>`[](#navlinknavlink)

> 这是 `<Link>`的特殊版，顾名思义这就是为页面导航准备的。因为导航需要有 “激活状态

- activeClassName: string

  > 导航选中激活时候应用的样式名，默认样式名为 active

- activeStyle: object

  > 如果不想使用样式名就直接写style

- to: string|object

  > 同`<Link>`

- isActive: func 通过返回值（boolean）决定导航是否激活，或者在导航激活时候做点别的事情。不管怎样，它不能决定对应页面是否可以渲染。

### 编程式导航[](#_5)

> 利用路由提供的history对象实现路由跳转 *history.push(path)* history.replace(path)

#### 获取history对象[](#history)

- 利用`<Route/>`渲染组件

  > 直接通过props.history获取

- withRouter

  > 利用withRouter高阶组件包装后,直接通过组件的props.history获取，就可以使用编程式导航进行点击跳转

- Context（了解，不推荐）

  > react-router v4 在 Router 组件中通过Contex暴露了一个router对象，router对象下包含history（即：this.context.router.history）

## 嵌套路由[](#_6)

props.match是实现嵌套路由的对象，当我们在某个页面跳转到它的下一级子页面时，我们不会显显性地写出当前页面的路由，而是用match对象的path和url属性。

- match.path：是指写在 `<Route>` 中的 path 参数；
- match.url：是指在浏览器中显示的真实 URL。

> match.path 可用于嵌套的 `<Route>`，而 match.url 可用于嵌套的 `<Link>`

```
<div className="subnav">
    <NavLink to={props.match.url + "/computer"} activeClassName="active">电脑</NavLink>
    <NavLink to={props.match.url + "/pad"} activeClassName="active">平板</NavLink>
    <NavLink to={props.match.url + "/acc"} activeClassName="active">配件</NavLink>
  </div>

  <Switch>
    <Route path={props.match.path + "/phone"} component={Phone}/>
    <Route path={props.match.path + "/computer"} component={Computer}/>
    <Redirect from={props.match.path} to={props.match.path + "/computer"} exact />
    <Route path={props.match.path + "/pad"} component={Pad}/>
    <Route path={props.match.path + "/acc"} component={Acc}/>
  </Switch>
```

## 动态路由[](#_7)

> 在匹配路径path 的后面加上冒号 + 参数， 如`path ="goods/:id"`

- 获取动态id方式： 当渲染组件时，路由会给我们组件注入3个参数（history,location,match），这里使用match 就可以了，它有一个params属性，就是专门获取动态路由参数的

### 六、sass的使用

##### 1、下载

```
npm i -D sass-loader node-sass
```

2、引入