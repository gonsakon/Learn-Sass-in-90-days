# @extend 與 @Mixin的差異性與使用時機

有些設計師沒辦法理解@extend與@Mixin的原理，  
會感覺這兩個功能差不了多少，  
所以這一章節主要是要來講這兩者的差異性。

##youtube影片教學
<a href="https://www.youtube.com/watch?v=cRX1wUcMsXc&feature=youtu.be" target="_blank">![](/images/video/Sass-1.png)</a>


## 進入主題
首先先講如何初步判斷該用@extend或@Mixin，
@extend主要是拿來`合併相同程式碼`用的，  
如果你每個段落的CSS程式碼如果都長得一模一樣，
那你就可以@extend來進行合併動作，  

而@Mixin呢？
他主要則是有兩個用途，  
第一就是`透過他幫你記住很多段落的程式碼`，  
像是CSS要隱藏文字的功能，你就可以用Compass內建的@Mixin，  
寫`@include hide-text`，他就能幫你呼叫出該功能的CSS程式碼段落。  
我甚至有一隻mixin的scss，裡面放了我很多歷年來寫的CSS原理，  
我要用他的時候，就呼叫@mixin的名字就好，   
這樣的話腦子就省掉不少記憶原理的負擔。

第二就是我們可以`透過它可以帶入變數的特性，來編譯出我們要的程式碼。`  
像是susy，如果我今天在SCSS裡面寫`@include span(8)`，  
帶入8這個變數的話，    
他就會幫我編譯出8欄的寬度出來，  

所以當你在設計網頁時，  
今天有一個CSS片段要衡量該怎麼設計的話，  
就看他是歸類於什麼屬性，
如果都是相同樣式且多行的程式碼，  
那就適合用@extend來把他合併起來。  

例如這樣：
```
// %title是css會被堆疊的位置
%title{
	font-size:18px;
	line-height:1.8;
	border-bottom: 3px solid #000;
	border-left:3px solid #000;
	padding: 0 0 0 30px;
}
.sidebar h2{
	@extend %title
}
.content h4{
	@extend %title
}
.main h3{
	@extend %title
}
//編譯出來的CSS
.sidebar h2,.content h4,.main h3{
	font-size:18px;
	line-height:1.8;
	border-bottom: 3px solid #000;
	border-left:3px solid #000;
	padding: 0 0 0 30px;
}
```

你可能會想說，  
那我用@mixin也可以啊，
不是也可以做到相同的效果？  
例如這樣：
```
@mixin title{
	font-size:18px;
	line-height:1.8;
	border-bottom: 3px solid #000;
	border-left:3px solid #000;
	padding: 0 0 0 30px;
}
.sidebar h2{
	@include title;
}
.content h4{
	@include title;
}
.main h3{
	@include title;
}
```
但這樣編譯出來，  
你CSS就會暴肥，
因為你每行都載入了相同片段，
三個地方設定了，就會載入了15行程式碼出來，  
這樣寫出來的東西自然會越來越臃腫，  
所以這樣的案例如果樣式都一模一樣，  
是不適合用@mixin，應該是用@extend合併起來節省程式碼數量，  
但又能達到相同效果。  
