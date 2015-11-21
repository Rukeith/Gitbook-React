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

> **Note：**  
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

> **Note：**  
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

> **Note：**  
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

> **Note：**  
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

> **Note：**  
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

> **Note：**  
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

	    // React 元素
	    optionalElement: React.PropTypes.element,

	    // 你也可以宣告這個 prop 是 class 的實例
	    // 使用 JS 的 instanceof 操作符的實例
	    optionalMessage: React.PropTypes.instanceOf(Message),

	    // 可以把它當作 enum
	    // 限制 prop 只接受指定的值
	    optionalEnum: React.PropTypes.oneOf(['News', 'Photos']),

	    // 指定物件可以為多個類型中的一個
	    optionalUnion: React.PropTypes.oneOfType([
	      React.PropTypes.string,
	      React.PropTypes.number,
	      React.PropTypes.instanceOf(Message)
	    ]),

	    // 由指定類型組成的陣列
	    optionalArrayOf: React.PropTypes.arrayOf(React.PropTypes.number),

	    // 物件有指定類型的屬性
	    optionalObjectOf: React.PropTypes.objectOf(React.PropTypes.number),

	    // 指定物件的參數
	    optionalObjectWithShape: React.PropTypes.shape({
	      color: React.PropTypes.string,
	      fontSize: React.PropTypes.number
	    }),

	    // 可以在任何類型後面加上 `isRequired` 來使 prop 不可為空
	    // 會給出警告訊息
	    requiredFunc: React.PropTypes.func.isRequired,

	    // 可以是任意類型，但是不可為空
	    requiredAny: React.PropTypes.any.isRequired,

	    // 可以自定義驗證。如果驗證錯誤，要回傳 Error 物件
	    // 不能使用`console.warn`或 throw，因為`oneOfType`會失效
	    customProp: function(props, propName, componentName) {
	      if (!/matchme/.test(props[propName])) {
	        return new Error('Validation failed!');
	      }
	    }
	  },
	  /* ... */
	});

## 默認Prop 值
React 支援以宣告的方式來定義`props`的預設值。

	var ComponentWithDefaultProps = React.createClass({
		getDefaultProps: function () {
			return {
				value: 'default value'
			};
		}
		/* ... */
	});

當父級沒有傳入 props 時，`getDefaultProps()`可以保證`this.props.value`有默認值，注意`getDefaultProps()`的結果會被緩存。得益於此，你可以直接使用 props，而不必手動編寫一些重複或無意義的代碼。

## 傳遞 Props：小技巧
有一些常用的 React 元件只是對 HTML 做簡單擴展。通常你會想少寫點程式碼來把傳入元件的 props 複製到對應的 HTML 元素上。這時 JSX 的 spread 語法會幫到你：

	var CheckLink = React.createClass({
		render: function () {
			// This takes any props passed to CheckLink and copies them to <a>
			return <a {...this.props}>{'√ '}{this.props.children}</a>;
		}
	});

	ReactDOM.render(
		<CheckLink href="/checked.html">
			Click here!
		</CheckLink>,
		document.getElementById('example')
	);

## 單個子級
使用`React.PropTypes.element`可以限定只能有一個子級傳入。

	var MyComponent = React.createClass({
		propTypes: {
			children: React.PropTypes.element.isRequired
		},
		render: function () {
			return (
				<div>
					{this.props.children}
					// 這必須是一個元素，否則將拋出錯誤訊息
				</div>
			);
		}
	});

