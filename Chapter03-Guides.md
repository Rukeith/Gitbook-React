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

我們想到的解決方案是 React 是不會去操作DOM的，除非不得不操作DOM 。它用一種更快的內置仿造的DOM來操作差異，為你計算出效率最高的DOM改變。

這個組件的輸入被稱為props - "properties"的縮寫。它們通過JSX語法進行參數傳遞。你必須知道，在組件裡這些屬性是不可直接改變的，也就是說this.props是只讀的。

組件就像是函數
React組件非常簡單。你可以認為它們就是簡單的函數，接受props和state (後面會討論)作為參數，然後渲染出HTML。正是由於它們如此簡單，使得它們非常容易理解。

注意:
一個限制 : React組件只能渲染單個根節點。如果你想要返回多個節點，它們必須被包含在同一個節點裡。
JSX語法
我們始終堅信，組件使用了正確方法去做關注分離，而不是通過“模板引擎”和“展示邏輯”。我們認為標籤和生成它的代碼是緊密相連的。此外，展示邏輯通常是很複雜的，通過模板語言實現這些邏輯會產生大量代碼。

我們得出解決這個問題最好的方案是通過JavaScript直接生成模板，這樣你就可以用一個真正語言的所有表達能力去構建用戶界面。為了使這變得更簡單，我們做了一個非常簡單、可選類似HTML語法，通過函數調用即可生成模板的編譯器，稱為JSX。

JSX讓你可以用HTML語法去寫JavaScript函數調用。為了在React生成一個鏈接，通過純JavaScript你可以這麼寫：React.createElement('a', {href: 'http://facebook.github.io/react/'}, 'Hello React!')。通過JSX這就變成了<a href="http://facebook.github.io/react/">Hello React!</a>。我們發現這會使搭建React應用更加簡單，設計師也偏向用這種語法，但是每個人都有自己的工作流，所以JSX並不強制必須使用的。

JSX非常小；上面“hello, world”的例子使用了JSX所有的特性。想要了解更多，請看深入理解JSX。或者直接使用在線JSX編譯器觀察變化過程。

JSX類似於HTML，但不是完全一樣。參考JSX陷阱學習關鍵區別。

最簡單開始學習JSX的方法就是使用瀏覽器端的JSXTransformer。我們強烈建議你不要在生產環境中使用它。你可以通過我們的命令行工具react-tools包來預編譯你的代碼。

沒有JSX 的React
你完全可以選擇是否使用JSX，並不是React必須的。你可以通過React.createElement來創建一個樹。第一個參數是標籤，第二個參數是一個屬性對象，第三個是子節點。

var  child  =  React . createElement ( 'li' ,  null ,  'Text Content' ); 
var  root  =  React . createElement ( 'ul' ,  {  className :  'my-list'  },  child ); 
React . render ( root ,  document . body );
方便起見，你可以創建基於自定義組件的速記工廠方法。

var  Factory  =  React . createFactory ( ComponentClass ); 
... 
var  root  =  Factory ({  custom :  'prop'  }); 
React . render ( root ,  document . body );
React 已經為HTML 標籤提供內置工廠方法。

var  root  =  React . DOM . ul ({  className :  'my-list'  }, 
             React . DOM . li ( null ,  'Text Content' ) 
           );