# Quick Start
## Getting Started
### JSFiddle
開始學習 React 最簡單的方式就是使用以下 JSFiddle 的 Hello World 範例：

* [React JSFiddle](https://jsfiddle.net/reactjs/69z2wepo/)
* [React JSFiddle without JSX](https://jsfiddle.net/reactjs/5vjqabv3/)

### 從 npm 開始使用 React
我們建議配合類似 *browserify* 或 *webpack* 的CommonJS 模組系統使用 React。
使用`react`和`react-dom`的 npm 套件。

	// main.js
	var React = require('react');
	var ReactDOM = require('react-dom');
	
	ReactDOM.render(
	  <h1>Hello, world!</h1>,
	  document.getElementById('example')
	);

To install React DOM and build your bundle after installing browserify:
安裝 React DOM 和 安裝 browserify 後，建立你的包

	$ npm install --save react react-dom
	$ browserify -t babelify main.js -o bundle.js

### 不藉由 npm 快速開始
如果你還沒準備好使用 npm，你可以下載初学者教程包(Starter Kit)，包含了未預建置前的 React 和 React DOM 版本。

在 Starter Kit 的根目錄，建立一個包含以下內容的`helloworld.html`。

	<!DOCTYPE html>
	<html>
	  <head>
	    <meta charset="UTF-8" />
	    <title>Hello React!</title>
	    <script src="build/react.js"></script>
	    <script src="build/react-dom.js"></script>
	    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.23/browser.min.js"></script>
	  </head>
	  <body>
	    <div id="example"></div>
	    <script type="text/babel">
	      ReactDOM.render(
	        <h1>Hello, world!</h1>,
	        document.getElementById('example')
	      );
	    </script>
	  </body>
	</html>

在 JavaScript 裡寫著 XML 格式的程式碼稱為 JSX，可以在 [JSX](https://facebook.github.io/react/docs/jsx-in-depth.html) 學到更多相關知識。為了把 JSX 轉成標準的 JavaScript，我們用`<script type="text/babel">`和引入 Babel 來在瀏覽器實現轉換。

#### 分離檔案
編寫的 React JSX 程式碼可以分離開來，創建`src/helloworld.js`，內容如下：

	ReactDOM.render(
	  <h1>Hello, world!</h1>,
	  document.getElementById('example')
	);

然後將它引入`helloworld.html`：
`<script type="text/babel" src="src/helloworld.js"></script>`

>Note：某些瀏覽器（如，Chrome 瀏覽器）將無法載入該檔案，除非是套過 HTTP。

#### 離線轉換
第一步，先透過 command-line 使用 [npm](https://www.npmjs.com/) 安裝 [Babel](http://babeljs.io/)  
`npm install --global babel`

然後將`src/helloworld.js`轉換成標準的 JavaScript
`babel src --watch --out-dir build`

每當你做任何修改後`build/helloworld.js`將會自動產生。可以閱讀 [Babel CLI document](http://babeljs.io/docs/usage/cli/) 瞭解更多使用方法。

	ReactDOM.render(
	  React.createElement('h1', null, 'Hello, world!'),
	  document.getElementById('example')
	);

更新 HTML 如下：

<!DOCTYPE html>
	<html>
	  <head>
	    <meta charset="UTF-8" />
	    <title>Hello React!</title>
	    <script src="build/react.js"></script>
	    <script src="build/react-dom.js"></script>
	    <!-- No need for Babel! -->
	  </head>
	  <body>
	    <div id="example"></div>
	    <script src="build/helloworld.js"></script>
	  </body>
	</html>

更多工具可以查看這邊
`https://github.com/facebook/react/wiki/Complementary-Tools`

## Tutorial
我們將建立一個簡單但是實用的評論框，可以將它放入你的部落格。一個類似於 Disqus, LiveFyre 或 Facebook 的即時評論的基本版本。
將會提供：

* 展示所有評論的介面
* 發佈評論的表單
* 後端 API 的串接位置，該串接需要自己實現

同時也包含一些簡潔的特性：

* **發布評論的體驗優化：**評論在儲存到服務器之前就會​​顯示在評論列表，因此感覺起來很快。
* **實時更新：**其他用戶的評論將會即時的顯示在評論框中。
* **Markdown格式：**用戶可以使用 Markdown 語法來編輯評論。

### 想要跳過後續所有的內容，只看原始碼？
[所有代碼都在GitHub。](https://github.com/reactjs/react-tutorial)

### 運行伺服器
為了開始本教程，將會需要一個在運作的伺服器。這將會是作為一個 API 接口，用於獲取和儲存資料。為了盡可能簡單，我們已經利用幾種腳本語言準備好了開發用的簡單伺服器。可以查看原始碼或者下載壓縮檔，裡面包含了所有開始學習教程所需的東西。

為了簡單起見，伺服器將會使用一個 JSON 文件作為資料庫。在生產環境中不會採用這種做法，但是這樣做確實簡化了模擬後端 API 的工作。一旦啟動了這個服務器，它就能提供我們需要的 API 接口，同時也能生成並發送我們需要的頁面。

### Getting started
本教程我們會盡可能的簡單。上述討論提及的頁面是一個 HTML 文件，它包含在伺服器的原始碼中，我們先看看這個文件。使用你最喜歡的編輯器打開`public/index.html`，它應該會看見這些內容（可能會有一些小的差異，後面我們會添加一個額外的`<script>`標籤）：

	<!-- index.html -->
	<!DOCTYPE html>
	<html>
	  <head>
	    <meta charset="utf-8" />
	    <title>React Tutorial</title>
	    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.14.0/react.js"></script>
	    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.14.0/react-dom.js"></script>
	    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.23/browser.min.js"></script>
	    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.1/jquery.min.js"></script>
	  </head>
	  <body>
	    <div id="content"></div>
	    <script type="text/babel" src="scripts/example.js"></script>
	    <script type="text/babel">
	      // To get started with this tutorial running your own code, simply remove
	      // the script tag loading scripts/example.js and start writing code here.
	    </script>
	  </body>
	</html>

在本教程的剩下部分，我們會在這個 script 標籤中編寫我們的 JavaScript 程式碼。我們沒有任何高端的頁面自動重整工具，所以在更動程式碼之後，需要手動重整瀏覽器來查看變化。按照你的步驟，啟動伺服器後，可以在瀏覽器中輸入`http://localhost:3000`。在沒對原始碼進行修改的前提下，第一次打開這個 URL 會看到我們計劃建立的完成品。當你準備好開始往下學習後，只需要刪掉上述程式碼中的`<script>`就可以了。

>**注意：**
>我們在這裡導入了 jQuery，因為想簡化未來 ajax 請求動作，但不代表 React 必須依靠 jQuery 才能運作。

### 你的第一個元件
React 中全是模塊化、可組裝的元件。以我們的評論框為例子，我們將有如下的元件結構：

	- CommentBox
	  - CommentList
	    - Comment
	  - CommentForm

我們來建立`CommentBox`元件吧，它只是一個簡單的`<div>`：

	// tutorial1.js
	var CommentBox = React.createClass({
	  render: function() {
	    return (
	      <div className="commentBox">
	        Hello, world! I am a CommentBox.
	      </div>
	    );
	  }
	});
	ReactDOM.render(
	  <CommentBox />,
	  document.getElementById('content')
	);

>**注意：**原生的 HTML 元素名以小寫字母開頭，而自定義的 React class name 以大寫字母開頭。

#### JSX 格式
首先你將會注意到 JavaScript 中類似 XML 的語法。我們有一個簡單的預編譯器，用於將這種語法糖轉換成純 JavaScript 代碼：

	// tutorial1-raw.js
	var CommentBox = React.createClass({displayName: 'CommentBox',
	  render: function() {
	    return (
	      React.createElement('div', {className: "commentBox"},
	        "Hello, world! I am a CommentBox."
	      )
	    );
	  }
	});
	ReactDOM.render(
	  React.createElement(CommentBox, null),
	  document.getElementById('content')
	);

JSX 語法是可選的，但是我們發現 JSX 格式比純 JavaScript 用起來更容易。更多內容請閱讀 [JSX 語法文章](https://facebook.github.io/react/docs/jsx-in-depth.html)。

#### 發生了什麼事
我們通過 JavaScript 物件傳遞一些方法到`React.createClass()`來創建一個新的React 元件。其中最重要的方法是`render`，該方法回傳一顆 React 元件樹，這棵樹最終將會渲染到 HTML。

這裡的`<div>`標籤不是真正的 DOM 節點；他們是 React `div`元件的實作。你可以當作這些標籤就是一些標記或者資料，React 知道如何處理它們。React 是**安全的**。我們不生成 HTML 字符串，因此預設阻止了 XSS 攻擊。

你沒必要返回基本的 HTML，可以回傳一個你（或者其他人）建立的元件樹。而這就是讓 React 變得**可組合化**的特性：一個前端可維護性的關鍵原則。

`ReactDOM.render()`實現了根元件、啟動框架，和把標記注入到第二個參數指定的原生 DOM 元素中。

`ReactDOM`模塊提供了一些 DOM 相關的方法，而`React`包含了 React 團隊分享的不同平台上的核心工具（例如，[React Native](http://facebook.github.io/react-native/)）。

### 建構元件


## Thinking in React