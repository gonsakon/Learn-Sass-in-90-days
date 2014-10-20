# MVCSS - Foundation

##程式碼連結
* <a href="http://mvcss.github.io/" target="_blank">MVCSS</a>
* <a href="http://mvcss.ycnets.com/" target="_blank">MVCSS中文翻譯</a> 

## Foundation 
Foundation是指當你要使用MVCSS設計模式來建立你的Sass結構時，  
所需要的預設設定，你也可以當做是當Sass專案創建時，預設會載入的初始設定。

一個MVCSS的專案結構會長成如下：  
```
application.sass
foundation/
  _reset.sass
  _helpers.sass
  _config.sass
  _base.sass
  _tools.sass
components/
structures/
vendor/
```
而foundation的組成如下：
1. Reset  
2. Helpers
3. Config
4. Base
5. Tools

## Foundation - Reset
我們在建立專案前，都會先導入Reset css先將所有瀏覽器的預設CSS樣式給清空，  
MVCSS是使用<a href="http://necolas.github.io/normalize.css/">， Normalize.css</a>，如果你不習慣它的Reset.css，也可以考慮使用 Eric Meyer 的 <a href="http://meyerweb.com/eric/tools/css/reset/reset.css" target="_blank">Reset CSS </a>。  
關於各種版本的Reset CSS差異性，   
我也寫過一篇<a href="http://ithelp.ithome.com.tw/question/10129547" target="_blank">文章</a>，各位可以從中評估並挑選自己上手的即可。  

## Foundation - Helpers 
Helpers是指專案上有用到的`functions`、`@Mixin`、`extend`、`animations`。 

**functions、@mixin**  
Sass、Compass其實就有很多好用的function使用了，  
但如果你有自己寫functioin與@Mixin那便也可以自行新增。  

**Extends**  
在MVCSS的觀念有個很有趣的一點是，  
應該要盡量避免使用`%`佔位選擇符，  
MVCSS提出了一個清除浮動的設定來解說：  
```
// ----- Clearfix ----- //

.group::after
  clear: both
  content: ''
  display: table
```  
`%`佔位選擇符的功用自然是能夠將class堆疊起來，  
但這樣同時也會造成堆疊的code變得擁擠，  
與其如此，倒不如直接在HTML TAG上面直接載入`.group`即可，  
這樣的概念也與OOCSS有些雷同：  
```
<footer class="group">  
  <p class="fl">Made with Envy</p>  
  <p class="fr" src="" alt="Envy Logo">test</op>
</footer>  
```  
假使有些模組會用到時，  
便直接繼承`.group`，  
```
.g  
  @extend .group  
  display: block  
  margin-left: -$g-gutter / 2  
  margin-right: -$g-gutter / 2  
```  
個人補充一點，  
但這樣並不代表`%`佔位選擇符就沒有用處，  
有些時候在每個區塊的文字字體都不一樣時，  
便可以透過這樣來管理字體：  
```
%helvetica
	"Helvetica Neue", Arial, sans-serif
%segoe
	"Segoe UI", "Myriad Pro", "Helvetica Neue", Arial, sans-serif
h1  
	@extend %segoe  
p,li  
	@extend %helvetica
.search .title
	@extend %segoe    
```  
**Animations** 
在Helpers中，應把全站的動畫(Animations)設定都集中起來，  
並可靈活套用於各種模組上，  
除非是特別的動畫模組才會在該模組下方直接寫Animations，  
否則都應整合在Helpers的Animations裡面。  

## Foundation - Config  
Config則是拿來設定所有變數與字型的地方。下面的範例將拆解為Base、Colors和Fonts的設定。  
**@Font-face** 
MVCSS的範例是引入了Bourbon的`+font-face mixin`提供字體檔案，  
但如果你已經有使用自己的網頁字體與服務的話，便可留空此段。  

**Variables(變數)**  
MVCSS的變數為了與它們的功能有所相呼應，  
都會加上前綴詞來了解該變數是屬於`Component(組件)`還是`Structure(結構)`，  
* ww
* `$b-*` 基礎變數
* `$c-` 顏色
* `g-` RWD斷點(breakpoints)
* $componentName-* 使用在 `Components(組件)`
* $structureName-* 使用在 `Structures(結構)`
```  
顏色的部份則是先定義一組顏色變數，  
再設計一組有語意化的來繼承，  
不過假使你的專案色系並沒有分到那麼細，  
那麼直接使用顏色變數也可以。  
```
// -------------------------------------  
//   Colors  
// -------------------------------------  

// ----- Palette ----- //  

$cerulean: #017ba7
$forest: #7ba05b
$gainsboro: #ecf0f1
$gold: #ffd700
$jet: #343434
$scarlet: #ff3f00
$white: #fff

// ----- Base ----- //

$c-background-invert: $white
$c-background: $gainsboro
$c-border: lighten($jet, 30%)
$c-error: $scarlet
$c-highlight: $cerulean
$c-text-invert: $white
$c-text: $jet
$c-subdue: lighten($cerulean, 40%)
$c-success: $forest
$c-warning: $gold

// ----- Components ----- //

// 範例：$row--a-background: $c-highlight

// ----- Structures ----- //

