# Sass教學手冊導讀  

<a href="http://sam0512.blogspot.tw/2013/10/sass.html" target="_blank">Sass教學手冊目錄連結</a>

## 目前的你是否適合使用Sass
如果你來到這裡，代表著你對CSS有著一定的了解，  
為了讓你能夠儘快進入學習狀況，  
這個章節主要是逐步教你如何掌握Sass。  

在你決定要學Sass前，  
你可以先瀏覽這兩篇文章，  
來評估這個語言適不適合現在的你，
1. <a href="http://ithelp.ithome.com.tw/question/10126703" target="_blank">http://ithelp.ithome.com.tw/question/10126703</a>  
2. <a href="http://ithelp.ithome.com.tw/question/10126905" target="_blank">SASS該怎麼寫？會和純CSS寫法差很多嗎？</a>  


以我自己的經驗，最好是設計過幾個網站再來碰Sass會比較好些，  
至少要知道`css reset`、了解`box-model`、行內塊狀的觀念，  
會使用`float`、`position`來排版，    
如果上面的詞彙你仍一知半解的話，  
目前的你可能還不適合學習Sass，  
因為Sass是一個更有效率地維護CSS的語言，  
如果你在基礎沒打好就直接學Sass那麼學習曲線會變得相當高。  

最後Sass有提供兩種寫法，一種是SCSS，它可以完全像是傳統CSS來撰寫，  
你甚至把副檔名從`.css`改為`.scss`也ok，  
對設計師來說比較容易上手，也是目前比較多人用的格式。  
另外一種則是Sass，寫法比較乾淨，但需要多些時間來學習，有興趣的可以瀏覽此篇文章：<a href="http://ithelp.ithome.com.tw/question/10126905" target="_blank">SASS該怎麼寫？會和純CSS寫法差很多嗎？</a>。

## 環境建立  
要開始寫Sass前，不免俗地要建立Sass開發環境，  
如果你是設計師，那就相當建議你購買<a href="http://fireapp.kkbox.com/" target="_blank">Fire.app</a>、<a href="http://incident57.com/codekit/" target="_blank">codekit</a>，  
這些軟體內建就有SASS、COMPASS開發環境，可省下你搞環境的流程，  
Fire.app的用法之前我也曾寫過一篇<a href="https://www.youtube.com/watch?v=Z_CmIMAiSiI" target="_blank">文章</a>，設計師們也可以前往參考。  
如果你是工程師，那就可以考慮使用Command-line來安裝，  
Windows可以參考<a href="http://ithelp.ithome.com.tw/question/10128634" target="_blank">這篇</a>，  Mac可以參考<a href="http://ithelp.ithome.com.tw/question/10157016">這篇</a>，Susy的部份請跳過。   
如果你暫時不想在你的電腦安裝任何軟體，想先嘗試看看Sass寫法的話，  
可以到<a href="http://codepen.io/" target="_blank">Codepen</a>、<a href="Sassmeister.com" target="_blank">Sassmeister</a>、<a href="http://jsbin.com/" target="_blank">JS Bin</a>的線上程式碼服務玩玩看，它們都有提供Sass格式的開發功能。  

這個教學手冊主要都是使用Sublime text 3來進行開發，  
如果你有其他順手的編輯器那也OK，  
但假使你是用Dreamweaver的話，建議你也可以跟著我的教學流程來改用Sublime。  
這裡也提供一些我的Sublime教學文件與影片：  
1. <a href="http://ithelp.ithome.com.tw/question/10159247" target="_blank">如何透過Sublime text 3 plugin打造Sass開發環境</a>  
2. <a href="https://www.youtube.com/watch?v=e4xBgPlSMhg" target="_blank">go to anything - 可隨意移動檔案位置</a>   
3. <a href="https://www.youtube.com/watch?v=o3zoFazTD2E" target="_blank">個人常用熱鍵</a>  
4. <a href="http://slides.com/gonsakon/5#/" target="_blank">簡報 - 換編輯器的動機</a>

