
1. 入口文件 index.js
2. React中的组件继承自React.Component类；
    组件中的内容定义在render函数的返回值中，返回值加小括号可以返回多行内容。
3. ReactDOM的render方法可以把一个组件挂载到一个dom节点上
4. JSX语法不需要加引号，直接写html标签即可
5. 自定义组件必须以大写字母开头
6. react组件规定只能有一个根元素，Fragment标签可以作为组件的根元素，并且不用创建多余标签。
7. 在JSX中使用js的变量需要加{}。
8. 在react中，组件中定义的数据都保存在组件的状态state中
9. 使用JSX绑定事件，第二个单词的字母要大写，例如：onChange。
10. 在绑定的事件中如果要执行自定义的方法，需要为该方法绑定this，把当前组件（this）bind到该方法上，在方法中才能调用，否则this=undefined。 
    例如：onChange={this.handleChange.bind(this)}	//JSX事件绑定
            //定义事件绑定触发时的方法
            handleChange(e){
            e.target  		   // 是当前dom对象
            this.setState({})  // this是在JSX中事件触发时绑定
            }
11. 如果要修改状态state中的值，要使用setState方法
12. Es6解构赋值；
        …this.state.list	展开运算符，把list数组中的值列举出来生成一个新的数组。
13. immutable的概念，react中不允许直接修改state中的内容，如果要修改，可以先创建一个副本，修改副本中的内容，在把副本复制给原始值。直接修改会影响后期的性能优化。
14. JSX中的注释
    {
        //单行注释
    }
    { /* 多行注释 */ }
15.  JSX中的样式名为className，如果使用class会和组件中的class关键字冲突；label标签的for属性用htmlFor替换。
16. 在JSX中如果不希望内容被转义，使用dangerousSetInnerHTML={{__html:item}}
		例如：我们在输入框中输入<h1>hello world</h1>如果我们不希望h1标签被转义，使用上面的属性，最外层的大括号表示里面是js表达式，里面的大括号代表说一个js对象。__html（双下划线）为属性名，item为要设置的值。