// 範例：$dropdown-link-color: $c-subdue

// -------------------------------------  
//   Base  
// -------------------------------------  
  
// ----- Borders & Box Shadow ----- //  

$b-borderRadius: 3px
$b-borderStyle: solid
$b-borderWidth: 2px
$b-border: $b-borderWidth $b-borderStyle $c-border
$b-boxShadow: 0 2px 0 rgba($jet, 0.25)

// ----- Typography ----- //

$b-fontFamily-heading: 'OpenSans', sans-serif
$b-fontFamily: 'OpenSans', sans-serif
$b-fontSize: 16px
$b-fontSize-s: 75%
$b-fontSize-m: 90%
$b-fontSize-l: 115%
$b-lineHeight: 1.5

// ----- Sizing ----- //

$b-space: em(20px)
$b-space-s: 0.5 * $b-space
$b-space-l: 2 * $b-space
$b-space-xl: 4 * $b-space

// -------------------------------------
//   Components
// -------------------------------------

// ----- Grid ----- //

$g-s: em(480px)
$g-m: em(800px)
$g-l: em(1024px)

// -------------------------------------  
//   Structures  
// -------------------------------------  

// ----- Dropdown ----- //

// example：$dropdown-width: em(200px)
```  
## Foundation - Base 
Base則是針對HTML TAG直接寫全域CSS樣式，  
以避免每個不同區塊的HTML TAG都還必須重新設定一次，  
因為HTML TAG太多，所以通常只會針對重點來設計樣式。  

MVCSS是先在頂端定義`html`和`body`樣式後，  
後面再分為`Block(塊狀樣式)`、`inline(行內樣式)`依序設定。  

HTML與BODY範例設定如下程式碼，  
透過下面的前綴詞，你一目了然就曉得`c-`是顏色變數，  
`b-`是來自於config的`base`的預設樣式：  
```
html
  background: $c-background
  color: $c-base
  font-family: $b-fontFamily
  font-size: $b-fontSize
  line-height: $b-lineHeight

body
  font-size: 100%
```  

**Block Content(塊狀內容)**    
在設計Base預設樣式的塊狀HTML tag時，  
設計原則是：  
1. 如確定特定HTML tag在全站樣式都長得一樣，可直接在HTML tag寫樣式
2. 為了避免外邊界疊加增加複雜度，所以限制垂直Margin為單一方向  
```
ul, p
  margin-bottom: $b-space
  margin-top: 0

li
  margin-bottom: $b-space-s
  margin-top: 0
h1, .h1,
h2, .h2,
h3, .h3,
h4, .h4
  font-family: $b-fontFamily-heading
  font-weight: bold
  line-height: 1.2
  margin-bottom: $b-space-xs
  margin-top: 0
```
**inline Content(行內內容)**    
自然是指行內元素，  
例如`a`、`strong`、`em`、`code`等等。  
```
a
  border-bottom: $b-border
  color: $c-highlight
  text-decoration: none
  &:hover,
  &:focus
    border-bottom-color: $c-highlight
    color: $c-subdue
```    
##Foundation - Tools  
MVCSS的Tools的觀念很像是<a href="https://github.com/gonsakon/Learn-Sass-in-90-days/blob/master/docs/CssDesignPattern/OOCSS.markdown" target="_blank">OOCSS</a>，  
但又不是純粹的OO，  
`Tools`的CSS設定都是可以直接指定在HTML tag的class上，  
例如，下面 card Component裡面的P段落需要用margin-bottom 對齊，所以能夠輕鬆使用一個 Tool的mbf來寫：  
```
<div class="card">
  <p class="mbf">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Veniam non dolor eligendi placeat.</p>
</div>
```
####Single Responsibility(單一職責)  
Tools盡可能限制職責，讓他越單純越好，並讓他能夠在不同組件與結構上快速產生不同樣是。每一個 Tool做一件事確保他們影響的這些元素是可預測的和可擴充的。  

#### 太超過的寫法  
如果你發現自己使用的Tools太多才能達到效果那就太超過了，  
你應該是要在模組(Module)或修飾符(Modifier)來新增樣式。  
我個人建議除非你是很純粹的OOCSS，  
否則建議Tools的結構在一個HTML TAG不要超過四個以上會比較好。  

MVCSS在文件上有提供一個範例：  
```
<a class="btn pbm pll prl ptm tsl" href="v3.zip" >Download v3.0.0</a>
<a class="btn pbm pll prl ptm tsl" href="v2.zip" >Download v2.4.1</a>
```  
在上面的例子中，雖然這樣也可以設計出一個按鈕，  
但如果每次要設計按鈕就必須寫那麼多class也是相當麻煩，  
所以MVCSS建議可以增加個修飾符(Modifier)來整合：  
```
//CSS結構
.btn--l
  font-size: $b-fontSize-l
  padding: $b-space $b-space-l
  
//HTML結構  
<a class="btn btn--l" href="v3.zip" >Download v3.0.0</a>
<a class="btn btn--l" href="v2.zip" >Download v2.4.1</a>
```  
要特別記住一點，Tools提供一組強大的class能夠針對各種情境、模組、組件上進行微調，但他並不能代替模組化的CSS。  