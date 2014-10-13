# @each+Sass Maps批次產生各元素樣式
##youtube影片教學  
<a href="https://www.youtube.com/watch?v=oZ79Vu4n5MA&feature=youtu.be" target="_blank">![](/images/sass/20141014-1.png)</a>
##範例程式碼
*  <a href="http://sassmeister.com/gist/71f07f3ac51aeb49ea19" target="_blank">sassmeister-程式碼範例</a>
*  <a href="http://www.sitepoint.com/sass-component-10-minutes/" target="_blank">A Sass Component in 10 Minutes</a>


如果你還沒先瀏覽這一篇<a href="http://sassmeister.com/gist/603cc93c8b7307bdfee2" target="_blank">如何使用Sass來管理你的Bootstrap</a>的話，  
建議你先瀏覽才可以理解兩者差異在哪裡，  

Bootstrap的Sass結構是先設計一組顏色變數，  
如果有五個顏色按鈕，就必須寫五行程式碼來去產生各class樣式。  

像是這樣子：
```
//全域顏色變數
$brand-primary:         #428bca !default;

//新增按鈕顏色變數
$btn-primary-color:              #fff !default; //按鈕文字顏色
$btn-primary-bg:                 $brand-primary !default; //按鈕背景顏色
$btn-primary-border:             darken($btn-primary-bg, 5%) !default; //

//手動新增class
.btn-primary {
  @include button-variant($btn-primary-color, $btn-primary-bg, $btn-primary-border);
}
```

這樣的作法有個缺點是，  
通常網頁元素不只有按鈕而已，  
至少也會有表單、表格、背景顏色等等，  
如果我又要多加一組顏色樣式，  
那豈不是又要到各個模組手動增加class設定？  

所以最近有開發者討論出另外一種設計模式，  
是使用each+Sass Maps來設計程式碼：
```
//scss程式碼
$types: (
  primary   :  #428bca,
  success   :  #5cb85c,
  info :  #5bc0de,
  warning    :  #f0ad4e,
  danger    :  #d9534f
) !default;
//按鈕
@each $name, $color in $types {
  .btn-#{$name} {
    background:$color;
    color:#fff;
    border: 1px solid darken($color,5%);
  }
}


//編譯出來的CSS
.btn-primary {
  background: #428bca;
  color: #fff;
  border: 1px solid #357ebd;
}
.btn-success {
  background: #5cb85c;
  color: #fff;
  border: 1px solid #4cae4c;
}

.btn-info {
  background: #5bc0de;
  color: #fff;
  border: 1px solid #46b8da;
}

.btn-warning {
  background: #f0ad4e;
  color: #fff;
  border: 1px solid #eea236;
}

.btn-danger {
  background: #d9534f;
  color: #fff;
  border: 1px solid #d43f3a;
}
```
我們一一來解析這樣的程式碼：
### Sass Maps  
Sass Maps是Sass 3.3所提供另一種變數的設定方式，  
有點像是json富有key與value的概念，  
所以一開始就把你這網站有哪些樣式整理好後，  
key就寫此顏色的名稱，  
valuse就寫他的色碼：
```
$types: (
  primary   :  #428bca,
  success   :  #5cb85c,
  info :  #5bc0de,
  warning    :  #f0ad4e,
  danger    :  #d9534f
)
```
### @each 
`@each $name , $color in $types`各別的意思是，  
`$types`就是去讀取你的Sass Map裡面的變數，  
看裡面有幾組，他的迴圈就會跑幾次。 
$name、$color這兩個變數你可以自己命名，  
只要知道第一個變數$name會去找冒號前面的內容，  
第二個變數$color會找冒號後面的值即可。

### ${} 插補  
變數沒辦法直接接字串，  
如果你希望變數可以連結字串的話，  
變數就必須使用插補包起來，  
所以我each裡面迴圈的程式碼，  
就可以透過插補動態產生class名稱，  
所以`.btn-#{$name}`跑第一次迴圈時，  
自然會先找到primary，組合起來就變成`.btn-primary`，  
後面就依序組合各別的Class名稱。 

## 那麼該如何去新增其他的網頁元件？  
日後如果你有其他的網頁元件，  
像是表格或表單的話，  
就再新增個@each來跑即可，  
例如下述程式碼則是透過Sass Maps變數同步批次新增表格與按鈕Class：
```

$types: (
  primary   :  #428bca,
  success   :  #5cb85c,
  info :  #5bc0de,
  warning    :  #f0ad4e,
  danger    :  #d9534f
) !default;
//按鈕
@each $name, $color in $types {
  .btn-#{$name} {
    background:$color;
    color:#fff;
    border: 1px solid darken($color,5%);
  }
}
//表格
@each $name, $color in $types {
  .table-#{$name} {
    th{
      background:$color;
      color:#fff;
      border: 1px solid darken($color,5%);
    }
    td{
      border: 1px solid darken($color,5%);
    }
  }
}

``` 

假使你的Sass架構設計成這樣的話，  
往後你要新增一組新的顏色樣式，又可同步在所有網頁組件上時，  
就只要新增一個Sass Map變數即可，  
後面的@each會幫你搞定，相對來說就省事多哩。  

這個設計模式個人認為比較適合用在一個網站上有多個主題時來使用，
各位可以再瀏覽此<a href="http://sassmeister.com/gist/603cc93c8b7307bdfee2" target="_blank">範例程式碼</a>，試著修改Sass Maps來體驗一下他的設計方式。  