## 究竟要學到哪個階段，才有辦法把CSS專案導入Sass  
這個問題也是許多網頁設計師詢問率相當高的，  
我第一個Sass專案實際上只有學一些基本功能就開始寫了，  
至少你要懂得
<a href="http://ithelp.ithome.com.tw/question/10127206" target="_blank">變數</a>、
<a href="http://ithelp.ithome.com.tw/question/10127521" target="_blank">計算</a>、
<a href="http://ithelp.ithome.com.tw/question/10127832" target="_blank">@import</a>、
<a href="http://ithelp.ithome.com.tw/question/10128138" target="_blank">@Mixin</a>、
<a href="http://ithelp.ithome.com.tw/question/10128359" target="_blank">@extend</a>、的功能，  
是每位開發者都一定會碰到的基礎核心功能，   
尤其是`@import`能夠讓你將程式碼切割成好幾份，  
讓你能夠聚焦瀏覽你想要關注的code，  
像我第一個使用Sass的專案，Sass結構長成這樣子：  

	@import "compass";
	@import "mixin"; // 放置所有全域變數與Mixin
	@import "reset"; // reset.css
	@import "extend"; // 都放@extend用的檔案
	@import "index"; // 首頁
	@import "page.."; // 內頁

如果你上面五個基礎功能都學會了，  
可參考這樣的結果試著寫第一個Sass專案，  
而掌握要領則是：  
1. 試著將時常需要寫到的設定用成Variable(變數)  
2. 共通網頁樣式使用extend進行合併  
3. 嘗試使用<a href="http://ithelp.ithome.com.tw/question/10131159" target="_blank">Compass CSS3 Mixin</a>  
4. 將各單元CSS切割出來Import  

先試著用這樣的架構寫寫看，  
學新東西最缺乏的就是踏出第一步，  
其實SCSS程式碼跟CSS寫法是一樣的，  
你也能把他單純當作CSS寫也沒關係，  
只要你嘗試用了，那你就已經是進步了。  

在設計過程中，你可以閱讀下表的連結來建立自己撰寫CSS的風格習慣：  
1. <a href="https://github.com/doggy8088/CSS-Guidelines" target="_blank">CSS-Guidelines</a>  
2. <a href="http://ithelp.ithome.com.tw/question/10161666" target="_blank">Sass Style Guide(樣式指南) - Sass、Github、Codepen</a>  

一開始碰觸`@mixin`跟`@extend`的時候，兩者可能容易搞不清楚使用時機，  
你可以瀏覽此篇<a href="http://ithelp.ithome.com.tw/question/10157149" target="_blank">文章</a>來釐清觀念。

如果你不曉得到底該如何開始，  
這裡也提供我個人的一步步上手Sass的教學流程提供參考：  
1. <a href="http://ithelp.ithome.com.tw/question/10138131" target="_blank">切圖、規劃Layout</a>  
2. <a href="http://ithelp.ithome.com.tw/question/10138444" target="_blank">Sass結構規劃、全域變數設定</a>  
3. <a href="http://ithelp.ithome.com.tw/question/10138746" target="_blank">網頁排版流程(上)</a>  
4. <a href="http://ithelp.ithome.com.tw/question/10138870" target="_blank">排版流程(下)</a>  

## 開始學習設計模式   
在以前寫CSS時，  
為了遵守一些設計模式時常會增加開發時間，  
程式碼會變得越來越難維護。  
但Sass內建的功能再加上Compass讓我們要導入設計模式就變得相當容易了。  

當你嘗試寫了一個Sass專案後，  
你可以開始學習SMACSS設計模式，  
這是我覺得目前較容易學習的設計模式，  
同時也相當適合導入Sass，  
讓你的程式碼結構變得更加容易調整。     
	 
1. <a href="http://ithelp.ithome.com.tw/question/10156313" target="_blank">SMACSS - Base、Laout</a>	 
2. <a href="http://ithelp.ithome.com.tw/question/10159948" target="_blank">SMACSS - Module Rules</a>	 
3. <a href="http://ithelp.ithome.com.tw/question/10160128" target="_blank">SMACSS - State Rules</a>	 
4. <a href="http://ithelp.ithome.com.tw/question/10160255" target="_blank">SMACSS - Theme Rules</a>	 
5. <a href="http://ithelp.ithome.com.tw/question/10161555" target="_blank">SMACSS - 結構規劃與其它補充</a>	 

SMACSS有提出一個推薦的Sass結構：  

	@import  
	   "site-settings",  
	   "mixins",  
	   "base",  
	   "states",  
	   "layout/grid",  
	   "module/btn",  
	   "module/bookmarks",  
	   "module/callout";  

site-setting的部份是基礎變數設定，  
接續下來是mixins、base、states，  
Grid的設定時常會建立在Layout上，  
所以會有一個Grid的檔案統一管理，  
再來Module就放你的獨立化的模組，  
當你讀完SMACSS再回頭看這樣的架構，  
相信會更有感覺。  

