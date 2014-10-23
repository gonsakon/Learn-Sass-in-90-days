# 這麼多Sass/css設計模式，究竟該如何逐步學習？  

以目前台灣比較熱門的CSS設計模式有： 
* <a href="https://smacss.com/" target="_blank">SMACSS</a>
* <a href="http://oocss.org/" target="_blank">OOCSS</a>
* <a href="http://Bem.info/" target="_blank">BEM</a>
* <a href="http://mvcss.github.io/" target="_blank">MVCSS</a>

較常見的前端框架有：
* <a href="http://getbootstrap.com/" target="_blank">Bootstrap</a>
* <a href="http://purecss.io/" target="_blank">Pure</a>

我個人建議的學習途徑是：
SMACSS>Pure>OOCSS>Bootstrap Sass>Bem>MVCSS

如果你已經設計過幾個網站，  
開始面臨到撰寫的CSS CODE 靈活性、可維護性遇到瓶頸時，    
那麼我個人建議先學習`Smacss`與`Pure`這兩個會比較好，  
尤其Pure更是以`Smacss`設計模式來延伸的，  
再加上它較輕量，也會在寫註解讓你知道他如何設計結構。  
這裡就來舉出兩個Pure的的設計手法，

###<a href="http://purecss.io/base/" target="_blank">Pure - Base </a> 
Pure裡面有一個CSS區塊是`Base`，  
這部份有參考<a href="https://github.com/gonsakon/Learn-Sass-in-90-days/blob/master/docs/SMACSS/1.markdown#base" target="_blank">SMACSS - Base</a>的觀念，除了使用Reset CSS外，   
也可以去思考有哪些HTML tag時常會用到哪些樣式，  
並直接在上面寫上CSS：  
```
a {color: #039;}
a:hover {color: #03F;}
```
這樣就不必在每個區塊上再寫一次連結顏色設定。  

而Pure - Base所使用的CSS Reset是Normalize，  
另外Base的CSS在最下面加上了Pure自己客製化的兩個全域code：  
```
[hidden] {
    display: none !important;
}
.pure-img {
    max-width: 100%;
    height: auto;
    display: block;
}
```  
`[hidden]`的功用是在Html Tag的屬性上加上`hidden`，  
該元素就會被隱藏起來，像是這樣子：  
```
<input type="text" name="_csrf" hidden>
```
第二個`.pure-img`則是拿來處理Responsive圖像用的，  
套入這語法就能讓圖片既能保持原本大小，  
同時在螢幕解析度小於圖片時，也能自適應螢幕解析度，  
我自己習慣是直接寫成這樣，這樣就不用每個img還得費勁加上class：  
```
img{
	max-width: 100%;
	height: auto;
	display: block;
}
```
###<a href="http://purecss.io/tables/" target="_blank">Pure - Table</a> 
提到這章節主要是了解如何新增子模組的流程，  
這觀念同時也參考了SMACSS - Module的 <a href="#">子模組(Subclassing Modules)</a> 觀念。 
首先我們來看Pure的table：  
<img src="../..//images/sass/20141022-1.png" alt="">
```
<table class="pure-table">
    <thead>
        <tr>
            <th>#</th> * 4
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1</td> * 4
        </tr>		
    </tbody>
</table>
``` 
如果我們需要加上水平線的話，只要在table的class寫上：  
```
<table class="pure-table pure-table-bordered">
```  
<img src="../..//images/sass/20141022-2.png" alt="">  

從上面的範例你可以看得出來，  
`pure-table`是提供預設樣的給table，  
而`pure-table-bordered`的CSS則是寫成下面這樣蓋掉預設`pure-tabe`裡面的的td樣式，  
藉由這樣的方式替模組增加子模組樣式：  
```
.pure-table-bordered td {
    border-bottom: 1px solid #cbcbcb;
}
.pure-table-bordered tbody > tr:last-child td,
.pure-table-horizontal tbody > tr:last-child td {
    border-bottom-width: 0;
}
```
你可以透過這樣的設計流程來設計其他模組，  
例如Pure的按鈕也是這樣設計的：  
<img src="../..//images/sass/20141022-3.png" alt="">  
首先在`pure-button `寫預設的樣式，  
今天要設定不同顏色，就再加個`pure-button-primary`來覆蓋，  
所以`pure-button-primary`的CSS就只有寫成這樣：  
```
.pure-button-primary{
	background-color: #0078e7;
	color: #fff;
}
``` 
透過這樣的思維，  
你就可以思考你的模組的變化性，  
再藉由子模組(Subclassing Modules)的觀念來豐富你的模組的多樣性，  
同時也能顧慮到程式碼的可維護性、可擴充性。 

