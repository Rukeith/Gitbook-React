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


## Tutorial
## Thinking in React