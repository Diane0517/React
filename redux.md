Redux
======
1.React 和 Redux
---------

      React 是单向数据流，由父组件流向子组件。如果2个非父子组件之间想要通信，就会有问题。为了解决这个问题，react提出设置一个全局的事件管理系统Flux。
    而Redux也是这样的。Redux把应用的状态（state）统一到一个地方来管理，也就是store。组件需要把自己的state  dispatch（发布）到store，
    而需要对应state的组件，则需要订阅（subscribe）对应的store中对应的state。
      关于二者的区别，Flux是一种设计模式，而Redux则是一个工具，来源于Flux，又不同。区别有以下3点：
      
      
    1.单一真实的数据来源
      Redux只有一个store来存储，管理整个应用的state。
      
    2.状态是只读的
        store提供来4个API：
        dispatch（action）
        subscribe（listener）
        getState（）
        replaceReducer（nextReducer）
        应用是无法直接更改状态的，如果想改变状态，则需要主动触发一个action，action中有具体的type,然后去改变store中的state。
        
    3.状态的改变是由纯函数完成的
        想改变state，需要触发action。而触发的action最终会发送到reducer里。reducer是会接收参数，返回新的state。之所以说reducer是纯函数，是因 为         它不会直接发送请求，返回值取决于接收的参数，并且接收的参数不会被改变。
          
 2.Redux
 ------
    1.创建store
      用到的方法是createStore（）；
      
      import {createStore} from ‘redux'；
      
      调用这个方法的时候，需要把所有的reducer都作为参数传过来，然后创建一个store。
    
    2.combineReducers
      允许我们根据不同的reducer来描述不同的store，然后把store中的状态和reducer对应起来。不能直接改变原来的state，所以只能返回新的state。
      
      Object.assign({},state,{foo:'123'});
      
    3.connect()
      React的组件和Redux可以通过这个方法连接起来，借助connect（）方法，接收2个参数，在实际项目，mapStateToProps（）这个函数作为参数传入。而这个函数的作用就是提取store 中的state，获取到当前组件需要的state。
      
      module.exports = connect(mapStateToProps)(Header)
 
      然后header这个组件就可以直接使用this.state.props...来获取对应的state里的数据
      
    4.Provider
    
      <Provider></Provider>组件，包含整个应用，而store被绑定在来provider上。
      例如：
      
      ReactDom.render(
        <Provider store={store}>
          <Homepage />
           document.getElementById('app')
        </Provider>
      );
      
      
    5.组件container和component
      
      组件分为‘可视化组件‘ 和 ’容器组件‘
      
      1.可视化组件（components）
        可视化组件，仅仅是为了渲染页面而存在，也就是我们看到的html结构。它不知道获取的数据是什么样的，也不知道数据来源，不知道数据的变化，也不能去改变props的数据，只负责渲染。
        
      2.容器组件（container） 
        又称为“智能组件”，常作为可视化组件的父组件出现。负责数据的传递，更改。
      
      
      
      
    
              