上面提到的只是SMACSS的其中細節而已，  
你可以一邊觀察SMACSS的設計模式，再一邊看Pure的前端框架，  
相信會對它有著更深入的了解。  

## OOCSS
在你稍微了解SMACSS，並開始逐步套用在專案中的時候，  
可以再深入學習<a href="https://github.com/gonsakon/Learn-Sass-in-90-days/blob/master/docs/CssDesignPattern/OOCSS.markdown" target="_blank">OOCSS</a>的觀念，  
有時候我們在寫`模組(Module)`時，  
常會寫到一些重複性很高的程式碼，  
例如`float:left`、`clear:both`，  
如果每個模組都還要重複性寫這些語法就會導致程式碼太臃腫。  
所以就可以寫類似這樣的code出來，並在html tag直接加上class即可。  
```
//CSS CODE
.clearfix{clear:both}
.fl{float:left}
.fr{float:right}
//HTML 結構  
<div class="card clearfix">
  <img class="fl"
  <p>test word</p>
</div>
``` 
從上面的HTML結構，  
我們就能得知CSS的關聯性， 
`card`是一個區塊，但這個圖片有些時候是要置左、有些時候要置右，  
有的時候又可能都不要，  
這時候OOCSS就派得上用場了，  

所以你在設計網頁時，
也可以考慮樣一些常用的設定給獨立出來，  
設計模組(SMACSS - module)時再搭配OOCSS就能夠更快產出你要的樣式。
同時節省不少重複寫code的負擔。  

## BEM 

延續OOCSS，  
像是上面的範例是很單純的`.card`裡面有img與p段落，  
但有時候一個CSS組件裡面有太多的元素組成，  
為了讓我們能夠一目了然透過HTML結構就能了解CSS關聯性，  
你可以考慮導入<a href="https://github.com/gonsakon/Learn-Sass-in-90-days/blob/master/docs/CssDesignPattern/BEM.markdown" target="_blank">Bem</a>	設計模式， 
像下面的Bem程式碼範例，我們就能得知
雙下底線我們就曉得這是該區塊block底下的元素，  
雙中線就是該區塊上獨特的樣式 。
```
.block{} //區塊 (Block)
.block__element{} //元素 (Element)
.block--modifier{}//修飾符（Modifier）
```
再來我們來看一個融合了SMACSS、OOCSS、BEM的範例：  
```
<header class="group">
    <img class="fl" alt="Website">
    <nav class="fr">
        <ul class="list list--inline">
            <li class="list__item">選單一</li>
            <li class="list__item">選單二</li>
            <li class="list__item">選單三</li>
        </ul>
    </nav>
</header>
```  
從上面就可以得知，  
group可能只是個`layout`，因為裡面的子元素並沒有任何有相關聯，  
`fl`、`fr`一看就曉得他是OOCSS的置左、右功能，  
再來裡面有一個list模組，增加了一個子模組，並用修飾符的命名規則。  
list裡面的li程式碼是有關聯性的，表示他是list模組裡面的子項目。  

## MVCSS  
MVCSS結合了非常多的設計模式更是結合了前面三者的設計流程，  
同時參考了許多熱門的前端框架，  
針對Sass的Styleguide、@import結構、命名規則都有著相當不錯的設計規範，  
我自己本身也有套用一些它裡面的規範，  
建議先將SMACSS、OOCSS、BEM這三個設計模式有初步的認識再來了解MVCSS較不會有障礙。  
  
##結論  
學習設計模式就像是你開始有自己的房間，  
但因為不懂整理訣竅所以東西雖然收整齊了，但過沒多久就又開始亂了，  
那就表示你收納、清潔的方式不對，  
所以就必須倚賴一些置物器具(筆筒、書櫃)來替你做有效的歸位，  
這樣才有辦法讓你的房間能夠井然有序得排列整齊。  

相信各位看上面那段話，其實把`CSS`、`網站`的詞彙套上去也是共通的，  
所以逐步找到自己整理房間的方法，讓它變得越來越乾淨、好清理吧！
