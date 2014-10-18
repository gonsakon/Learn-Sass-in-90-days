# BEM
##youtube影片教學  
<a href="https://www.youtube.com/watch?v=1koKr0-k8Wc" target="_blank">![](/images/video/20141019-2.png)</a>  

##程式碼連結 & 圖片來源

* <a href="http://oocss.org/" target="_blank">BEM</a>   
* <a href="http://bem.info/method/definitions/" target="_blank">What is BEM?</a> 
* <a href="http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/" target="_blank">MindBEMding – getting your head ’round BEM syntax</a>  

BEM由Yandex團隊提出來的一種創新命名Class名稱的設計模式，  
如果你還不熟悉SMACSS或OOCSS章節的話，  
建議先熟悉那兩個章節再來了解BEM比較不會吃力些。  

BEM的意思是區塊（Block）、元素（Element）、修飾符（Modifier），  
它們最大的優勢就是可以光瀏覽class名稱就能夠告訴開發者它們彼此間的依賴關係。  
在進入BEM的解說前，  
我們先來聊一下以前在設計CSS容易遇到的狀況，    
一般我們在閱讀下面的HTML結構時：  
```
<ul class="menu">
    <li class="item active"><a href="#"></a></li>
    <li class="item"><a href="#"></a></li>
</ul>
```  
不論是你看別人的code，  
或者是你有一兩天沒寫又回頭看時，  
都會思考著這樣的問題：  
1.class裡的product與menu是否有互相關聯？例：`.product .menu`  
2.還是說product是`layout`，menu是`module`，兩者其實並無關係？  
3.li裡面的active是否為list裡面的範圍域？  

通常網頁設計師碰到這樣的code，  
自然就會去翻他的CSS，來找出他們的關係，  
假使有用到Sass的@import功能，  
要找可能也會找一段時間。  

但如果是用BEM命名，  
class命名規則就會改為：  
```
<div class="product">
    <div class="menu">
        <li class="menu__item menu__item--active"><a href="#"></a></li>
        <li class="menu__item"><a href="#"></a></li>
    </div>
</div>
```  
在我第一次看到這種code的時候，  
說實話我心裡也是OS：「這什麼邪門歪道啊」，  
但了解他的邏輯再回頭來看code就覺得還蠻直覺易懂的，  
所以到這裡我們就開始進入主題吧。  

```
.block{} //區塊 (Block)
.block__element{} //元素 (Element)
.block--modifier{}//修飾符（Modifier）
```
## 區塊 (Block)
我們在設計網站時，  
一定會設計幾個區塊(Block)出來，  
如下圖表頭裡面有LOGO、選單、搜尋框、登入視窗等等，  
這樣才能方便移動整個區塊到對應位置，  
這時候我們就會用class命名他們區塊對應的語意，  
例如`.menu`、`.logo`、'.search'、'.auth'，  
<img src="../../images/sass/20141018-3.png" height="573" width="1024" alt="">

## 元素 (Element)  
再來我們深入menu的區塊，  
你可以看到下圖選單內有四個元素，  
如果這些元素設定是會綁定在這個區塊上時，  
就可以在區塊的class後面加上雙下底線`__`來辨識他是該區塊底下的元素，  
Class就會設計為`.menu__item{} `。  
PS：除了HTML tag外，如果是一個CSS組件也可把它視為元素 (Element) 。
<img src="../../images/sass/20141018-4.png" height="377" width="617" alt="">  
## 修飾符（Modifier）
修飾符（Modifier）的觀念和SMACSS的<a href="../SMACSS/3.State Rules.markdown">State Rules</a>很相似。  
當區塊或元素因為狀態而改變時，  
就在後面加上雙中線`--`來辨識它是修飾符，  
像是下圖選單的部份，當被點選時為了要讓使用者了解該元素有被點選，  
所以就會用javascript動態加入class為`.menu__item--active`，  
所以如果我們要判斷這個class是屬於元素還是修飾符的設定，  
就只要看class最後面是雙中線`--`還是雙下底線`__`就知道他是屬於哪一種了。  
<img src="../../images/sass/20141018-5.png" height="135" width="447" alt="">   
修飾符（Modifier）可以使用的時機非常多，  
除了狀態更動外，樣式設計也可以放到修飾符內，  
這裡來舉一些例子：  
(1)滑鼠點選某個元素(Element)時，動態新增一個`.element--Modifier`來更換元素樣式。  
(2)新增一個新按鈕時，我們可以這樣子設計`btn btn--green clearfix`，就能了解`btn--green`是一個修飾符。  
(3)原本為滿版的搜尋區塊要變成三分之一大小的區塊時，就可以這樣寫：`search search--1of3`   

