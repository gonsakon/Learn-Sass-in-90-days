# MVCSS - Components、Structures

##程式碼連結
* <a href="http://mvcss.github.io/" target="_blank">MVCSS</a>
* <a href="http://mvcss.ycnets.com/" target="_blank">MVCSS中文翻譯</a> 

## Components(組件)
具有辨識性的UI皆放在Components的Sass目錄裡面，  
這些命名通常都會是抽象命名，  
抽象命名的觀念其實和SMACSS的<a href="https://github.com/gonsakon/Learn-Sass-in-90-days/blob/master/docs/SMACSS/1.markdown#layout" target="_blank">Layout Rules</a>相似的。  
這樣你才能確保你的模組能夠任意移動到各區塊去，  
同時又不會造成語意上的混亂。  

像以MVCSS裡面有提到一個範例，  
`g`(Grid抽象命名)和`card`用來處理Layout與container，  
同時裡面可以能夠包含許多模組：  
```
<div class="g">
  <div class="g-box g-b--1of2">
    <div class="card">
      <!-- Content -->
    </div>
  </div>
  <div class="g-b g-b--1of2">
    <div class="card">
      <!-- Content -->
    </div>
  </div>
</div>
```  
其他的Components像是`thumb`只會影響一個元素，  
乍看之下跟`tools`的觀念很像，  
兩者的差異是Components可以透過Bem的`modifier`的觀念來延伸樣式，但`tools`不行：  
```
<div class="bucket">
  <div class="bucket-media">
    <img class="thumb thumb--m" src="avatar-nick.jpg" alt="Nick Walsh">
  </div>
  <div class="bucket-content">
    <p>Nick Walsh</p>
  </div>
</div>
```   
## Structures
Structures的觀念時常用在某些特定情境或內容類型，  
在一些情境下，也會用在主題樣式或RWD響應式網站上。  

有些開發者時常會將`Component`與`Structure`混淆，  
所以MVCSS提出了三種辨別的方式來幫助我們在兩者間進行辨別。  

1. 作用範圍大小  
2. 依賴其他模組  
3. 專案間是否具有可移植性，或者是沒有  

#### 1.作用範圍大小 
當一個Module(模組)會影響一個元素或元素間的排列(譬如他的樣式範圍很廣泛)，那就代表你處理的結構有很大的可能是`Structure`。  

假如你正在設計一個相當常見的網站，  
header表頭裡面左邊有logo，  
再加上一些水平導覽列`nav`在右邊。  
你可以使用一個`Helpers`、`Components`和 `Tools` 的組合來設計。   
```  
<header class="group">
    <img class="fl">
    <nav class="fr">
        <ul class="list list--inline">
            <li class="list-item"><a href="/">Home</a></li>
            <li class="list-item"><a href="/blog">Blog</a></li>
            <li class="list-item"><a href="/contact">Contact</a></li>
        </ul>
    </nav>
</header>
```
這樣的架構在PC版型上或許沒問題，  
但假使我們要設計RWD響應式網頁的時候會發生什麼事？  
在低螢幕解析度的行動裝置上，如果希望導覽列有這些功能：  
* 填滿 viewport寬度
* Stack links atop one another
* 使用交替色在列表背景上  

在PC上我們的導覽列是水平的，  
所以我們在`ul`上面使用了`list--inline`的設定，  
但假使這個網站有RWD時，  
導覽列自然會變成垂直從上到下的排版方式，  
這樣他就不會是`inline`的排版了，    
在語意越來越混亂時，就會導致開發上的困難。  

在這樣的情況下，  
最好的辦法就是創造一個新的結構(Structures)，  
並且在裡面定義新的主題與RWD響應式清單模組。  

#### 2. 依賴其他模組 
不像是Components，Structures可以依賴，甚至可使用擴充(extend),以及預先存在的Components，  
這個方法在想要添加主題或行為到一個Component是非常有用的，  
但也請記得要保持獨特得變化在裡面。  
在MVCSS的架構，主要是使用`g`(Grid)的Component在網頁排版上，  
並且嘗試保持簡單，但有些情況下會希望在更特別的模組引入既有的Component。  
像下面的例子就是定義了一個`collection`的結構，  
在`nth-child(3n + 1)`清除浮動，  
增加該模組的Grid的變化性：    
```
.collection

// -------------------------------------  
//   Modifiers
// -------------------------------------  

.collection--1of3

  .collection-item:nth-child(3n + 1)
    clear: left

// -------------------------------------  
//   Scaffolding  
// -------------------------------------  

// ----- Item ----- //  

.collection-item  
  margin-bottom: $b-space-l  
```
在上面有提到MVCSS是使用`g`(Grid)的Component來排版，  
假設有一個HTML結構有用到`collection`的架構時，  
就可以使用`g` (Grid) Component 和 `collection`Structure來組合我們想要的樣式。  

PS：使用過多的修飾符到`grid`和``grid-box`會讓HTML結構變得難以閱讀，所以簡寫成`g`、`g-b`  
```
<div class="g collection collection--1of3">
  <div class="g-b g-b--1of3 collection-item">
    <!-- Content -->
  </div>
  <div class="g-b g-b--1of3 collection-item">
    <!-- Content -->
  </div>
  <div class="g-b g-b--1of3 collection-item">
    <!-- Content -->
  </div>
  <div class="g-b g-b--1of3 collection-item">
    <!-- Content -->
  </div>
</div>
```  
但這樣還是有太多類別在套用樣式，  
要更加優化HTML結構的可讀性，  
你可以使用@extend的指令。  
```
.collection
  @extend .g

// -------------------------------------
//   Modifiers
// -------------------------------------

.collection--1of3
  @extend .g-b--1of3

  .collection-item:nth-child(3n + 1)
    clear: left

// -------------------------------------
//   Scaffolding
// -------------------------------------

// ----- Item ----- //

.collection-item
  @extend .g-b
  margin-bottom: $b-space-l
```
我們在Sass裡面繼承了`g`、`g-b`的Component，  
同時再撰寫獨特的樣式在`.collection-item`裡面，  
這樣HTML結構就能變得這麼漂亮了：  
```
<div class="collection collection--1of3">
  <div class="collection-item">
    <!-- Content -->
  </div>
  <div class="collection-item">
    <!-- Content -->
  </div>
  <div class="collection-item">
    <!-- Content -->
  </div>
  <div class="collection-item">
    <!-- Content -->
  </div>
</div>
```  
#### 3. 專案間是否具有可移植性，或者是沒有  
上面兩點的作用範圍大小和是否依賴其他模組都會影響可移植性，  
當你在判斷你現在設計的CSS區塊與組件能夠隨意在各個區塊套用時，那就代表他具有可移植性，你便能把他歸類為Component。  
但另一方面如果在你在一個模組區塊上寫了一定數量的程式碼，  
那就表示把該模組分類成Structure會更好一些。
