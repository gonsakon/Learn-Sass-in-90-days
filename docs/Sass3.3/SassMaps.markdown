#SASS MAPS

##範例程式碼

*  <a href="http://www.sitepoint.com/using-sass-maps/" target="_blank">Using Sass Maps</a>
*  <a href="http://www.w3cplus.com/preprocessor/sass-maps.html" target="_blank">w3cplus - Sass Maps</a>
*  <a href="http://css-tricks.com/handling-z-index/" target="_blank">Handling z-index</a>
*  <a href="http://ericsuzanne.com/pres/map-magic/" target="_blank">SASS MAP MAGIC</a>

這個章節主要是來介紹如何將變數利用Sass 3.3的Sass Maps的方式來做延伸運用，  

我個人是覺得這功能主要是拿來提升`程式碼可讀性`、`變數群組化`用的，  
它提供變數具有像是json的資料組合，裡面也是key/value的結構：  

	$map: (
		key:value,
		key2:value2,
		key3:value3
	);  
  
在寫Sass Maps的時候，要特別注意幾點：  
1. 最後一個key/value後面的逗號可以省略  
2. key的名稱不能重複，否則會編譯錯誤  
3. key/value的名稱可以是許多資料類型(數字、字串、布林等等)      

接著來看Sass Maps是如何提取裡面的key/value，  
在以前我們只能這樣載入變數：  
```
$default-color: #fff !default;
$primary-color: #22ae39 !default;
.box{
	color: $default-color;
	background: $primary-color
}
```
但如果是Sass Maps的話是這樣：  
```
$color: (
    default: #fff,
    primary: #22ae39
);
.box{
	color: map-get($color,default);
	background: map-get($color,primary)
}
```  
Sass 3.3開放的時候有人寫了上面這樣的範例，  
那時我看了就覺得反而比以前寫得還要冗長許多，  
後來仔細看才發現Sass Maps除了`map-get`外，  
還有許多功能可以使用，例如：  
* map-get($map,$key)：取出$map裡指定的$key，將value取出來。
* map-merge($map1,$map2)：將兩個$map合併起來。
* map-remove($map,$key)：從Map裡面刪除一個$key。
* map-keys($map)：取出所有的$key。
* map-values($map)：取出所有的value。
* map-has-key($map,$key)：瀏覽裡面是否有$key值，有則回傳true，沒有便回傳false。
* keywords($args)：Returns the map of named arguments passed to a function or mixin that takes a variable argument list. The argument names are strings, and they do not contain the leading $.  

這裡就來舉出在哪些情境下，  
比較適合使用Sass Maps：  
## @each批次產生樣式  
以前我們要產生數組不同顏色按鈕時，必須這樣寫：  
```
//全域顏色變數
$brand-defaule: #333 !default;
$brand-primary: #428bca !default;
//手動新增class
.btn-defaule {
  background: $brand-defaule;
}.btn-primary {
  background: $brand-primary;
}
```  
你可以看出每新增一組樣式時，  
都必須手動新增Class名稱，  
但如果是用@each+Sass Maps的話：  
```
//scss程式碼
$types: (
  defaule   :  #333,
  primary   :  #428bca,
) !default;
//按鈕
@each $name, $color in $types {
  .btn-#{$name} {
    background:$color;
    color:#fff;
    border: 1px solid darken($color,5%);
  }
}
```  
透過這樣，往後我們就把Sass Maps移動到`Variable.scss`做統一管理，  
要新增一組按鈕樣式時，只要增加Sass Maps的一組key/value即可，  
如果上面程式碼看不太懂，可再瀏覽<a href="https://github.com/gonsakon/Learn-Sass-in-90-days/blob/master/docs/Sass/%40each%2BSass%20Maps%E6%89%B9%E6%AC%A1%E7%94%A2%E7%94%9F%E5%90%84%E5%85%83%E7%B4%A0%E6%A8%A3%E5%BC%8F.markdown" target="_blank">延伸閱讀</a>。   

## Z-index管理  
網頁元素實際上和photoshop一樣有圖層的概念，  
可以透過語法來賦予他們的圖層覆蓋設定，  
但如果網站設定較複雜時，  
就很難了解網站的圖層設定值，  
這時我們也可以透過Sass Maps來做統一管理。

首先新增一個`_z-index.scss`，  
在裡面寫：  
```
$zindex: (
  modal     : 9000, 
  overlay   : 8000,
  dropdown  : 7000,
  header    : 6000,
  footer    : 5000
);

.header {
  z-index: map-get($zindex, header);
}
``` 
往後只要有用到z-index的元素就直覺曉得該拿這檔案瀏覽， 

在以前設計Sass結構時，都會認為變數在一個SCSS檔應該統一管理，  
但這樣的話你要管理z-index時，  
就必須跑以下流程：  
1. 一個新區塊要設定z-index  
2. 到變數的scss檔看一下設定值    
3. 再開啟要新增區塊的scss新增z-index    

相信這樣比較你就可以看得出來兩者的差異性，  
前者的方式都可在一個`z-index`檔上直接做完，  
相對來說也省事多了。  

## 提升可讀性  
在設計Font icon時，都會寫一個icon指定一個class：  
```
icon-checkmark:before {
  content: "\e258";
}
.icon-instagram:before {
  content: "\e32e";
}
.icon-twitter:before {
  content: "\e32f";
}
.icon-dribbble:before {
  content: "\e341";
}
.icon-github:before {
  content: "\e34c";
}
.icon-soundcloud:before {
  content: "\e35d";
}
```  
你可以看得出來這樣要查詢、修改樣式非常麻煩，但透過Sass Maps+each的設計就可改寫為：  
```
$icons: (
  skull: "\e18c",
  warning: "\e243",
  checkmark: "\e258",
  instagram: "\e32e",
  twitter: "\e32f",
  dribbble: "\e341",
  github: "\e34c",
  soundcloud: "\e35d",
  stackoverflow: "\e367",
);
[data-icon]:before {
  @extend %icon; //icon預設樣式
  content: attr(data-icon);
}

@each $name, $glyph in $icons {
  [data-icon='#{$icon}']:before {
    content: map-get($icons, $name);
  }
}
```  
往後我們要瀏覽這個網站有哪些樣式，  
就只要看Sass Maps來瀏覽，  
便不用像最上面還需要用滾輪滾上滾下花時間來找，  
相對來說可讀性就高許多了。

## 總結 
上面的範例是我自己實際有在使用的例子，  
你也可以開始思考如何透過Sass Maps讓自己的程式碼更加友善地管理，  
看完我的文章，你也可以到最上面的範例程式碼連結瀏覽更佳詳細的資訊。
