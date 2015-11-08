# Why React？
React 是一個由 Facebook 和 Instagram 用來建立使用者界面的 JavaScript library。很多人認為 React 是 [MVC](http://www.wikiwand.com/en/Model%E2%80%93view%E2%80%93controller) 中的 **V**。

我們建立 React 是為了解決一個問題：**building large applications with data that changes over time.**

## 簡單
簡單的表達出你的應用程式在任一個時間點應該長的樣子，然後當底層的資料改變時，React 會自動處理所有 UI 的更新。

## 聲明式(Declarative)
當資料變化後，React 概念上與點擊“刷新”按鈕類似，但僅會更新變化的部分。

## 構建可組合的元件
React 都是關於建立可重複使用的元件。事實上，透過 React 你*唯一*要做的事情就是建立元件。由於其良好的封裝性，元件使代碼可重複使用、測試和關注分離（separation of concerns）更加簡單。

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
我們始終堅信，元件應該要專注於分離，而不是透過“樣板引擎”和“顯示邏輯”。我們認為標籤和生成它的程式碼是緊密相連的。此外，顯示邏輯通常是很複雜的，透過樣板語言實現這些邏輯會變得笨重。

我們得出解決這個問題最好的方案是透過 JavaScript 直接生成樣板，這樣你就可以用一個真正語言的所有表達能力去建立 UI。

為了使這變得更簡單，我們做了一個非常簡單、可選的類似 HTML 語法，透過函數即可生成樣板的編譯器，稱為 JSX。

**JSX 讓你可以用 HTML 的語法來寫 JavaScript 函數。**要在 React 生成一個連結，透過純的 JavaScript 你可以這麼寫：
`React.createElement('a', {href: 'http://facebook.github.io/react/'}, 'Hello React!')`

透過 JSX 這就變成了：
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

方便起見，你可以創建基於自定義元件的速記工廠方法。

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
如果屬性的值被省略掉了，JSX 會把它當作`true`。要透過`false`屬性表達式必須使用。這個最常用於 HTML 表單元素，配合屬性像是`disabled`,`required`,`checked`和`readOnly`。

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

**Autobinding：**在 JavaScript 裡創建回調的時候，為了保證`this`的正確性，一般都需要明確地綁定方法到它的實例上。有了 React，所有方法被自動綁定到了它的元件實例上(使用 ES6 class 語法時除外)。React 還緩存這些綁定方法，所以 CPU 和內存都是非常高效。而且還能減少打字！

**Event Delegation：**React 實際並沒有把事件處理器綁定到節點本身。當 React 啟動的時候，它在最外層使用唯一一個事件監聽器處理所有事件。當元件被掛載和卸載時，只是在內部映射裡添加或刪除事件處理器。當事件觸發，React 會根據映射知道如何分發(dispatch)。當沒有事件處理器可以映射時，會當作空操作處理。參考 [David Walsh 很棒的文章](http://davidwalsh.name/event-delegate)了解這樣做高效率的原因。

## 元件其實是狀態機（State Machines）
React 把 UIs 當作簡單狀態機。把 UI 想像成擁有不同狀態然後渲染這些狀態，可以輕鬆讓UI 和資料保持一致。

React 裡，只需更新元件的 state，然後根據新的 state 重新渲染 UI。React 來決定如何最高效率地更新 DOM。

## State 工作原理
一般用來通知 React 資料變更的方法是調用`setState(data, callback)`。這個方法會合併（merge）`data`到`this.state`，並重新渲染元件。當元件渲染完成後，會呼叫可選的`callback`。大部分情況下不需要提供`callback`，因為 React 會負責把 UI 更新到最新狀態。

## 哪些元件應該有 State？
大部分元件的工作應該是從`props`裡取資料並渲染出來。然而有時需要對使用者輸入、伺服器請求或者時間變化等作出回應，這時需要使用 state。

**試著盡可能的減少在元件使用 state。** 這樣做能隔離 state，把它放到最合理的地方，也能減少冗餘，同時也易於理解應用程式的運作過程。

常用的模式是建立多個只負責渲染資料的無狀態（stateless）元件，在它們的上層創建一個富有狀態（stateful）的元件並透過把它的 state 傳給子級元件的`props`。這個富有狀態的元間封裝了所有的互動邏輯，而這些無狀態元件則負責明確低地渲染資料。

## 哪些應該在 State 做？
**State 應該包括那些可能被元件的事件處理器改變並觸發 UI 更新的資料。**真實的應用程式中這種資料一般都很小且能被 JSON 序列化。當創建一個富有狀態的元件時，想像一下它的狀態最少需要哪些資料，並只把這些資料存到`this.state`。在`render()`裡再根據 state 來計算你需要的其它資訊。你會發現以這種方式思考和開發應用程式最終往往是正確的，因為如果在 state 裡添加多餘資料或計算資料，需要你經常手動保持資料同步，而不能讓 React 來幫你處理。

## 哪些不應該在 State 做？
`this.state`應該僅包括能表示 UI 的狀態所需的最少資料。因此，它不應該包括：

* **計算所得資料：**不要擔心根據 state 來預先計算資料 —— 把所有的計算都放到`render()`裡更容易保證 UI 和資料的一致性。例如，在 state 裡有一個陣列，我們要把陣列長度渲染成字串，直接在`render()`裡使用`this.state.listItems.length + ' list items'`比把它儲存到 state 裡好的多。
* **React 元件：**在`render()`裡使用當前 props 和 state 來創建它。
* **基於 props 的重複數據：**盡可能使用 props 來作為唯一的資料來源。把 props 保存到 state 的一個有效的場景是需要知道它以前值的時候，因為 props 可能會因為父級元件重新渲染而變化。

# 複合元件 (Multiple Components)
截至目前為止，我們已經學會如何用單個元件來顯示資料和處理使用者輸入。下一步讓我們來體驗 React 最激動人心的特性之一：**可組合性（composability）**。

## 動機：關注分離
透過重複使用那些接口定義良好的元件來開發新的模組化元件，我們得到了與使用函數和 classes　相似的好處。具體來說就是能夠透過開發簡單的元件把程式的*不同關注面分離*。如果為程式開發一套自定義的元件庫，那麼就能以最適合業務場景的方式來展示你的 UI。

## 組合實例
一起來使用 Facebook Graph API 開發可以顯示個人圖片和使用者名的簡單 Avatar 元件吧。

	var Avatar = React.createClass({
		render: function () {
			return (
				<div>
					<ProfilePic username={this.props.username} />
					<ProfileLink username={this.props.username} />
				</div>
			);
		}
	});
	
	var ProfilePic = React.createClass({
		render: function () {
			return (
				<img src={'https://graph.facebook.com/' + this.props.username + '/picture'} />
			);
		}
	});

	var ProfileLink = React.createClass({
		render: function () {
			return (
				<a href={'https://www.facebook.com/' + this.props.username}>
					{this.props.username}
				</a>
			);
		}
	});
	
	ReactDOM.render(
		<Avatar username="pwh" />,
		document.getElementById("example")
	);

## 從屬關係
上面例子中，`Avatar`擁有`ProfilePic`和`ProfileLink`。在 React 中，**擁有者就是給其它元件設置`props`的那個元件。**更正式地說，如果元件`X`是在元件`Y`的`render()`方法中建立的，那麼`Y`就擁有`X`。如同之前講過，元件不能修改自身的`props` - 它們總是與它們擁有者設置的保持一致。這是保持 UIs 一致性的關鍵性原則。

畫出從屬關係與父子關係的區別相當的重要。從屬關係是 React 特有的，而父子關係簡單來講就是 DOM 裡的標籤的關係。在上一個例子中，`Avatar`擁有`div`、`ProfilePic`和`ProfileLink`，`div`是`ProfilePic`和`ProfileLink`的父級（但不是擁有者）。

## 子級
當建立 React 元件實例時，你可以在開始標籤和結束標籤之間引用 React 元件或者Javascript 表達式：

	<Parent><Child /></Parent>

`Parent`能透過專門的`this.props.children`屬性讀取子級。**`this.props.children`是一個不透明的資料結構：**使用 [React.Children 工具](https://facebook.github.io/react/docs/top-level-api.html#react.children)來操作。

### 子級校正（Reconciliation）
**校正就是每次 render 方法調用後 React 更新 DOM 的過程。**一般情況下，子級會根據它們被渲染的順序來做校正。例如，假定有兩個渲染過程生成以下相應的標記：

	// Render Pass 1
	<Card>
	  <p>Paragraph 1</p>
	  <p>Paragraph 2</p>
	</Card>
	// Render Pass 2
	<Card>
	  <p>Paragraph 2</p>
	</Card>

直觀來看，只是刪除了`<p>Paragraph 1</p>`。事實上，React 先更新第一個子級的內容，然後刪除最後一個元件。React 是根據子級的*順序*來校正的。

### 子元件狀態管理
對於大多數元件來說，這沒什麼大礙。但是，對於使用`this.state`在多次渲染過程中維持資料的富有狀態元件，這樣做潛在很多問題。

多數情況下，可以透過隱藏元件來避開這些問題而不是刪除它們。

	// Render Pass 1
	<Card>
	  <p>Paragraph 1</p>
	  <p>Paragraph 2</p>
	</Card>
	// Render Pass 2
	<Card>
	  <p style={{display: 'none'}}>Paragraph 1</p>
	  <p>Paragraph 2</p>
	</Card>

### 動態子級
如果子元件位置會改變（如在搜索結果中）或者有新元件添加到列表開頭（如在串流中）情況會變得更加複雜。如果子級要在多個渲染過程中保持自己的特徵和狀態，在這種情況下，你可以透過給子級設置唯一的`key`值來區分。

	render: function () {
		var results = this.props.results;
		return (
			<ol>
				{results.map(function(result){
					return <li key={result.id}>{result.text}</li>;
				})}
			</ol>
		);
	}

當 React 校正帶有`key`值的子級時，它會確保它們被重新排序（而不是破壞）或者刪除（而不是重用）。

務必把`key`值直接添加到陣列中的元件身上，而不是陣列中每個元件內部最外層的 HTML 上：

	// WRONG!
	var ListItemWrapper = React.createClass({
	  render: function() {
	    return <li key={this.props.data.id}>{this.props.data.text}</li>;
	  }
	});
	var MyComponent = React.createClass({
	  render: function() {
	    return (
	      <ul>
	        {this.props.results.map(function(result) {
	          return <ListItemWrapper data={result}/>;
	        })}
	      </ul>
	    );
	  }
	});

	// Correct :)
	var ListItemWrapper = React.createClass({
	  render: function() {
	    return <li>{this.props.data.text}</li>;
	  }
	});
	var MyComponent = React.createClass({
	  render: function() {
	    return (
	      <ul>
	        {this.props.results.map(function(result) {
	           return <ListItemWrapper key={result.id} data={result}/>;
	        })}
	      </ul>
	    );
	  }
	});

另外也可以傳遞 ReactFragment 物件來做為有`key`的子級。可以在 [Keyed Fragments](https://facebook.github.io/react/docs/create-fragment.html) 看到更多詳細資訊。

## 資料流
React 中，資料流透過上面介紹過的`props`從擁有者到所擁有的元件。這就是高效率的單向資料綁定(one-way data binding)：擁有者透過它的`props`或`state`計算出一些值，並把這些值綁定到它們所擁有元件的`props`上。因為這個過程遞迴般的發生，所以資料變化會自動的在所有被使用的地方反映出來。

## A Note on Performance
你或許會擔心如果一個擁有者有大量子級時，對於資料的變化做出響應會非常耗費性能。好消息是執行 JavaScript 非常的快，而且`render()`方法一般相當簡單，所以在大部分應用程式裡這樣做速度極快。此外，性能上的瓶頸大多是因為 DOM 更新，而非 JS 的執行。React 會透過批量更新和變化檢測來優化性能。

然而有時候需要做細部的性能控制。這種情況下，可以重寫`shouldComponentUpdate()`方法返回`false`來讓 React 跳過對子級的處理。參考 [React reference docs](https://facebook.github.io/react/docs/component-specs.html)了解更多。

> **注意：**  
> 如果在資料變化時讓`shouldComponentUpdate()`返回`false`，React 就不能保證 UI 會同步。當使用它的時候一定確保你清楚到底做了什麼，並且只在遇到明顯性能問題的時候才使用它。不要低估 JavaScript 的速度，DOM 操作通常才是慢的原因。

# 可重用元件 (Reusable Components)
設計接口的時候，把通用的設計元素（按鈕，表單框，佈局元件等）拆成接口良好定義的可重用的元件。這樣，下次開發相同 UI 時就可以寫更少的代碼，也意義著更高的開發效率，更少的Bug 和更少的程式體積。

## Prop 驗證
隨著應用不斷變大，對於確保元件被正確使用變得非常有用。為此我們讓你可以設定`propTypes`。`React.PropTypes`提供很多驗證器(validator)來驗證傳入資料的有效性。當向`props`傳入無效資料時，JavaScript console 會拋出警告。注意為了性能考慮，只在開發環境驗證`propTypes`。下面用例子來說明不同驗證器的區別：

	React.createClass({
	  propTypes: {
	    // 可以宣告 prop 為指定的 JS 基本類型
	    // 默認下，這些 prop 不是一定需要使用的
	    optionalArray: React.PropTypes.array,
	    optionalBool: React.PropTypes.bool,
	    optionalFunc: React.PropTypes.func,
	    optionalNumber: React.PropTypes.number,
	    optionalObject: React.PropTypes.object,
	    optionalString: React.PropTypes.string,
	
	    // Anything that can be rendered: numbers, strings, elements or an array
	    // (or fragment) containing these types.
	    optionalNode: React.PropTypes.node,
	
	    // A React element.
	    optionalElement: React.PropTypes.element,
	
	    // You can also declare that a prop is an instance of a class. This uses
	    // JS's instanceof operator.
	    optionalMessage: React.PropTypes.instanceOf(Message),
	
	    // You can ensure that your prop is limited to specific values by treating
	    // it as an enum.
	    optionalEnum: React.PropTypes.oneOf(['News', 'Photos']),
	
	    // An object that could be one of many types
	    optionalUnion: React.PropTypes.oneOfType([
	      React.PropTypes.string,
	      React.PropTypes.number,
	      React.PropTypes.instanceOf(Message)
	    ]),
	
	    // An array of a certain type
	    optionalArrayOf: React.PropTypes.arrayOf(React.PropTypes.number),
	
	    // An object with property values of a certain type
	    optionalObjectOf: React.PropTypes.objectOf(React.PropTypes.number),
	
	    // An object taking on a particular shape
	    optionalObjectWithShape: React.PropTypes.shape({
	      color: React.PropTypes.string,
	      fontSize: React.PropTypes.number
	    }),
	
	    // You can chain any of the above with `isRequired` to make sure a warning
	    // is shown if the prop isn't provided.
	    requiredFunc: React.PropTypes.func.isRequired,
	
	    // A value of any data type
	    requiredAny: React.PropTypes.any.isRequired,
	
	    // You can also specify a custom validator. It should return an Error
	    // object if the validation fails. Don't `console.warn` or throw, as this
	    // won't work inside `oneOfType`.
	    customProp: function(props, propName, componentName) {
	      if (!/matchme/.test(props[propName])) {
	        return new Error('Validation failed!');
	      }
	    }
	  },
	  /* ... */
	});

默認Prop 值
React支持以聲明式的方式來定義props的默認值。

var  ComponentWithDefaultProps  =  React . createClass ({ 
  getDefaultProps :  function ()  { 
    return  { 
      value :  'default value' 
    }; 
  } 
  /* ... */ 
});
當父級沒有傳入props時，getDefaultProps()可以保證 this.props.value有默認值，注意getDefaultProps的結果會被緩存。得益於此，你可以直接使用props，而不必寫手動編寫一些重複或無意義的代碼。

傳遞Props：小技巧
有一些常用的React組件只是對HTML做簡單擴展。通常，你想少寫點代碼來把傳入組件的props複製到對應的HTML元素上。這時JSX的spread語法會幫到你：

var  CheckLink  =  React . createClass ({ 
  render :  function ()  { 
    //這樣會把CheckList所有的props複製到<a> 
    return  < a  {... this . props } > { '√ ' }{ this . props . children } < /a>; 
  } 
});

React . render ( 
  < CheckLink  href = "/checked.html" > 
    Click  here ! 
  < /CheckLink>, 
  document . getElementById ( 'example' ) 
);
單個子級
React.PropTypes.element可以限定只能有一個子級傳入。

var  MyComponent  =  React . createClass ({ 
  propTypes :  { 
    children :  React . PropTypes . element . isRequired 
  },

  render :  function ()  { 
    return  ( 
      < div > 
        { this . props . children }  //有且僅有一個元素，否則會拋異常。
      < /div> 
    ); 
  }

});
Mixins
組件是React裡復用代碼最佳方式，但是有時一些複雜的組件間也需要共用一些功能。有時會被稱為跨切面關注點。React使用mixins來解決這類問題。

一個通用的場景是：一個組件需要定期更新。用setInterval()做很容易，但當不需要它的時候取消定時器來節省內存是非常重要的。React提供生命週期方法來告知組件創建或銷毀的時間。下面來做一個簡單的mixin，使用setInterval()並保證在組件銷毀時清理定時器。

var  SetIntervalMixin  =  { 
  componentWillMount :  function ()  { 
    this . intervals  =  []; 
  }, 
  setInterval :  function ()  { 
    this . intervals . push ( setInterval . apply ( null ,  arguments )); 
  }, 
  componentWillUnmount :  function ()  { 
    this . intervals . map ( clearInterval ); 
  } 
};

var  TickTock  =  React . createClass ({ 
  mixins :  [ SetIntervalMixin ],  //引用mixin 
  getInitialState :  function ()  { 
    return  { seconds :  0 }; 
  }, 
  componentDidMount :  function ()  { 
    this . setInterval ( this . tick ,  1000 );  //調用mixin的方法
  }, 
  tick :  function ()  { 
    this . setState ({ seconds :  this . state . seconds  +  1 }); 
  }, 
  render :  function ()  { 
    return  ( 
      < p > 
        React  has  been  running  for  { this . state . seconds }  seconds . 
      < /p> 
    ); 
  } 
});

React . render ( 
  < TickTock  /> , 
  document . getElementById ( 'example' ) 
);
關於mixin 值得一提的優點是，如果一個組件使用了多個mixin，並且有多個mixin 定義了同樣的生命週期方法（如：多個mixin 都需要在組件銷毀時做資源清理操作），所有這些生命週期方法都保證會被執行到。方法執行順序是：首先按mixin 引入順序執行mixin 裡方法，最後執行組件內定義的方法。


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