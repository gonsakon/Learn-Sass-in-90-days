# MVCSS - Styleguide

##程式碼連結
* <a href="http://mvcss.github.io/" target="_blank">MVCSS</a>
* <a href="http://mvcss.ycnets.com/" target="_blank">MVCSS中文翻譯</a>  

##進入主題  
MVCSS融合了SMACSS、OOCSS、BEM的設計模式，  
同時有參考了Foundation、Bootstrap、SUIT、inuit.css的framework，  
所以在你要瀏覽MVCSS的設計模式時，  
建議先回頭將SMACSS、OOCSS、BEM的觀念先弄清楚，  
再來讀MVCSS比較不會有障礙，因為文件內容時常會提到它有些結構有參考某個設計模式，  

這個章節主要是來講styleguide的部份，  
你可以搭配上面連結的文件來做延伸閱讀，  
而我這裡則會針對他每個細節來做更進一步的解說。

##樣式表（Style Sheets）
MVCSS的程式碼範例都是使用`Sass`，  
所以如果你是SCSS開發者的話，有些細節可能要注意一下。  
例如要命名一個Mixin，在Scss上是`@mixin bg(){}`，  
Sass只要這樣寫`=bg(){}`即可。  


## Style Sheets  
MVCSS有一套基本的撰寫SASS的風格參考：  
### CSS依照字母來排序
如果有依照這樣來排列CSS設定，  
較容易找得到自己想要找得程式碼，  
除了MVCSS外，其他很多設計模式也建議這樣子做，  
這個部分見仁見智，我自己沒有遵守：
```
//沒有依照字母排列
.box{
	zoom: 1;
	position: relative;
	font-size: 13px;
	color: #000;
	line-height: 1.5;
	background: url(../img.png);
	letter-spacing: 1pt;
}
//有依照字母排列
.box{
	background: url(../img.png);
	color: #000;
	font-size: 13px;
	letter-spacing: 1pt;
	line-height: 1.5;
	position: relative;
	zoom: 1;
}
```
###Extends和Mixins建議放在CSS設定前面
除了Extends和Mixins外，  
有用到Sass功能的建議都放在最前面，  
可讀性會比較高
```
//mixin和extend混在CSS設定裡面，較不好閱讀
.box{
	zoom: 1;
	@include bg();
	position: relative;
	font-size: 13px;
	color: #000;
	@include hide-text();
	line-height: 1.5;
	background: url(../img.png);
	letter-spacing: 1pt;
	@extend g-1of3;
}
//Extends和Mixins放在CSS設定前面
.box{
	@include bg();
	@include hide-text();
	@extend g-1of3;
	background: url(../img.png);
	color: #000;
	font-size: 13px;
	letter-spacing: 1pt;
	line-height: 1.5;
	position: relative;
	zoom: 1;
}
```
###使用兩個空格縮排 
使用Tab在一些編輯器和編譯軟體上容易遇到問題，  
用空白問題較少，  
這裡也補充一些使用Sass格式需要注意的問題。  
1. 一個Sass檔案裡面不能同時存在T	ab與空白縮排，會導致編譯錯誤
2. 在import Sass檔案時，允許一個檔案是Tab，另外一個檔案是空白縮排


### 在 : 之後添加一個空格
```
//有些有空白有些沒有，導致文件瀏覽不易
.box{
	color:#fff;
	background: #000;
	line-hieght:1.5;
	text-align: center
}
//一致性都有留白
.box{
	color: #fff;
	background: #000;
	line-hieght: 1.5;
	text-align: center
}
```
### 在註解 // 之後添加一個空格  
### 在值中的逗號之後添加一個空格（如 rgba(#000, 0.5)）
這兩點也是同上，為得是建立好規則，  
以便團隊在設計程式碼上比較一致乾淨。  

### 堅持使用`class`來設計樣式，不用`ID`  
這部份和SMACSS的<a href="https://github.com/gonsakon/Learn-Sass-in-90-days/blob/master/docs/SMACSS/2.Module%20Rules.markdown#%E9%80%B2%E5%85%A5%E4%B8%BB%E9%A1%8C" target="_blank">Module Rules</a>理念相同，  
如果是被設計成模組的區塊，  
由於ID只能一個在網頁上，不能多處都放相同ID，  
假使有個模組要顯示多個在網頁上時，那就必須重新設計了，  
所以才會建議使用class來撰寫CSS樣式，  
但並不代表全部都不能使用ID，  
如果你確定該元素或區塊在各頁面上確實只會顯示一處時，  
那就可以使用ID，例如`Laout`區塊。


### 盡可能限制巢狀結構
(待補充)  

## 標記（Markup） 
1. 需依照Component、Structure、Tool、state、、context來排列class。
2. 每個模式如果有修飾符（modifier classes），就必須連接在模組class後面。
這裡如果看不懂沒關係，等到後面一一介紹Component、Structure等功能再回頭看相信便能一目了然。
```
<div class="g collection collection--1of3 bch mtl tci is-active has-dropdown"></div>
```
## 數值規範數字遊戲(Styleguide - The Numbers Game)  
1. 預設的文字單位是使用`px`，並設定在`config`的HTML tag上
2. 行距是沒有單位的，例如`1.8`  
3. padding、margin是已預設文大小的倍數，使用`em`來設定
4. 字體大小除了`html`的tag外，其他都是使用`%`的單位來設定  

這裡補充一下，  
我自己是沒有follow這樣的設定，  
所有的文字設定與大小與行距都還是用px，
原因是我有用Compass的<a href="https://github.com/gonsakon/Learn-Sass-in-90-days/blob/master/docs/susy2/3.Grid%20settings(%E4%B8%8B)%20debug%20Compass%20Vertical%20Rhythm.markdown" target="_blank">Compass Vertical Rhythm</a> ，  
這裡還是要強調一點，  
設計模式並非要全然參考，  
有些時候是你技術未到位，觀念無法掌握，  
有得時候是你已經有自己的方法處理此細節，  
所以取其優點讓自己的撰寫習慣變得更加漂亮即可。  

## 註解寫法  

依照模組的權重來寫註解：  
```
// *************************************  
//
//   第一階  
//   -> 描述  
//
// *************************************    

// -------------------------------------  
//   第二階  
// -------------------------------------  

// ----- 第三階 ----- //  

// 第四階  
```  
## 命名習慣  
請參考此譯者的<a href="http://mvcss.ycnets.com/styleguide/naming/" target="_blank">翻譯連結</a>。