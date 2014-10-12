#使用animate.scss增強網頁瀏覽體驗

<a href="https://www.youtube.com/watch?v=b142GI0s1gU" target="_blank">![](/images/sass/20141013-1.png)</a> 

##範例程式碼
*  <a href="https://github.com/gonsakon/bootstrap-sass-sample" target="_blank">Github 範例程式碼</a>

## 學習目標

*  了解Bootstrap Sass結構
*  能夠透過Sass變數來統一管理Bootstrap的樣式設定
*  新增一組新的按鈕樣式


## 進入主題
Bootstrap的Sass架構如下，  
你也可以到此<a href="https://github.com/twbs/bootstrap-sass/tree/master/assets/stylesheets" target="_blank">連結</a>瀏覽詳細架構
```
|- _bootstrap.scss
|- bootstrap資料夾
	|- _variables.scss
	|- _mixins.scss
	|- Mixin資料夾
		|- _button.scss
		|- _其他元件.scss
     
```
我們從上往下瀏覽下來，  
根目錄的`_bootstrap.scss`自然是載入所有的子檔案Bootstrap用的，  
裡面載入的<a href="https://github.com/twbs/bootstrap-sass/blob/master/assets/stylesheets/_bootstrap.scss" target="_blank">先後順序</a>則是： 
*  變數
*  Mixin
*  CSS Reset
*  核心CSS(按鈕、表格、表單、格線系統)
*  組件(下拉選單、頁碼表、麵包屑、navbar、按鈕群組)
*  JS組件
*  公用(clearfix、text-hide、RWD)  


## 變數
Bootstrap所有的設定都可以透過Boostratp的<a href="https://github.com/twbs/bootstrap-sass/blob/master/assets/stylesheets/bootstrap/_variables.scss" target="_blank">_variables.scss</a>來設定，  
Bootstrap的顏色設定則是先設定了一組顏色變數，  
要使用時，則再透過語意化命名來提取它，例如像這樣子：  
```
$brand-primary:         #428bca !default;
$brand-success:         #5cb85c !default;
$brand-info:            #5bc0de !default;
$brand-warning:         #f0ad4e !default;
$brand-danger:          #d9534f !default;

//** Global textual link color.
$link-color:            $brand-primary !default;
```
上面五個就是Bootstrap的預設五種顏色色系，  
像譬如說，我今天希望我所有網頁上的網頁連結都要變成是`$brand-primary`的顏色時，  
我就抽象命名一個`$link-color`的方式，將顏色變數帶進去，  
這樣有助於我們在閱讀時，可以透過變數命名來知道他的用處，  

Bootstrap的核心CSS都有繼承預設色系，  
你可以試著將顏色變數修改就會發現，  
所有的核心CSS與各個組件的色系也跟著修改了，  
再加上Bootstrap的每個細節都有用變數來統一管理，  
想要客製化自己所要的theme自然得心應手。  

## 如何新增一組新的按鈕樣式
你會發現Bootstrao就只有五種的主要顏色色系，  
但如果今天你的網站需要更多種的按鈕樣式時，  
如何透過它的結構來新增樣式呢？  
這時就必須要先了解他的設計模式，  

首先來講他的設計核心CSS的流程，  
這裡自然以按鈕來當範例，  
###流程一 建立按鈕變數
在`_variables.scss`透過全域顏色變數新增各按鈕變數：
```
$brand-primary:         #428bca !default;
$brand-success:         #5cb85c !default;
$brand-info:            #5bc0de !default;
$brand-warning:         #f0ad4e !default;
$brand-danger:          #d9534f !default;

$btn-primary-color:              #fff !default; //按鈕文字顏色
$btn-primary-bg:                 $brand-primary !default; //按鈕背景顏色
$btn-primary-border:             darken($btn-primary-bg, 5%) !default; //按鈕border顏色
```

### 流程二 設定按鈕mixin與輸出class
再來Bootstrao會有兩個_button.scss，  
一個是拿來處理button <a href="https://github.com/twbs/bootstrap-sass/blob/master/assets/stylesheets/bootstrap/mixins/_buttons.scss" target="_blank">mixin</a>用的，  
另一個則就是拿來<a href="https://github.com/twbs/bootstrap-sass/blob/master/assets/stylesheets/bootstrap/_buttons.scss#L57" target="_blank">輸出class</a>用，裡面各個按鈕class自然有用到mixin設定。  
如下程式碼：  
```
//mixin資料夾裡面的 _button.scss
@mixin button-variant($color, $background, $border) {
  color: $color;
  background-color: $background;
  border-color: $border;

  &:hover,
  &:focus,
  &:active,
  &.active,
  .open > &.dropdown-toggle {
    color: $color;
    background-color: darken($background, 10%);
        border-color: darken($border, 12%);
  }
  &:active,
  &.active,
  .open > &.dropdown-toggle {
    background-image: none;
  }
  &.disabled,
  &[disabled],
  fieldset[disabled] & {
    &,
    &:hover,
    &:focus,
    &:active,
    &.active {
      background-color: $background;
          border-color: $border;
    }
  }

  .badge {
    color: $background;
    background-color: $color;
  }
}
//輸出class用的 _button.scss
.btn-default {
  @include button-variant($btn-default-color, $btn-default-bg, $btn-default-border);
}
.btn-primary {
  @include button-variant($btn-primary-color, $btn-primary-bg, $btn-primary-border);
}
```
Bootstrap所有的核心CSS都是類似這樣的建立流程，  
表單、表格、格線、按鈕等等都是會有一個檔案拿來輸入class，另一個是設定Mixin。  

這樣你就可以知道，  
如果你要新增一組按鈕樣式，  
也是比照這樣的流程辦理，  
假設我要建立一個紫色的按鈕，  
流程就是： 
```
//_variables.scss  新增全域顏色變數、按鈕變數
$brand-primary:         #428bca !default;
$brand-success:         #5cb85c !default;
$brand-info:            #5bc0de !default;
$brand-warning:         #f0ad4e !default;
$brand-danger:          #d9534f !default;

$brand-pink:         pink !default;
$btn-pink-color:              #fff !default; //按鈕文字顏色
$btn-pink-bg:                 $brand-pink !default; //按鈕背景顏色
$btn-pink-border:             darken($btn-primary-bg, 5%) !default; //按鈕border顏色

// bootstrap / _buttons.scss 新增一個按鈕class，再把變數套上去
.btn-pink {
  @include button-variant($btn-pink-color, $btn-pink-bg, $btn-pink-border);
}

``` 
如果你要偷懶點的作法，直接在`.btn-pink`的mixin上面依序添入文字顏色、背景顏色、border顏色的色碼也可以，詳細的開發流程我也有錄影，可以再比對參考。  

##總結  
Bootstrap的Sass結構真的不錯，  
相當建議各位弄懂它的設計手法，  
保證讓你的Sass規劃功力大增！  


  