所以我們再來看一些程式碼，  
加深我們對BEM的印象：  
####  一個Block裡面有兩個元素，Block區塊還有個修飾符來更動它的狀態  
```
//
<form class="site-search  site-search--full">
    <input type="text" class="site-search__field">
    <input type="Submit" class="site-search__button" value ="Search" >
</form>
```

#### 下面的程式碼，我們看不懂`.media`和`body`是否有相關聯
```
<div class="media"> //.media
    <img src="logo.png" alt="Foo Corp logo" class="img-rev">
    <div class="body"> //.body
        <h3 class="alpha">Welcome to Foo Corp</h3>
        <p class="lede">Foo Corp is the best, seriously!</p>
    </div>
</div>
```
#### 但這樣子寫你就看得出來說，`.media`裡面有一個`.media_body`的元素，不過裡頭的h3與p則是獨立沒有關聯。
```
<div class="media">
    <img src="logo.png" alt="Foo Corp logo" class="media__img--rev">
    <div class="media__body">
        <h3 class="alpha">Welcome to Foo Corp</h3>
        <p class="lede">Foo Corp is the best, seriously!</p>
    </div>
</div>  
```
## 什麼時機不會需要用到BEM 
#### 如果可以獨立成為一個class，具有複用性 
當我們網站內容有個CSS設定時常會用到其他地方時，  
就會把他獨立成一個class名稱提升他的複用性，  
例如清除浮動就是一個例子，  
我們可能會在很多的元素上用到這個語法`.clearfix{clear:both}`，  
或者是置左功能`.pull-left{float:left}`。  

#### 並不是所有的元素都要遵守BEM的規則
假設來說我`.content`裡面有個選單元素，  
所以你就寫了`.content__menu`，  
但你必須去了解這個元素是否會在表尾、側欄其他地方出現，  
如果會的話，那就應該是從.menu當做一個區塊來向內延伸設計把它變成一個Module模組才對。 

## Sass 3.3 支援BEM設計模式  
BEM在以前還不讓人接受的其中一個原因是，  
在寫class時都還必須撰寫前面的class名稱才有辦法繼續寫下去，  
例如下面的程式碼，我每次寫都還必須寫前面的.media才有辦法繼續寫下去，  
這樣就必須打很多重複的code： 
```
.media{}
.media--full{}
.media__submit{}
.media__img{}
.media__img--border{}
```
但自從Sass3.3開始支援`&`能夠連接字串後，就能簡化成這樣的方式，同樣也能得到上面的結果：
```
.media{
  &--full{}
  &__submit{}
  &__submit{
    &--border{
    }
  }
}
```  
當然如果你看不習慣這樣的SASS CODE，  
自己手寫也ok的。  

##總結  
BEM的功能主要就是要讓你在瀏覽HTML CODE時，  
能夠透過觀察class，就能了解你的CSS架構，  
讓你不用再回去追CSS Code才辨別得出哪些是`Layout`、`Module`、`OOCSS`，  
就算你專案沒打算使用BEM，那也可以套用其觀念，讓團隊都有個一致的命名規則，  
讓同事都能一目了然地看懂網站上的架構。  