我自己推薦的SMACSS架構是這樣：  

	@import "compass";
	@import "mixin";  // 所有全域變數與Mixin  
	@import "reset";  // reset.css  
	@import "extend"; // 都放@extend用的檔案  
	@import "layout"; // 共同框架,第一層
	@import "module"; //button,form,table   
	@import "pages/index、pages1、pages2 ";     

如果你想針對Sass結構有更深入了解，可以看這兩篇文章：  

1. <a href="http://ithelp.ithome.com.tw/question/10132821" target="_blank">規劃你的Sass結構</a>
2. <a href="http://ithelp.ithome.com.tw/question/10139186" target="_blank">如何逐步整合自己的Sass資料夾</a>  

當你學完後，可以再來依序學習OOCSS、BEM、MVCSS，  
讓自己的架構可以適情況加入這些設計模式讓程式碼更加得靈活，  
你可以先瀏覽這篇<a href="http://ithelp.ithome.com.tw/question/10161196" target="_blank">文章</a>，來去評估學習路徑。  

1. <a href="http://ithelp.ithome.com.tw/question/10160437" target="_blank">OOCSS</a>  
2. <a href="http://ithelp.ithome.com.tw/question/10160545" target="_blank">BEM</a>
3. <a href="http://ithelp.ithome.com.tw/question/10160702" target="_blank">MVCSS - Styleguide</a>
4. <a href="http://ithelp.ithome.com.tw/question/10160779" target="_blank">MVCSS - Foundation</a>
5. <a href="http://ithelp.ithome.com.tw/question/10160912" target="_blank">MVCSS - Components、Structures</a>
6. <a href="http://ithelp.ithome.com.tw/question/10161057" target="_blank">MVCSS - Manifest、Vendor</a>  

## 除此之外，我還可以學哪些東西呢？  
Sass+Compass可以導入相當多的設計原理到程式碼內，  
像是文字排版其中一種實踐方式為<a href="http://www.slideshare.net/sfismy/vertical-rhythm" target="_blank">垂直韻律</a>，  
將<a href="http://ithelp.ithome.com.tw/question/10131877" target="_blank">Framework套用到Sass專案</a>，  
使用Compass內建的功能來設計<a href="" target="_blank">CSS Sprite</a>，  
不用手動＠import，<a href="" target="_blank">sass-globbing輕鬆import所有sass檔</a>，  
除此之外還有這些功能：  
1. <a href="http://ithelp.ithome.com.tw/question/10131473" target="_blank">如何透過Sass&Compass支援CSS3動畫效果</a>  
2. <a href="http://ithelp.ithome.com.tw/question/10133611" target="_blank">利用@Mixin與Sass運算建立Grid System</a>  
3. <a href="http://ithelp.ithome.com.tw/question/10136259" target="_blank">如何讓你的CSS動畫更具動態效果</a>  
4. <a href="http://ithelp.ithome.com.tw/question/10137464" target="_blank">@for+random()創造無限可能</a>  
5. <a href="http://ithelp.ithome.com.tw/question/10135991" target="_blank">透過index()與nth()來設計網站版本樣式控制管理</a>  
6. <a href="http://ithelp.ithome.com.tw/question/10159400" target="_blank">使用animate.scss增強網頁瀏覽體驗</a>  
7. <a href="http://ithelp.ithome.com.tw/question/10159555" target="_blank">如何使用Sass來管理你的Bootstrap</a>  
8. <a href="http://ithelp.ithome.com.tw/question/10159726" target="_blank">@each+Sass Maps批次新增各元素樣式</a>  

再來你也可以瀏覽我自己比較常用的Sass 3.3的功能：  

1. <a href="http://ithelp.ithome.com.tw/question/10156220" target="_blank">參考父選擇符：&</a>  
2. <a href="http://ithelp.ithome.com.tw/question/10159158" target="_blank">Sass 3.3 Source Maps</a>  
3. <a href="http://ithelp.ithome.com.tw/question/10161389" target="_blank">使用Sass Maps提升程式可讀、變數群組性</a>   

## Susy究竟好不好學？  
如果你要學Susy，  
但是不懂Grid System的話，  
建議要先了解Grid的演化史會較好些，  
學習路徑是：<a href="http://960.gs/" target="_blank">960grid</a>  > <a href="http://getbootstrap.com/css/#grid-options" target="_blank">bootstrap RWD grid</a> > susy。  
這樣你才能了解為什麼Susy那麼多人推薦。 