## Mixins
元件是 React 裡重複使用程式碼的最佳方式，但是有時一些差異很大的元件間也需要共用一些功能。有時會被稱為 [cross-cutting concerns](http://www.wikiwand.com/en/Cross-cutting_concern)。React 提供`mixins`來解決這類問題。

一個常用的場景是：一個元件需要定期更新。用`setInterval()`做很容易，但當不需要它的時候取消定時器來節省內存是非常重要的。React 提供 [lifecycle methods](https://facebook.github.io/react/docs/working-with-the-browser.html#component-lifecycle) 來告知元件創建或銷毀的時間。下面來做一個簡單的`mixin`，使用這些方法提供一個簡單的`setInterval()`，會在元件銷毀時自動清空。

	var SetIntervalMixin = {
		componentWillMount: function () {
			this.intervals = [];
		},
		setInterval: function () {
			this.intervals.push(setInterval.apply(null, arguments));
		},
		componentWillUnmount: function () {
			this.intervals.forEach(clearInterval);
		}
	};

	var TickTock = React.createClass({
		mixins: [SetIntervalMixin], // 使用 mixin
		getInitialState: function () {
			return {seconds: 0};
		},
		componentDidMount: function () {
			this.setInterval(this.tick, 1000); // 呼叫 mixin 上的方法
		},
		tick: function () {
			this.setState({seconds: this.state.seconds + 1});
		},
		rendr: function () {
			return (
				<p>
					React has been running for {this.state.seconds} seconds.
				</p>
			);
		}
	});

	ReactDOM.render(
		<TickTock />,
		document.getElementById('example')
	);

關於 mixin 值得一提的優點是，如果一個元件使用了多個 mixin，並且有多個 mixin 定義了同樣的生命週期方法（例如：多個 mixin 都需要在元件銷毀時做資源清理操作），所有這些生命週期方法都保證會被執行到。方法執行順序是：首先按照 mixin 引入順序執行 mixin 裡方法，最後執行元件內定義的方法。

## ES6 Classes
你也可以定義 React classes 當作原生 JavaScript class。範例上使用 ES6 的 class 語法：

	class HelloMessage extends React.Component {
		render () {
			return <div>Hello {this.props.name}</div>
		}
	}
	ReactDOM.render(<HelloMessage name="Sebastian" />, mountNode);

這個 API 跟沒有`getInitialState`的`React.createClass`相似。你可以在建構式設定自己的`state`屬性，以替代`getInitialState`方法。

另一個不同的地方是`propTypes`和`defaultProps`被當作建構式的屬性，而不是在 class 裡面。

	export class Counter extends React.Component {
		constructor(props) {
			super(props);
			this.state = {count: props.initialCount};
		}
		tick() {
			this.setState({count: this.state.count + 1});
		}
		render() {
			return (
				<div onClick={this.tick.bind(this)}>
					Click: {this.state.count}
				</div>
			);
		}
	}

	Counter.propTypes = {initialCount: React.PropTypes.number};
	Counter.defaultProps = {initialCount: 0};

### 沒有自動綁定
方法遵循跟普通 ES6 classes 相同的語義，這意味著它們不會自動綁定到`this`實例。你必須明確使用`.bind(this)`或 [arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)`=>`。

### 沒有 Mixins
不幸的是 ES6 不支援任何 mixin。因此，當在 React 使用 ES6 classes 將無法支援 mxins。我們正在努力使它更容易支持這樣的用法而不是求助於 mixin。

## Stateless Functions
你也可以定義你的 React classes 作為一個原生的 JavaScript function。例如使用 stateless function 語法：

	function HelloMessage(props) {
		return <div>Hello {props.name}</div>;
	}
	ReactDOM.render(<HelloMessage name="Sebastian" />, mountNode);

或使用新的 ES6 arrow 語法：

	var HelloMessage = (props) => <div>Hello {props.name}</div>;
	ReactDOM.render(<HelloMessage name="Sebastian" />, mountNode);

This simplified component API is intended for components that are pure functions of their props. 這些元件不會保留內部 state，不會有 backing instances 也不會有元件的生命週期方法。They are pure functional transforms of their input, with zero boilerplate.

> **Note：**  
> Because stateless functions don't have a backing instance, you can't attach a ref to a stateless function component. Normally this isn't an issue, since stateless functions do not provide an imperative API. Without an imperative API, there isn't much you could do with an instance anyway. However, if a user wants to find the DOM node of a stateless function component, they must wrap the component in a stateful component (eg. ES6 class component) and attach the ref to the stateful wrapper component.

在一個理想的世界裡，大部分的元件是 stateless functions，因為這些無狀態的元件可以按照 React 核心內更快的程式碼路徑。這是在可能的情況下推薦的模式。

# Transferring Props
在 React 中最常見的模式是在一個抽象的概念包裝元件。外部元件暴露一個簡單的屬性做一些事情，可能有更複雜的實作細節。

您可以使用 [JSX spread attributes](https://facebook.github.io/react/docs/jsx-spread.html) 來合併舊的屬性和額外的值：

	<Component {...this.props} more="values" />

如果你不使用 JSX，你可以使用任何物件，例如 ES6 `Object.assign`或是 Underscore 的`_.extend`：

	React.createElement(Component, Object.assign({}, this.props, {more: 'values'}));

本教程的其餘部分介紹的最佳做法。它使用 JSX 和 實驗中的 ES7 語法。

## 手動傳輸
大部分情況下你應該明確地向下傳遞 props。這可以確保您只露出內部 API 的一個子集，一個你知道會運作。

	var FancyCheckbox = React.createcLASS({
		render: function () {
			var fancyClass = this.props.checked ? 'FancyChecked' : 'FancyUnchecked';
			return (
				<div className={fancyClass} onClick={this.props.onClick}>
					{this.props.children}
				</div>
			);
		}
	});
	ReactDOM.render(
		<FancyCheckbox check={true} onClick={console.log(console)}>
			Hello world!
		</FancyCheckbox>,
		document.getElementById('example')
	);

但`name`這個屬性怎麼辦？還有`title`、`onMouseOver`這些屬性？

## 在 JSX 裡使用...傳遞
> **Note：**  
> `...`語法是 Object Rest Spread proposal 的一部份。這個 proposal 有望成為一項標準。查看 [Rest and Spread Properties ...](https://facebook.github.io/react/docs/transferring-props.html#rest-and-spread-properties-...) 下面區塊瞭解更多。

有時把所有屬性都傳下去是不安全和繁瑣的。這時可以使用 [destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) 配合剩餘屬性來把未知屬性批量提取出來。

列出所有要當前使用的屬性，後面跟著`...other`。

	var { checked, ...other } = this.props;

這樣能確保把所有 props 傳下去，除了那些已經被使用了的。

	var FancyCheckbox = React.createClass({
		rendr: function () {
			var { checked, ...other } = this.props;
			var fancyClass = checked ? 'FancyChecked' : 'FancyUnchecked';
			// `other` 包含 { onClick: console.log } 但不是包含 checked 屬性
			<div {...other} className={fancyClass} />
		}
	});
	ReactDOM.render(
		<FancyCheckbox checked={true} onClick={console.log.bind(console)}>
			Hello world!
		</FancyCheckbox>,
		document.getElementById('example')
	);

> **Note：**  
> 上面例子中，`checked`屬性也是一個有效的 DOM 屬性。如果你沒有使用解構賦值，那麼可能無意中把它傳出去。

在傳遞這些未知的`other`屬性時，要經常使用解構賦值模式。

	var FancyCheckbox = React.createClass({
		render: function () {
			var fancyClass = this.props.checked ? 'FancyChecked' : 'FancyUnchecked';
			// 錯誤方式：`checked` 將不會被傳遞到內部元件
			return (
				<div {...this.props} className={fancyClass} />
			);
		}
	});

## 使用和傳遞同一個 Prop
如果元件需要使用一個屬性又要往下傳遞，可以直接使用`checked={checked}`再傳一次。這樣做比傳整個 this.props 要好，更利於重構和語法檢查。

	var FancyCheckbox = React.creatClass({
		render: function () {
			var {checked, title, ...other} = this.props;
			var fancyClass = checked ? 'FancyChecked' : 'FancyUnchecked';
			var fancyTitle = checked ? 'X ' + title : 'O ' + title;

			return (
				<label>
					<input {...other}
						checked={checked}
						className={fancyClass}
						type="checkbox"
					/>
					{fancyTitle}
				</label>
			);
		}
	});

> **Note：**  
> 順序很重要，把`{...other}`放到 JSX props 前面可以確保它不被覆蓋。上面例子中我們可以保證 input 的 type 是 "checkbox"。

## Rest and Spread 屬性 ...
Rest 屬性可以把對象剩下的屬性提取到一個新的對象。會把所有在解構賦值中列出的屬性剔除。

這是 [ES7 草案](https://github.com/sebmarkbage/ecmascript-rest-spread)中的試驗特性。

	var { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4};
	x; // 1
	y; // 2
	z; // { a: 3, b: 4}

> **Note：**  
> 這份草案已經到了第二階段而且現在在 Babel 中預設可使用。在 Babel 舊版中可能會需要使用`babel --optional es7.objectRestSpread`來啟用這個轉換。

## 使用 Underscore 來傳遞
如果不使用 JSX，可以使用一些 library 來實現相同效果。Underscore 提供`_.omit`來過濾屬性，`_.extend`複製屬性到新的對象。

	var FancyCheckbox = React.creatClass({
		render: function () {
			var checked = this.props.checked;
			var other = _.omit(this.props, 'checked');
			var fancyClass = checked ? 'FancyChecked' : 'FancyUnchecked';
			return (
				React.DOM.div(_.extend({}, other, { className: fancyClass }))
			);
		}
	});

# Forms
諸如`<input>`、`<textarea>`、`<option>`這樣的表單元件不同於其他原生元件，因為他們可以透過使用者互動發生變化。這些元件提供的界面使響應使用者互動的表單數據處理更加容易。這些元件提供的介面，使得更容易地在 UI 上響應表單管理。

關於`<form>`事件詳情請查看[表單事件](https://facebook.github.io/react/docs/events.html#form-events)。

## Interactive 屬性
表單元件支援幾個受使用者互動影響的屬性：

* `value`，用於`<input>`、`<textarea>`元件。
* `checked`，用於類型為`checkbox`或者`radio`的`<input>`元件。
* `selected`，用於`<option>`元件。
在 HTML 中，`<textarea>`的值通過子節點設置；在 React 中則應該使用 value 代替。

表單元件可以通過在`onChange`屬性設置回調函數來監聽元件變化。當使用者做出以下互動時，`onChange`執行並通過瀏覽器做出響應：

* `<input>`或`<textarea>`的 value 發生變化時。
* `<input>`的`checked`狀態改變時。
* `<option>`的`selected`狀態改變時。

和所有 DOM 事件一樣，所有的 HTML 原生元件都支持`onChange`屬性，而且可以用來監聽觸發的 change 事件。

> **Note：**  
> For `<input>` and `<textarea>`, `onChange` supersedes — and should generally be used instead of — the DOM's built-in [oninput](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/oninput) event handler.

## 控制元件
設置了`value`的`<input>`是一個控制元件。對於受控制的`<input>`，渲染出來的 HTML 元素始終保持`value`屬性的值。例如：

	render: function () {
		return <input type="text" value="Hello!" />;
	}

上面的範例將渲染出一個值為`Hello!`的`input`元素。使用者在渲染出來的元素裡輸入任何值都不會起作用，因為React已經賦值為`Hello!`。如果想響應更新使用者輸入的值，就得使用`onChange`事件：

	getInitialState: function () {
		return {value: 'Hello!'};
	},
	handleChange: function (event) {
		this.setState({value: event.target.value});
	},
	render: function () {
		var value = this.state.value;
		return <input type="text" value={value} onChange={this.handleChange} />;
	}

上面的範例中，React 將使用者輸入的值更新到`<input>`元件的`value`屬性。這樣實現響應或者驗證使用者輸入的介面就很容易了。例如：

	handleChange: function (event) {
		this.setState({value: event.target.value.substr(0, 140)});
	}

這將會接收使用者的輸入但是會擷取前 140 個字符。

### 複選框和單選按鈕的潛在問題
要知道，在試圖正常化 checkbox 和 radio 的`change`事件處理，React 使用了`click`事件取代`change`事件。For the most part this behaves as expected, except when calling `preventDefault` in a `change` handler. `preventDefault` stops the browser from visually updating the input, even if `checked` gets toggled. This can be worked around either by removing the call to `preventDefault`, or putting the toggle of `checked` in a `setTimeout`.

## 不受控制元件
沒有設置`value` (或者設為`null`)的`<input>`元件是一個不受限元件。對於不受限的`<input>`元件，渲染出來的元素會直接反應使用者輸入。例如：

	render: function () {
		return <input type="text" />;
	}

這將渲染出一個空值的輸入框，使用者輸入的值將立即反應到元素上。如果想要監聽值的更新，就和受限元素一樣，使用`onChange`事件。

### 預設值
如果想給元件設置一個非空的初始值，可以使用`defaultValue`屬性。例如：

	render: function () {
		return <input type="text" defaultValue="Hello!" />;
	}

這個範例渲染出來的元素和**受限元件**一樣有一個初始值，但這個值用戶可以改變並會反應到界面上。
同樣地，類型為`radio`、`checkbox`的`<input>`支持`defaultChecked`屬性，`<select>`支持`defaultValue`屬性。

	render: function () {
		return (
			<div>
				<input type="radio" name="opt" defaultChecked /> Option 1
				<input type="radio" name="opt" /> Option 2
				<select defaultValue="C">
					<option value="A">Apple</option>
					<option value="B">Banana</option>
					<option value="C">Cranberry</option>
				</select>
			</div>
		);
	}

> **Note：**  
> `defaultValue`和`defaultChecked`屬性只會在第一次渲染時使用到。如果你需要在隨後的渲染更新值，你將會需要使用[控制元件](https://facebook.github.io/react/docs/forms.html#controlled-components)

## 進階主題
### 為什麼使用控制元件？
在 React 中使用諸如`<input>`的表單元件時，遇到了一個在傳統 HTML 中沒有的挑戰。比如下面的在 HTML 的範例：

	<input type="text" name="title" value="Untitled" />

在 HTML 中將渲染*初始值*為`Untitled`的輸入框。當使用者改變輸入框的值時，節點的`value`*屬性（property）*將隨之變化，然而`node.getAttribute('value')`還是會返回初始設置的值`Untitled`。

與 HTML 不同，React 元件必須在任何時間點描繪視圖的狀態，而不僅僅是在初始化時。比如在 React 中：

	render: function () {
		return <input type="text" name="title" value="Untitled" />;
	}

該方法在任何時間點渲染組件以後，輸入框的值就應該*始終*為`Untitled`。

### 為什麼`<textarea>`使用`value`屬性？
在 HTML 中，`<textarea>`的值通常使用子節點設置：

	<!--反例：在React中不要這樣使用！-->
	<textarea name="description">This is the description.</textarea>

對 HTML 而言，讓開發者設置多行的值很容易。然而，因為 React 是 JavaScript，沒有字符限制，可以使用`\n`實現換行。簡言之，React 已經有`value`、`defaultValue`屬性，`</textarea>`元件的子節點扮演什麼角色就有點模棱兩可了。基於此，設置`<textarea>`值時不應該使用子節點：

	<textarea name="description" value="This is the description." />

如果非*要*使用子節點，效果上和使用`defaultValue`一樣。

### 為什麼`<select>`使用`value`屬性
HTML 中`<select>`通常使用`<option>`的`selected`屬性設置選中狀態；React 為了更方便的控制元件，採用以下方式代替：

	<select value="B">
		<option value="A">Apple</option>
		<option value="B">Banana</option>
		<option value="C">Cranberry</option>
	</select>

如果是不受限組件，則使用`defaultValue`替代。

> **Note：**  
> 可以向`value`屬性傳遞一個陣列，可以在`select`標籤中選擇多個選項：`<select multiple={true} value={['B', 'C']} />`。

# Working With the Browser
React 提供了強大的抽象功能，讓你在大多數的使用情境中不再需要直接操作 DOM，但是有時你還是需要簡單地調用底層的 API，或者使用第三方 library 或已存在的程式碼。

## 虛擬 DOM
React 是很快的，因为它從不直接操作 DOM。React 在内存中維護一个快速響應的 DOM。`render()`方法其實是回傳一個 DOM 的*描述*，React 能夠利用内存中的描述来計算出最快更新到瀏覽器的方法。

另外，React 實現了一个完備的虛擬事件系统，儘管各個瀏覽器都有自己的怪異行為，React 確保所有事件物件都符合 W3C 規範，並且持續觸發，用一種高性能的方式跨瀏覽器（and everything bubbles consistently and in a performant way cross-browser）。你甚至可以在 IE8 中使用一些HTML5 的事件！

大多數時候你應該待在 React 的 “虛擬瀏覽器” 世界裡，因为它性能更加好且容易理解。然而，有時你需要簡單地調用底層的 API，或者借助於第三方類似 jQuery 插件這種 library。React 為你提供了直接使用底層 DOM API 的途徑。

## `Refs`和`getDOMNode()`
為了和瀏覽器互動，你將需要一個對 DOM 節點的引用。你可以在每個元素附上`ref`，它允許你引用元件的**backing instance**。如果您需要調用元件的必要功能，或者希望訪問底層 DOM 節點，這會非常有用。想了解更多關於 refs，包括如何有效地使用它們，請參閱我們的 [refs to components](https://facebook.github.io/react/docs/more-about-refs.html) 文件。

## 元件生命週期
元件的生命週期包含三個主要部分：

* **掛载：** 元件被插入到 DOM 中。
* **更新：** 元件被重新渲染，查明 DOM 是否應該刷新。
* **卸載：** 元件從 DOM 中移除。
React 提供生命周期方法，你可以在這些方法中放入自己的程式碼。我們提供 **will** 方法，會在某些行為發生之前調用，和 **did** 方法，會在某些行為發生之後調用。

### 掛載
* `getInitialState()：object`在元件被掛載之前调用。Stateful 元件應該實現這個方法，返回初始的 state 資料。
* `componentWillMount()`在掛載發生之前立即被调用。
* `componentDidMount()`在掛載結束後馬上被調用。需要 DOM 節點的初始化操作應該放在這裡。

### 更新
* `componentWillReceiveProps(object nextProps)`當一個掛載的元件接收到新的 props 的時候被調用。該方法應該用於比較`this.props`和`nextProps`，然後使用`this.setState()`來改變state。
* `shouldComponentUpdate(object nextProps, object nextState)：boolean`當元件做出是否要更新 DOM 的決定的時候被調用。實現該函數來作為`this.props`和`nextProps`，以及`this.state`和`nextState`的比較優化，如果不需要 React 更新 DOM，則返回 false。
* `componentWillUpdate(object nextProps, object nextState)`在更新發生之前被調用。你**不可以**在這裡調用`this.setState()`。
* `componentDidUpdate(object prevProps, object prevState)`在更新發生之後調用。

### 卸載
* `componentWillUnmount()`在元件被卸載和刪除之前被调用。清理工作應該放在這裡。

### 掛載的方法（Mounted Methods）
掛載的複合元件也支持以下方法：

* `component.forceUpdate()`會在當你知道一些很深的元件 state 已經被改變而沒有使用`this.setState()`時可以在該元件上面調用。

## Browser Support and Polyfills
在 Facebook，我們支援舊版的瀏覽器，包括 IE8。我已經花了很長時間來編寫相容代碼，讓我們可以邊寫超前思維的 JS。這位著我們沒有一些黑客可以充斥在我們程式碼中，並且我們依然能夠預期我們的程式碼"正常運作"。例如，不使用`+new Date()`，我們能夠寫`Date.now()`。我們在內部使用，的因此開源的 React 也是相同的。我們延續了這一理念運用在前瞻性思維的JS。

In addition to that philosophy, we've also taken the stance that we, as authors of a JS library, should not be shipping polyfills as a part of our library. If every library did this, there's a good chance you'd be sending down the same polyfill multiple times, which could be a sizable chunk of dead code. If your product needs to support older browsers, chances are you're already using something like [es5-shim](https://github.com/es-shims/es5-shim).

### 支持舊版浏览器的兼容代码
[kriskowal es5-shim](https://github.com/es-shims/es5-shim) 的`es5-shim.js`提供了以下 React 需要的 API：

* `Array.isArray`
* `Array.prototype.every`
* `Array.prototype.forEach`
* `Array.prototype.indexOf`
* `Array.prototype.map`
* `Date.now`
* `Function.prototype.bind`
* `Object.keys`
* `String.prototype.split`
* `String.prototype.trim`

[kriskowal es5-shim](https://github.com/es-shims/es5-shim) 的`es5-shim.js`也提供了以下 React 需要的 API：

* `Object.create`
* `Object.freeze`

The unminified build of React needs the following from [paulmillr's console-polyfill](https://github.com/paulmillr/console-polyfill).

* `console.*`

當在 IE8 中使用 HTML5 元素，包括`<section>`,`<article>`,`<nav>`,`<header>`和 `<footer>`，它需要引入 [html5shiv](https://github.com/aFarkas/html5shiv) 或其他類似的腳本。

### 跨瀏覽器問題
雖然 React 已經非常好的描述了瀏覽器的差異，有些瀏覽器是有限制的或呈現古怪的行為，我們無法照到一個解決方法。

#### onScroll event on IE8
在 IE8 中`onScroll`的事件不會觸發而且 IE8 沒有一個 API 定義處理程序可以抓到事件，意思是 React 沒有辦法監聽這些事件出反應。目前這一個事件處理程序在 IE8 被忽略。

See the [onScroll doesn't work in IE8](https://github.com/facebook/react/issues/631) GitHub issue for more information.

# Working With the Browser - Refs to Components
在建立你的元件之後，你可能會想要"reach out"和在`render()`返回的元件實力上調用否些方法。通常來說，這樣是不必要的，因為活躍的資料流(Reactive data)總是確保最近的 props 被發送到每個從`render()`輸出的子級。然而，有一些情況下，它仍可能有必要或有益的。所以 React 提供`refs`的逃生艙口。當你需要做以下動作時，這些`refs`相當有用：找到由元件 render 的 DOM 標記（例如絕對位置），在大型的非 React 應用程式中使用 React 元件，或轉換現有的程式碼到 React。

讓我們來看看如何獲得一個引用，然後潛入一個完整的例子。

## 從 ReactDOM.render 回傳 ref
為了不混淆你在你定義的元件的`render()`方法，[ReactDOM.render()](https://facebook.github.io/react/docs/top-level-api.html#reactdom.render) 將會回傳一個 reference 到你元件的 **backing instance**(或`null`的 [stateless 元件](https://facebook.github.io/react/docs/reusable-components.html#stateless-functions))。

	var myComponent = ReactDOM.render(<MyComponent />, myContainer);

但是請記住，JSX 不回傳元件實例。只是一個 **ReactElement：**一個輕量級的表現，告訴 React 要掛載的元件應該長怎樣。

	var myComponentElement = <MyComponent />; // 這只是一個 ReactElement

	// Some code here...

	var myComponentInstance = ReactDOM.render(myComponentElement, myContainer);
	myComponentInstance.doSomething();

> **Note：**  
> 這個應該永遠只在頂層使用。在元件內部，讓你的`props`和`state`處理跟子元件的溝通，或使用可取得一個 ref（字符串屬性或回調函式）的其他方法之一。

## ref 回調屬性
React 支援一種特殊的屬性，你可以綁定到任何元件上。`ref`屬性可以是一個回調函式，而且這個回調函式會在元件被掛載後立即執行。reference 元件將會被當作參數來傳遞，而且回調函式可能會立刻使用元件，或者儲存 reference 到未來使用(或兩者都有)。

作法很簡單，添加一個`ref`屬性到`render`回傳的東西上面去

	render: function () {
		return (
			<TextInput ref={function(input) {
				if (input != null) {
					input.focus();
				}
			}} />
		);
	},

或是使用 ES6 的 arrow function：

	render: function () {
		return <TextInput ref={(c) => this._input = c} />;
	},
	componentDidMount: function () {
		this._input.focus();
	},

當綁定一個 ref 到 DOM 元件，像是`<div />`。你會得到 DOM 節點; 當綁定一個 ref 到複合元件，像是`<TextInput />`，你將會得到 React class 實例。在第二種情況下，你可以調用該元件的方法，如果有任何被暴露在它的 class 定義。

需要注意的是，當引用的元件被卸載以及 ref 有變化，舊的 ref 將為`null`並作為一個參數。這可以防止記憶體洩漏，該實例被存儲，像是在第一實施例的情況。另外也要注意，可以寫把 refs 寫在內聯函數表達式，一如這裡的例子。React 會在每次更新時，查看不同的函數對象。ref 將會在它調用元件實例時立刻被調用為`null`。

## ref 字串屬性
React 也支援在每個元件上使用字串當作 ref 屬性，雖然這種方法是之前的遺產。

1. 指定任何從`render`回傳的`ref`屬性，例如：  

		<input ref="myInput" />
	
2. 在一些其他的代碼（通常是事件處理程序代碼），透過`this.refs`來存取 **backing instance**，例如：

		var input = this.refs.myInput;
		var inputValue = input.value;
		var inputReact = input.getBoundingClientRect();

## 完成示例
為了取得一個 referenece 到 React 元件，你可以使用`this`來得到當前的 React 元件，或是可以使用 ref 來得到一個你擁有元件的 reference。它們的運作像下面：

	var MyComponent = React.createClass({
		handleClick: function () {
			// 明確地使用原生 DOM API 來 focus text input
			this.myTextInput.focus();
		},
		render: function () {
			// ref 屬性添加一個 reference 到元件的 this.refs 當元件掛載時
			return (
				<div>
					<input type="text" ref={(ref) => this.myTextInput = ref} />
					<input type="button" value="Focus the text input" onClick={this.handleClick} />
				</div>
			);
		}
	});

	ReactDOM.render(<MyComponent />, document.getElementById("example"));

在這個範例中，我們可以從 text input 的 **backing instance** 取得一個 referenece，而且會在按鈕被點擊時調用`focus()`。

對於複合元件，這個 reference 將參考元件 class的實例，所以你將可以調用被該 class 定義的任何方法。如果你需要存取元件的底層 DOM 節點，你可以使用 [ReactDOM.findDOMNode](https://facebook.github.io/react/docs/top-level-api.html#reactdom.finddomnode) 作為"太空艙"，但是我們並不建議，因為它會打破封裝而且在大多情況下，有一個更清晰的方式可以在 React model 內建構你的程式碼。

## 總結
Refs 是一種給指定的子元件實例發送消息的很好的方式，從某種程度上來看，通過`props`和`state`來做這件事倒顯得不太方便。They should, however, not be your go-to abstraction for flowing data through your application. By default, use the Reactive data flow and save ref s for use cases that are inherently non-reactive.

### 優點：
* 可以在元件 classes 裡面定義任何公共的方法（比如在預輸入的重置方法），然後通過 refs 來調用這些公共的方法（比如`this.refs.myTypeahead.reset()`）。在大多數的情況下，你可以使用內建的 React 資料流來取代使用 refs。
* 執行 DOM 幾乎需要深入到 “原生的” 元件，比如通過 ref 獲取`<input />`元素的底層 DOM 節點。Refs 是做這件事唯一可靠的方式。
* Refs 是被自動管理的！如果某個子級實例被銷毀了，它的 ref 也會自動銷毀。不用考慮內存問題（除非你自己做一些瘋狂的操作，保存了什麼 reference）。

### 當心:
* *絕不要*在任何元件的`render`方法中存取 refs - 或者在某個元件的`render`方法正在調用 stack 中運行的時候。
* If you want to preserve Google Closure Compiler advanced-mode crushing resilience, make sure to never access as a property what was specified as a string. This means you must access using `this.refs['myRefString']` if your ref was defined as `ref="myRefString"`.
* If you have not programmed several apps with React, your first inclination is usually going to be to try to use refs to "make things happen" in your app. If this is the case, take a moment and think more critically about where `state` should be owned in the component hierarchy. Often, it becomes clear that the proper place to "own" that state is at a higher level in the hierarchy. Placing the state there often eliminates any desire to use `refs` to "make things happen" – instead, the data flow will usually accomplish your goal.
* Refs may not be attached to a [stateless function](https://facebook.github.io/react/docs/reusable-components.html#stateless-functions), because the component does not have a backing instance. You can always wrap a stateless component in a standard composite component and attach a ref to the composite component.

# Tooling Integration
每個專案都使用了不同的系統來構建和部署 JavaScript。我們嘗試盡量讓 React 不受環境影響。

## React
### CDN-hosted React
我們在我們的[下載頁面](https://facebook.github.io/react/downloads.html)提供了 React 的 CDN-hosted 版本。這些預構建的檔案使用 UMD 模塊格式。直接簡單地把它們放在`<script>`標籤中將會給在你的環境中插入一個全域的 React 物件。React 也可以在CommonJS和AMD環境下正常工作。

### 使用主分支
我們在 [GitHub 倉庫](https://github.com/facebook/react)的主分支上有一些構建指令。我們在`build/modules`下構建了符合 CommonJS 模組規範的樹形目錄，你可以放置在任何環境或者使用任何打包工具，只要支援 CommonJS 規範。

## JSX
### 瀏覽器中的JSX轉換
如果你喜歡使用 JSX，Babel 提供了 [in-browser ES6 and JSX transformer for development](http://babeljs.io/docs/usage/browser/) 叫做 browser.js。可以從`babel-core`的 npm 套件引入或是從 [CDNJS](http://cdnjs.com/libraries/babel-core)。用一個`<script type="text/babel">`標籤來觸發 JSX 轉換器。

> **注意：** 
> 瀏覽器中的 JSX 轉換器是相當大的，並且會在客戶端導致無謂的計算，這些計算是可以避免的。不要在生產環境使用 - 參考下一節。

### 生產環境化：預編譯 JSX
如果你有 [npm](https://www.npmjs.com/)，你可以簡單地運行`npm install -g babel-cli`。Babel 內建支援到 React v0.12+。標籤會自動轉換到其等效的`React.createElement（...）`,`displayName`自動推斷並添加到所有`React.createClass`呼叫。

這個工具會把使用 JSX 語法的文件轉換成可以直接在瀏覽器裡面運行起來的原生 JavaScript 文件。它也會為你監聽目錄，然後自動轉換變化的文件；例如：`babel --watch src/ --out-dir lib/`。

從 Babel 6 開始，默認情況下並不包括轉換。這意味著在執行`babel`指令時，必須指定選項，或是`.babelrc`必須指定選項。Additional packages must also be installed which bundle together a number of transforms, called presets. The most common use when working with React will be to include the es2015 and react presets. More information about the changes to Babel can be found in [their blog post announcing Babel 6](http://babeljs.io/blog/2015/10/29/6.0.0/)。

這裡是一個例子，如果你使用了 ES2015 格式和 React

	npm install babel-preset-es2015 babel-preset-react
	babel --presets es2015,react --watch src/ --out-dir lib/

預設的 JSX 檔案會轉換成副檔名為`.js`的檔案。執行`babel --help`來瞭解更多使用 Babel 的方法。

	$ cat test.jsx
	var HelloMessage = React.createClass({
	  render: function() {
	    return <div>Hello {this.props.name}</div>;
	  }
	});
	
	ReactDOM.render(<HelloMessage name="John" />, mountNode);
	$ babel test.jsx
	"use strict";
	
	var HelloMessage = React.createClass({
	  displayName: "HelloMessage",
	
	  render: function render() {
	    return React.createElement(
	      "div",
	      null,
	      "Hello ",
	      this.props.name
	    );
	  }
	});
	
	ReactDOM.render(React.createElement(HelloMessage, { name: "John" }), mountNode);

## 有用的開源項目
開源社區開發了在幾款編輯器中集成 JSX 的插件和構建系統。點擊 [JSX 集成](https://github.com/facebook/react/wiki/Complementary-Tools#jsx-integrations)查看所有內容。

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