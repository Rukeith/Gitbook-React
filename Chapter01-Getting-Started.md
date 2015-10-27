# React.js Getting Started
React 元件套過`render()`的方法，接受輸入的資料和回傳顯示。範例中使用一種類似於 XML 格式叫做 JSX，輸入的資料套過`render()`傳入元件候，儲存於`this.props`。其中 React 並不一定要使用 JSX。

	var HelloMessage = React.createClass({
	  render: function() {
	    return <div>Hello {this.props.name}</div>;
	  }
	});
	
	React.render(<HelloMessage name="John" />, mountNode);

## 一個有狀態的組件
除了​​接受輸入數據（通過`this.props`），元件還可以保持內部狀態數據（通過`this.state`）。當一個元件的狀態資料變化，渲染的標記將被重新調用`render()`更新畫面。

	var Timer = React.createClass({
	  getInitialState: function() {
	    return {secondsElapsed: 0};
	  },
	  tick: function() {
	    this.setState({secondsElapsed: this.state.secondsElapsed + 1});
	  },
	  componentDidMount: function() {
	    this.interval = setInterval(this.tick, 1000);
	  },
	  componentWillUnmount: function() {
	    clearInterval(this.interval);
	  },
	  render: function() {
	    return (
	      <div>Seconds Elapsed: {this.state.secondsElapsed}</div>
	    );
	  }
	});
	
	React.render(<Timer />, mountNode);

## 一個應用程式
使用`props`和`state`，可以組合構建出一個小型的 Todo 應用程式。下面例子使用`state`去追蹤當前列表的項目以及使用者已經輸入的文本。儘管事件綁定似乎是以內聯的方式，但它們將被收集起來並以事件代理的方式實現。

	var TodoList = React.createClass({
	  render: function() {
	    var createItem = function(itemText) {
	      return <li>{itemText}</li>;
	    };
	    return <ul>{this.props.items.map(createItem)}</ul>;
	  }
	});
	var TodoApp = React.createClass({
	  getInitialState: function() {
	    return {items: [], text: ''};
	  },
	  onChange: function(e) {
	    this.setState({text: e.target.value});
	  },
	  handleSubmit: function(e) {
	    e.preventDefault();
	    var nextItems = this.state.items.concat([this.state.text]);
	    var nextText = '';
	    this.setState({items: nextItems, text: nextText});
	  },
	  render: function() {
	    return (
	      <div>
	        <h3>TODO</h3>
	        <TodoList items={this.state.items} />
	        <form onSubmit={this.handleSubmit}>
	          <input onChange={this.onChange} value={this.state.text} />
	          <button>{'Add #' + (this.state.items.length + 1)}</button>
	        </form>
	      </div>
	    );
	  }
	});
	
	React.render(<TodoApp />, mountNode);

## 一個使用外部插件的組件
React 是靈活的，並且提供 hooks 讓你跟其他 library 和 framework 串接。下面例子展現了一個案例，使用外部 Markdown library 實作即時轉換 textarea 的值。

	var converter = new Showdown.converter();
	
	var MarkdownEditor = React.createClass({
	  getInitialState: function() {
	    return {value: 'Type some *markdown* here!'};
	  },
	  handleChange: function() {
	    this.setState({value: this.refs.textarea.getDOMNode().value});
	  },
	  render: function() {
	    return (
	      <div className="MarkdownEditor">
	        <h3>Input</h3>
	        <textarea
	          onChange={this.handleChange}
	          ref="textarea"
	          defaultValue={this.state.value} />
	        <h3>Output</h3>
	        <div
	          className="content"
	          dangerouslySetInnerHTML={{
	            __html: converter.makeHtml(this.state.value)
	          }}
	        />
	      </div>
	    );
	  }
	});
	
	React.render(<MarkdownEditor />, mountNode);