Susy有兩個版本各別是Susy1與Susy2，  
有人問我先學1以後學2會不會比較快？  
其實1跟2差還蠻多的，直接學2比較好，  
因為Susy2裡面就有Susy1的功能了。

Susy2的教學連結如下，記得要從第一章慢慢看起，  
直接跳後面章節章節會看不懂的。

0. <a href="http://ithelp.ithome.com.tw/question/10158915" target="_blank">Susy2學習摘要</a>  
1. <a href="http://ithelp.ithome.com.tw/question/10157016" target="_blank">如何打造Susy2開發環境</a>  
2. <a href="http://ithelp.ithome.com.tw/question/10155687" target="_blank">Grid settings(上)</a>  
3. <a href="http://ithelp.ithome.com.tw/question/10155815" target="_blank">Grid settings(中)</a>  
4. <a href="http://ithelp.ithome.com.tw/question/10155937" target="_blank">Grid settings(下) debug Compass Vertical Rhythm</a>  
5. <a href="http://ithelp.ithome.com.tw/question/10156066" target="_blank">960Grid 固定版型(Fixed layout)設計</a>  
6. <a href="http://ithelp.ithome.com.tw/question/10156169" target="_blank">960Grid 流體版型(Fulid layout)設計，susy1&gt;susy2轉換</a>  
7. <a href="http://ithelp.ithome.com.tw/question/10156478" target="_blank">mobile to desktop responsive grid with breakpoint</a>  
8. <a href="http://ithelp.ithome.com.tw/question/10156589" target="_blank">透過susy-breakpoint、layout設計RWD Grid</a>
9. <a href="http://ithelp.ithome.com.tw/question/10156708" target="_blank">不對稱(Asymmetrical) RWD Grid</a>  
10. <a href="http://ithelp.ithome.com.tw/question/10156963" target="_blank">使用with layout讓版型同時存在兩種以上的Grid</a>
11. <a href="http://ithelp.ithome.com.tw/question/10157325" target="_blank">實作Bootstrap3 RWD Grid</a>  
12. <a href="http://ithelp.ithome.com.tw/question/10157547" target="_blank">shorthand(簡寫)</a>  
13. <a href="http://ithelp.ithome.com.tw/question/10157777" target="_blank">Toolkit - span Mixin、function</a>  
14. <a href="http://ithelp.ithome.com.tw/question/10157982" target="_blank">Toolkit - gutter、container</a>  
15. <a href="http://ithelp.ithome.com.tw/question/10158151" target="_blank">Toolkit - Rows &amp; Edges</a>  
16. <a href="http://ithelp.ithome.com.tw/question/10158505" target="_blank">Susy2 語法速記表</a>  
17. <a href="http://ithelp.ithome.com.tw/question/10158384" target="_blank">Susy2 網路教學資源</a> 
18. <a href="http://ithelp.ithome.com.tw/question/10158679" target="_blank">使用Susy2前，你必須要懂的CSS觀念</a>  

如果你仍有Susy1的專案，也可以瀏覽下面我寫的教學：  

1. <a href="http://ithelp.ithome.com.tw/question/10139425" target="_blank">Susy Grid教學(上)</a>  
2. <a href="http://ithelp.ithome.com.tw/question/10139587" target="_blank">Susy Grid教學(下)</a>  
3. <a href="http://ithelp.ithome.com.tw/question/10139734" target="_blank">Off-Canvas layout with Susy</a>  
4. <a href="http://ithelp.ithome.com.tw/question/10139889" target="_blank">Susy 版型種類介紹</a>  
5. <a href="http://ithelp.ithome.com.tw/question/10140181" target="_blank">Compass Vertical Rhythm &amp; Susy other setting</a>  
6. <a href="http://ithelp.ithome.com.tw/question/10140341" target="_blank">Susy RWD Grid排版流程(上)</a>  
7. <a href="http://ithelp.ithome.com.tw/question/10140472" target="_blank">Susy RWD Grid排版流程(下)</a>    


##結論  
相信透過這樣一系列的導讀，  
就能找到自己學習Sass的流程，  
有些連結沒有列上的部份你可以再到<a href="http://sam0512.blogspot.tw/2013/10/sass.html" target="_blank">Sass教學手冊目錄連結</a>來瀏覽。  
遇到問題的話也歡迎透過<a href="https://www.facebook.com/sfismy" target="_blank">Facebook</a>聯繫我嘍^_^
