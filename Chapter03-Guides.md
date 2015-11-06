# Why React？
React 是一個由 Facebook 和 Instagram 用來建立使用者界面的 JavaScript library。很多人認為 React 是 [MVC](http://www.wikiwand.com/en/Model%E2%80%93view%E2%80%93controller) 中的 **V**。

我們建立 React 是為了解決一個問題：**building large applications with data that changes over time.**

## 簡單
簡單的表達出你的應用程式在任一個時間點應該長的樣子，然後當底層的資料改變時，React 會自動處理所有 UI 的更新。

## 聲明式(Declarative)
當資料變化後，React 概念上與點擊“刷新”按鈕類似，但僅會更新變化的部分。

## 構建可組合的組件
React 都是關於建立可重複使用的元件。事實上，通過 React 你*唯一*要做的事情就是建立元件。由於其良好的封裝性，元件使代碼可重複使用、測試和關注分離（separation of concerns）更加簡單。

## 給它5分鐘的時間
React 挑戰了很多傳統的知識，第一眼看上去可能很多想法有點瘋狂。當你閱讀這篇指南，請[給它5分鐘的時間](https://signalvnoise.com/posts/3124-give-it-five-minutes)；那些瘋狂的想法已經幫助 Facebook 和 Instagram 從裡到外建立了上千個元件了。

## 了解更多
你可以從[這篇部落格](https://facebook.github.io/react/blog/2013/06/05/why-react.html)了解更多我們創造 React 的動機。

---

# 呈現資料
UI 能做的最基礎的事就是呈現一些資料。React 讓顯示資料變得簡單，當資料變化時，UI 會自動同步更新。

## Getting Started
讓我們看一個非常簡單的例子。新建一個名為`hello-react.html`的文件，內容如下：

	<!DOCTYPE html>
	<html>
	  <head>
	    <meta charset="UTF-8" />
	    <title>Hello React</title>
	    <script src="https://fb.me/react-0.14.1.js"></script>
	    <script src="https://fb.me/react-dom-0.14.1.js"></script>
	    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.23/browser.min.js"></script>
	  </head>
	  <body>
	    <div id="example"></div>
	    <script type="text/babel">
	
	      // ** Your code goes here! **
	
	    </script>
	  </body>
	</html>

在接下去的文件中，我們只關注 JavaScript 代碼，假設我們把代碼插入到上面那個模板中。用下面的 JSX 替換上面用來佔位的註釋。

	var HelloWorld = React.createClass({
	  render: function() {
	    return (
	      <p>
	        Hello, <input type="text" placeholder="Your name here" />!
	        It is {this.props.date.toTimeString()}
	      </p>
	    );
	  }
	});
	
	setInterval(function() {
	  ReactDOM.render(
	    <HelloWorld date={new Date()} />,
	    document.getElementById('example')
	  );
	}, 500);

## 響應式更新(Reactive Updates)
在瀏覽器中打開`hello-react.html`，並在輸入框輸入你的名字。你會發現 React 在 UI 只改變了時間，你在輸入框的輸入內容會保留著，即使你沒有寫任何程式碼來完成這個功能。React 也為你解決了這個問題。

我們想到的解決方案是讓 React 不去操作 DOM，除非不得不操作 DOM。它用一種更快的內置仿造的 DOM 來操作差異，為你計算出效率最高的 DOM 變化。

這個元件的輸入被稱為`props` － "properties" 的縮寫。它們在 JSX 語法中當作屬性來傳遞。你必須知道，在元件裡這些屬性是不可直接變更的，也就是說`this.props`是唯讀的。

## 元件就像是函數
React 元件非常簡單。你可以把它們當作是簡單的函數，接受`props`和`state`(後面會討論)作為參數，然後渲染出 HTML。把這記在心裡，元件就會非常容易理解。

> 注意：  
> **One limitation**：React 元件只能渲染單個根節點。如果你想要返回多個節點，它們必須被包含在同一個節點裡。

## JSX 語法
我們始終堅信，元件應該要專注於分離，而不是通過“樣板引擎”和“顯示邏輯”。我們認為標籤和生成它的程式碼是緊密相連的。此外，顯示邏輯通常是很複雜的，通過樣板語言實現這些邏輯會變得笨重。

我們得出解決這個問題最好的方案是通過 JavaScript 直接生成樣板，這樣你就可以用一個真正語言的所有表達能力去建立 UI。

為了使這變得更簡單，我們做了一個非常簡單、可選的類似 HTML 語法，通過函數即可生成樣板的編譯器，稱為 JSX。

**JSX 讓你可以用 HTML 的語法來寫 JavaScript 函數。**要在 React 生成一個連結，通過純的 JavaScript 你可以這麼寫：
`React.createElement('a', {href: 'http://facebook.github.io/react/'}, 'Hello React!')`

通過 JSX 這就變成了：
`<a href="http://facebook.github.io/react/">Hello React!</a>`

我們發現這會使建立 React 應用程式更加簡單，設計師也偏向使用這種語法，但是每個人都有自己的工作流，所以 **JSX 並不是強制要求使用的。**

JSX 非常小。想學習更多的話，可以看 [JSX in depth](https://facebook.github.io/react/docs/jsx-in-depth.html)。Or see the transform in action in [the Babel REPL](https://babeljs.io/repl/).

JSX 類似於HTML，但不是完全一樣。參考 [JSX 陷阱](https://facebook.github.io/react/docs/jsx-gotchas.html)學習重要的區別。

[Babel 提供了許多種的入門使用 JSX 的方式](http://babeljs.io/docs/setup/)。範圍從命令行到 Ruby on Rails，選擇最適合你工作的工具。

## 沒有 JSX 的 React
你完全可以選擇是否使用 JSX，不一定要用來寫 React。你可以在純的 JavaScript 套過 `React.createElement`來建立 React 元件，可以帶入標籤名、元件、物件屬性和多種的可選子參數。

	var child1 = React.createElement('li', null, 'First Text Content');
	var child2 = React.createElement('li', null, 'Second Text Content');
	var root = React.createElement('ul', { className: 'my-list' }, child1, child2);
	ReactDOM.render(root, document.getElementById('example'));

方便起見，你可以創建基於自定義組件的速記工廠方法。

	var Factory = React.createFactory(ComponentClass);
	...
	var root = Factory({ custom: 'prop' });
	ReactDOM.render(root, document.getElementById('example'));
	
React 已經為 HTML 標籤提供內置工廠方法。

	var root = React.DOM.ul({ className: 'my-list' },
	             React.DOM.li(null, 'Text Content')
	           );
	           
# 資料呈現 - JSX in Depth
JSX 是一個看起來很像 XML 的 JavaScript 語法擴充。React 可以用來做簡單的 JSX 句法轉換。

## 為什麼要使用 JSX？
你不需要為了 React 使用JSX，可以直接使用純粹的 JS。然而我們建議使用 JSX，因為它是簡潔且熟悉用來定義樹狀結構且帶有屬性的語法。

對於非專職開發者（比如設計師）同樣比較熟悉。

XML 有固定的開啟和閉合標籤。這能讓複雜的樹更易於閱讀，優於方法調用和 object literals。

它沒有修改 JavaScript 語義。

## HTML 標籤 vs. React 元件
React 可以渲染 HTML 標籤(strings) 或 React 元件(classes)。  
要渲染 HTML 標籤，只需在 JSX 裡使用小寫字母開頭的標籤名。

	var myDivElement = <div className="foo" />;
	ReactDOM.render(myDivElement, document.getElementById('example'));

要渲染 React 元件，只需創建一個大寫字母開頭的本地變數。

	var MyComponent = React.createClass({/*...*/});
	var myElement = <MyComponent someProperty={true} />;
	ReactDOM.render(myElement, document.getElementById('example'));

React 的 JSX 裡約定使用首字母大、小寫來區分本地元件的 classes 和 HTML 標籤。

> **注意：**  
> 由於 JSX 就是 JavaScript，一些標識符像`class`和`for`不建議作為 XML 屬性名。作為替代，React DOM 元件使用`className`和`htmlFor`來做對應的屬性。

## 轉換
React JSX 把類 XML 的語法轉成純粹 JavaScript，XML 元素、屬性和子節點被轉換成`React.createElement`的參數。

	var Nav;
	// Input (JSX):
	var app = <Nav color="blue" />;
	// Output (JS):
	var app = React.createElement(Nav, {color:"blue"});

注意，要想使用`<Nav />`，`Nav`變數一定要在作用區間內。  
JSX 也支援使用 XML 語法定義子結點：

	var Nav, Profile;
	// Input (JSX):
	var app = <Nav color="blue"><Profile>click</Profile></Nav>;
	// Output (JS):
	var app = React.createElement(
	  Nav,
	  {color:"blue"},
	  React.createElement(Profile, null, "click")
	);

JSX 當 displayName 是`undefined`，將會從變數賦值判斷 class 的 [displayName](https://facebook.github.io/react/docs/component-specs.html#displayname)

	// Input (JSX):
	var Nav = React.createClass({ });
	// Output (JS):
	var Nav = React.createClass({displayName: "Nav", });

使用 [Babel REPL](https://babeljs.io/repl/) 來試用 JSX 並理解它是如何轉換到原生 JavaScript，還有 [HTML 到 JSX 轉換器](https://facebook.github.io/react/html-jsx.html)來把現有 HTML 轉成 JSX。

如果你要使用 JSX，這篇[新手入門](https://facebook.github.io/react/docs/getting-started.html)教程來教你如何搭建環境。

> **注意：**  
> JSX 表達式總是會當作 ReactElement 執行。具體的實際細節可能不同。一種優化的模式是把 ReactElement 當作一個行內的對象字面量形式來繞過`React.createElement`裡的校驗代碼。

## 命名空間的元件
如果你正在建立有許多子節點的元件，像是表單。你可能最後會有很多變數宣告。

	// Awkward block of variable declarations
	var Form = MyFormComponent;
	var FormRow = Form.Row;
	var FormLabel = Form.Label;
	var FormInput = Form.Input;
	
	var App = (
	  <Form>
	    <FormRow>
	      <FormLabel />
	      <FormInput />
	    </FormRow>
	  </Form>
	);

為了使其更簡單，更容易。命名空間元件讓你使用一個元件，它把其他元件當作屬性。

	var Form = MyFormComponent;
	
	var App = (
	  <Form>
	    <Form.Row>
	      <Form.Label />
	      <Form.Input />
	    </Form.Row>
	  </Form>
	);

要做到這一點，你只需要建立你的"子元件"當作主元件的屬性。

	var MyFormComponent = React.createClass({ ... });
	
	MyFormComponent.Row = React.createClass({ ... });
	MyFormComponent.Label = React.createClass({ ... });
	MyFormComponent.Input = React.createClass({ ... });

JSX 將會在編譯程式碼時處理成正確的原生 JavaScript。

	var App = (
	  React.createElement(Form, null,
	    React.createElement(Form.Row, null,
	      React.createElement(Form.Label, null),
	      React.createElement(Form.Input, null)
	    )
	  )
	);

> **Note：**  
> 這項功能只在 [v0.11](https://facebook.github.io/react/blog/2014/07/17/react-v0.11.html#jsx) 以上

## JavaScript 表達式
### 屬性表達式
要使用 JavaScript 表達式作為屬性值，只需把這個表達式用一對大括號(`{}`)包起來，不要用引號(`""`)。

	// Input (JSX):
	var person = <Person name={window.isLoggedIn ? window.name : ''} />;
	// Output (JS):
	var person = React.createElement(
	  Person,
	  {name: window.isLoggedIn ? window.name : ''}
	);

### 布林屬性
如果屬性的值被省略掉了，JSX 會把它當作`true`。要通過`false`屬性表達式必須使用。這個最常用於 HTML 表單元素，配合屬性像是`disabled`,`required`,`checked`和`readOnly`。

	// These two are equivalent in JSX for disabling a button
	<input type="button" disabled />;
	<input type="button" disabled={true} />;
	
	// And these two are equivalent in JSX for not disabling a button
	<input type="button" />;
	<input type="button" disabled={false} />;

### 子節點表達式
同樣地，JavaScript 表達式可用於描述子結點：

	// Input (JSX):
	var content = <Container>{window.isLoggedIn ? <Nav /> : <Login />}</Container>;
	// Output (JS):
	var content = React.createElement(
	  Container,
	  null,
	  window.isLoggedIn ? React.createElement(Nav) : React.createElement(Login)
	);

### 註釋
JSX 裡添加註釋很容易；它們只是 JS 表達式而已。你只需要在一個標籤的子節點內(非最外層)小心地用`{}`包圍要註釋的部分。

	var content = (
	  <Nav>
	    {/* child comment, put {} around */}
	    <Person
	      /* multi
	         line
	         comment */
	      name={window.isLoggedIn ? window.name : ''} // end of line comment
	    />
	  </Nav>
	);

> **注意：**  
> JSX 類似於 HTML，但不完全一樣。參考 [JSX 陷阱](https://facebook.github.io/react/docs/jsx-gotchas.html)了解主要不同。

# 資料呈現 - JSX 擴展屬性
如果你事先知道元件需要的全部（屬性），JSX 很容易地這樣寫：
`var component = <Component foo={x} bar={y} />;`

## 修改Props 是不好的
如果你不知道要設置哪些屬性，你可能之後在物件上添加

	var component = <Component />;
	component.props.foo = x; // bad
	component.props.bar = y; // also bad

這樣是反模式，因為 React 不能幫你檢查屬性類型（propTypes）。這樣即使你的屬性類型有錯誤也不能得到清晰的錯誤提示。

Props 應該被當作禁止修改的。修改 props 對象可能會導致預料之外的結果，所以最好不要去修改 props。

## 延展屬性（Spread Attributes）
現在你可以使用 JSX 的新特性 - 延展屬性：

	var props = {};
  	props.foo = x;
  	props.bar = y;
  	var component = <Component {...props} />;

傳入到物件的屬性會被複製到元件的 props 內。  
它能被多次使用，也可以和其它屬性一起用。注意順序很重要，後面的會覆蓋掉前面的。

	var props = { foo: 'default' };
  	var component = <Component {...props} foo={'override'} />;
  	console.log(component.props.foo); // 'override'

## 這個奇怪的...標記是什麼？
這個`...`操作符（也被叫做延展操作符 － spread operator）已經在 [ES6 陣列](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)支援。相關的還有 ES7 規範草案中的 [Object Rest and Spread Properties](https://github.com/sebmarkbage/ecmascript-rest-spread)。我們利用了這些還在製定中標準中已經被支持的特性來使 JSX 擁有更優雅的語法。

# 資料呈現 - JSX 陷阱
JSX 與 HTML 非常相似，但是有些主要的不同點要注意。

> **注意：**  
> 關於 DOM 的區別，如行內`style`屬性，參考[這裡](https://facebook.github.io/react/docs/dom-differences.html)

## HTML 實體
HTML 實體可以插入到 JSX 的文本中：  
`<div>First &middot; Second</div>`

如果想要在 JSX 中顯示 HTML 實體，可能會遇到二次轉譯的問題。因為 React 為了防止各種 XSS 攻擊，預設會轉譯所以字符串。

	// Bad: It displays "First &middot; Second"
	<div>{'First &middot; Second'}</div>

有很多種避開這些問題的方法，最簡單的就是直接在 JavaScript 使用 Unicode。但需要確保檔案是 UTF-8 編碼而且瀏覽器也指定使用 UTF-8 編碼。

	<div>{'First · Second'}</div>

更安全的做法是找到[實體的 Unicode 編碼](http://www.fileformat.info/info/unicode/char/b7/index.htm)，然後在 JavaScript 字符串裡使用。

	<div>{'First \u00b7 Second'}</div>
	<div>{'First ' + String.fromCharCode(183) + ' Second'}</div>

可以在陣列裡混合使用字符串和 JSX 元素。

	<div>{['First ', <span>&middot;</span>, ' Second']}</div>

萬不得已，可以使用[原始的 HTML](https://facebook.github.io/react/tips/dangerously-set-inner-html.html)。

	<div dangerouslySetInnerHTML={{__html: 'First &middot; Second'}} />

## 自定義 HTML 屬性
如果向原生 HTML 元素傳遞不屬於 HTML 規範內的屬性，React 不會渲染它們。如果想要使用自定義的屬性，則需要加上前綴詞`data-`。

	<div data-custom-attribute="foo" />

以 `aria-` 開頭的 [Web Accessibility](http://www.w3.org/WAI/intro/aria) 屬性可以正常使用。

	<div aria-hidden={true} />

# Interactivity and Dynamic UIs
我們已經[學會如何使用 React 呈現數據](https://facebook.github.io/react/docs/displaying-data.html)。現在讓我們來學習如何建立互動的 UIs。

## 簡單例子
	var LikeButton = React.createClass({
	  getInitialState: function() {
	    return {liked: false};
	  },
	  handleClick: function(event) {
	    this.setState({liked: !this.state.liked});
	  },
	  render: function() {
	    var text = this.state.liked ? 'like' : 'haven\'t liked';
	    return (
	      <p onClick={this.handleClick}>
	        You {text} this. Click to toggle.
	      </p>
	    );
	  }
	});
	
	ReactDOM.render(
	  <LikeButton />,
	  document.getElementById('example')
	);

## 事件處理與合成事件（Synthetic Events）
React 裡只需把事件處理器（event handler）以駱峰式命名（camelCased）當作元件的 props 傳入即可，就像使用普通 HTML 那樣。React 內部創建一套合成事件系統來使所有事件在 IE8 和以上瀏覽器表現一致。也就是說，React 知道如何找出和捕獲事件，而且你的事件處理器接收到的 events 參數與 [W3C 規範](http://www.w3.org/TR/DOM-Level-3-Events/)一致，無論你使用哪種瀏覽器。

如果需要在手機或平板等觸控設備上使用 React，需要調用`React.initializeTouchEvents(true);`啟用觸控事件處理。

## 幕後原理：自動綁定和事件代理
在幕後，React 做了一些操作來讓程式碼高效​​運行且易於理解。

**Autobinding：**在 JavaScript 裡創建回調的時候，為了保證this的正確性，一般都需要顯式地綁定方法到它的實例上。有了React，所有方法被自動綁定到了它的組件實例上。React還緩存這些綁定方法，所以CPU和內存都是非常高效。而且還能減少打字！

**Event Delegation：** React實際並沒有把事件處理器綁定到節點本身。當React啟動的時候，它在最外層使用唯一一個事件監聽器處理所有事件。當組件被加載和卸載時，只是在內部映射裡添加或刪除事件處理器。當事件觸發，React根據映射來決定如何分發。當映射里處理器時，會當作空操作處理。參考David Walsh很棒的文章了解這樣做高效的原因。

組件其實是狀態機（State Machines）
React 把用戶界面當作簡單狀態機。把用戶界面想像成擁有不同狀態然後渲染這些狀態，可以輕鬆讓用戶界面和數據保持一致。

React 裡，只需更新組件的state，然後根據新的state 重新渲染用戶界面（不要操作DOM）。React 來決定如何最高效地更新DOM。

State 工作原理
常用的通知React數據變化的方法是調用setState(data, callback)。這個方法會合併（merge）data到this.state，並重新渲染組件。渲染完成後，調用可選的callback回調。大部分情況下不需要提供callback，因為React會負責把界面更新到最新狀態。

哪些組件應該有State？
大部分組件的工作應該是從props裡取數據並渲染出來。但是，有時需要對用戶輸入、服務器請求或者時間變化等作出響應，這時才需要使用State。

** 嘗試把盡可能多的組件無狀態化。** 這樣做能隔離state，把它放到最合理的地方，也能減少冗餘，同時易於解釋程序運作過程。

常用的模式是創建多個只負責渲染數據的無狀態（stateless）組件，在它們的上層創建一個有狀態（stateful）組件並把它的狀態通過props傳給子級。這個有狀態的組件封裝了所有用戶的交互邏輯，而這些無狀態組件則負責聲明式地渲染數據。

哪些應該作為State？
State應該包括那些可能被組件的事件處理器改變並觸髮用戶界面更新的數據。真實的應用中這種數據一般都很小且能被JSON序列化。當創建一個狀態化的組件時，想像一下表示它的狀態最少需要哪些數據，並只把這些數據存入this.state。在render()裡再根據state來計算你需要的其它數據。你會發現以這種方式思考和開發程序最終往往是正確的，因為如果在state裡添加冗餘數據或計算所得數據，需要你經常手動保持數據同步，不能讓React來幫你處理。

哪些不應該作為State？
this.state應該僅包括能表示用戶界面狀態所需的最少數據。因此，它不應該包括：

計算所得數據：不要擔心根據state來預先計算數據——把所有的計算都放到render()裡更容易保證用戶界面和數據的一致性。例如，在state裡有一個數組（listItems），我們要把數組長度渲染成字符串，直接在render()裡使用this.state.listItems.length + ' list items'比把它放到state裡好的多。
React組件：在render()裡使用當前props和state來創建它。
基於props的重複數據：盡可能使用props來作為惟一數據來源。把props保存到state的一個有效的場景是需要知道它以前值的時候，因為未來的props可能會變化。







# Multiple Components
# Reusable Components
# Transferring Props
# Forms
# Working With the Browser
# Working With the Browser - Refs to Components
# Tooling Integration
# Add-Ons
# Add-Ons - Animation
# Add-Ons - Two-Way Binding Helpers
# Add-Ons - Test Utilities
# Add-Ons - Cloning Elements
# Add-Ons - Keyed Fragments
# Add-Ons - Immutability Helpers
# Add-Ons - PureRenderMixin
# Add-Ons - Performance Tools
# Advanced Performance
# Context