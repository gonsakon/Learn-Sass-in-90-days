# Sass開發經驗分享  
這篇分享會比較雜一些，  
主要是分享這一兩年使用Sass時遇到的問題，  
畢竟寫程式並不是自己一個人的事情，  
有的時候會因為團隊組成、合作窗口而有所調整。


## 團隊開發  
如果你進入較具規模的公司時，  
裡面勢必是一個團隊，後端、前端、視覺設計師、UI設計師等等，  
所以你寫的Sass檔案也一定會跟其他前端需要協同作業，  
當多人在一起寫Sass專案時，如果沒事先設定規範，就容易像多頭馬車一樣不受控制。  
所以這裡就來分享自己的血淚史XDD  

在那之前先來講解我個人的角色，  
我是前端工程師，我不設計視覺畫面、也不碰後端。  

##在團隊專案建立前，先建立樣式規範、命名原則  
有一次我和其他前端在一塊寫Sass的時候，  
因為沒事先建立好設計規範，所以我們的顏色變數就變成這樣：  

	/color
	$darkgreen: #5EB95E
	$text-color: #ccc
	$hot-color: #46d3b9
	$white: #fff
	$black: #000
	$color-bg: #0f222b 
	$dark-blue: #0C4191
	$light-blue: #1B75BC
	$common-dark: #535E64
	$common-red: #FD5259
	$orange: #FFD74D
	$red: #FD5259
	$dark: #535E64

上面的顏色變數有些是*抽象命名*、*顏色變數*， 
你完全沒辦法從中得知這網站主色系是什麼， 
因為完全沒有規則性，這就是因為當初我們沒有事先訂好命名原則的關係，    
日後如果又有前端來參與此專案，  
你勢必就還得再一次解說你的專案。  
所以之後我們的程式碼命名規範就變成這樣：  

	//顏色色系
	$blue: #428bca;
	$white: #ffffff;
	$black: #000000;
	$pink: #f0ad4e;
	$gray: #ccc
	//抽象命名
	$btn-primary-color: $fff;
	$btn-primary-bg: $blue;
	$btn-primary-border: darken($blue, 5%); 

這樣的設計規範是先依照這網站的樣式設定一組顏色變數，  
然後後面建立網頁元素時，  
所有協同開發者都要繼承*初始顏色色系*來延伸設計。  

這樣的好處是今天如果有其他協同者要來參與，  
看這樣的變數架構就能一目了然知道這個網站的顏色樣式是如何配色，  
他要設計後續顏色就可以拿這一套來作延伸設計。  

如果你是前端工程師會Sass，  
但你的同事是美術視覺設計師時，  
可以推薦他使用<a href="http://sassme.arc90.com/">SassMe</a>這個服務，  
將顏色色碼帶進去後，  
你就在上面直接使用Sass 顏色function，  
請他將一些網站上的組件樣式透過lighten、darken的方式來設計並提供給你。   

從這個例子你就可以看得出來，  
如果你在之前沒有先把`命名原則`、`Sass結構`來事先規範的話，  
開發後期你就會感受到專案越來越沒辦法控制。

除此之外，<a href="https://github.com/styleguide/css" target="_blank">Github</a>與<a href="http://codepen.io/chriscoyier/blog/codepens-css">codepen</a>有提出一些自己的Sass撰寫習慣，各位也可以瀏覽參考。  

## 從Sass程式碼知道自己哪裡還有不足之處
有些人會問我CSS跟SASS、Less這類的預處理器最大差異性在哪裡，  
我個人認為使用預處理器的最大好處就是要實踐設計模式相當地方便：  
首先我們先來看一段CSS程式碼：  

	.box{
		font-size: 16px;
		line-height:24px;
		width: 120px;
		margin-right: 10px;
		border-radius:5px;
		color: #3c1c3f
	}
這樣的程式碼你可以看得出來，  
他設定了行距與字型大小，  
同時設定了一個寬度並擁有CSS圓弧效果，  
但是你從這樣的code並沒辦法了解是否其他地方有套用到此功能，  
以及它究竟有使用了哪些設計模式與原理，  
換作是Sass的話就會變成這樣： 

	.box{
		@include adjust-font-size-to($font-m);
		@include span(3);
		@include border-radius(5px)
		color: $color-gray
	}
`adjust-font-size-to`是Compass實踐文字排版垂直韻律所用，  
`span`是使用Susy2的方式編譯出你要的Grid寬度和Gutter，  
`border-radius`則是Compass CSS3的Mixin，會自動幫你編譯所有的前綴支援  
文字顏色自然是透過變數來代入。  

你可以看得出來Sass的程式碼最大的優勢就是可以利用它內建的功能(@mixin、@extend、function)等等，
來去依照設計原理給實踐出來，這樣就能讓你的Code是具有系統性的方式來設計。  
 
所以我在寫Sass的時候，  
都會去評估我設計的程式碼，  
有沒有還有哪些細節沒有被模組化、設計原理化等等，  
像有很多細節你都可以考慮套用到你的Sass架構，例如：  
1. Retina、SVG spritee  
2. Compass文字排版(垂直韻律)  
3. CSS3瀏覽器前綴詞支援  
4. 使用變數統一管理樣式(顏色、字型、留白間距)   
5. 導入設計模式規劃Sass結構(SMACSS、OOCSS、BEM、MVCSS)  
6. 導入Grid system(960grid、Susy)  

在以前傳統寫CSS時，  
要套用一些設計原理時，  
常常就必須再花時間去整理code，  
但使用Sass透過Mixin、function的方式來統一管理自己想要編譯出來的程式碼，  
管理與維護上自然方便許多。  

所以直到現在我都還會審視自己的CSS code，  
來評估該如何讓我的CSS能夠透過設計原理來實踐出來，  
並有效率地去管理。


## 因應專案性質來設計Sass結構

如果今天設計的網頁性質，  
每一個頁面的獨特性都很高，例如藝術、滾動視差，  
沒辦法建立`module(模組)`區塊來提升複用性時。  
我就會這樣來設計Sass結構：
  
	all.sass
	|-- _reset.sass
	|-- _base.sass
	|-- _layout.sass
	|-- _page.sass
	|-- page
		 |-- page1.sass
		 |-- page2.sass

將page分出有page1、page2，  
讓團隊可以分工認領A要哪幾頁，B要寫哪幾頁，  
因為是客製化比較不會有程式碼衝突的問題。  

如果是該網站是每個組件複用性比較高時，  
像是電子商務網站時，  
就可以寫成這樣：  

	all.sass
	|-- _reset.sass
	|-- _base.sass
	|-- _layout.sass
	|-- _module.sass
	|-- module
		 |-- _button.sass
		 |-- _table.sass
		 |-- _form.sass
		 |-- _grid.sass
		 |-- _l-list.sass
		 |-- _l-menu.sass
你的網頁樣式可透過`module`將已經設計好各個組件來組出一個網頁出來，  
要新增新頁時，就透過既有的Module元素來組合出來，不用再額外去新增樣式。  

所以你可以看得出來，  
因為專案性質不同，  
你的Sass結構就需要有所調整，  
如果你學得CSS/Sass設計模式更多，  
就更容易思考如何去設計出客製化的Sass結構。  
