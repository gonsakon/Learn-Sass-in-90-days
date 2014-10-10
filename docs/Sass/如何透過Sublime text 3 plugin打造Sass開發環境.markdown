#如何透過Sublime text 3 plugin打造Sass開發環境

##youtube影片教學  
<a href="https://www.youtube.com/watch?v=er2evZqsvbg&feature=youtu.be" target="_blank">![](/images/video/susy2-11.png)</a> 

<a href="http://www.sublimetext.com/3" target="_blank">Sublime text 3 網站連結</a>，  
首先Sublime text 3是沒有提供Sass、Scss語法高亮的，
所以你必須先安裝 Package Control後才能安裝支援Sass與Scss的插件。
Package Control的安裝流程可以瀏覽此<a href="https://sublime.wbond.net/installation" target="_blank">安裝流程</a>，如果看不懂的話可以瀏覽影片安裝流程：  

接下來就要來講各個Plugin的功能，  
以下熱鍵都是For Mac，  
但我會提供Plugin連結，  
裡面會顯示Windows的熱鍵功能。  

### Sass、Scss

Sublime預設是沒有支援Sass、Scss的高亮效果的，  
所以首要安裝的Plugin自然是這兩個。

### emmet
可以快速產生出你要的HTML、CSS程式碼：  
* <a href="http://docs.emmet.io/" target="_blank">emmet官網</a>
* <a href="http://docs.emmet.io/cheat-sheet/" target="_blank">emmet 字典</a>
這裡也提供我常用的片段，  
請記得要展開出片段時，  
要再程式碼最右側按`Tab`鍵來展開：
```
html:5   //展開html5的格式
link:css //插入一個CSS連結
script:src //插入一個javscript
p*3      //三個P段落
h1+p     // 會編譯成<h1></h1><p></p>
h1>a     // 會編譯成<h1><a href="#"></a></h1>
a[href='http://xxx.com'] //在html tag裡面寫屬性
.box    // 展開為 <div class="box"></div>

.box > ul >li*3 >a     //會編譯成下列程式碼：
<div class="box">
	<ul>
		<li><a href=""></a></li>
		<li><a href=""></a></li>
		<li><a href=""></a></li>
	</ul>
</div>
```
再來，我最喜歡的功能是`Wrap with Abbreviation`，  
以前我在上稿的時候，都是先寫HTML再一一貼稿上去，  
但有時候恍神就會貼成這樣：   
```
<ul>
	<li>文案內容</li>
	<li></li>文案內容    //不小心貼到外面
	<li><文案內容/li>    //貼到html標籤裡面
</ul>
```
`Wrap with Abbreviation`則是你可以先把文案貼到HTML，  
再按`Control+L`做成自己要的格式，  
這樣我就可以把所有的文案都貼上去，  
再變成我要的格式，上稿流程變得更加順利。  
你可以瀏覽這兩則影片來看他的效果：  
* <a href="https://www.youtube.com/watch?v=GFzjOzwtcxA#t=345">youtube影片</a>
* <a href="https://www.youtube.com/watch?v=zKjDFBeIS20">youtube影片2</a>

### Goto-CSS-Declaration
<a href="https://sublime.wbond.net/packages/Goto-CSS-Declaration">plugin介紹連結</a>
你可以從該連結可以看出，  
如果你HTML或CSS都有開啟，  
把游標移動到HTML的Class上輸入熱鍵`Command+right`、`Command+left`，  
游標就會跑到對應的CSS去了，  
這樣你就不會再費時來找CSS設定在哪裡。  

### Auto​File​Name
<a href="https://sublime.wbond.net/packages/AutoFileName">plugin介紹連結</a>  
這個Plugin的功能是，  
當你在寫HTML的a、img，或CSS的background時  
它會自動幫你load檔案的路徑出來，  
讓你不會再去找資料夾瀏覽圖片名稱再來載入，  
真的相當的方便！  

### Sass​Beautify
<a href="https://sublime.wbond.net/packages/SassBeautify">plugin介紹連結</a>  
有的時候我們寫SCSS時，  
程式碼會寫得很亂，  
雖然也能編譯成功，  
但排版沒排整齊心情就會很啊雜，  
這時候你就可以安裝這個plugin，  
但他觸發的方式是要用`Command+shift+p`輸入指令來觸發，  
裡面會有一個`Sass​Beautify`的指令，  
輸入後就會幫你排整齊。 

###HTML-CSS-JS Prettify
<a href="https://sublime.wbond.net/packages/HTML-CSS-JS%20Prettify">plugin介紹連結</a>   
這個也是拿來自動格式化排版用的，  
但必須安裝Node.js，  
他除了CSS外，也可以格式化HTML與JS，  
觸發的方式是要用`Command+shift+p`輸入指令來觸發，  
裡面會有一個`HTMLPrettify`的指令，  
輸入後就會幫你排整齊。

###SideBarEnhancements
<a href="https://sublime.wbond.net/packages/SideBarEnhancements">plugin介紹連結</a>   
增強左側資料夾的功能，  
比預設多了很多東西，  
例如可開啟指定的資料夾位置、強化搜尋、複製檔名路徑等等，  
也是必裝的軟體