# OOCSS  

##程式碼連結
<a href="http://oocss.org/" target="_blank">OOCSS</a>  
<a href="http://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/" target="_blank">An Introduction To Object Oriented CSS (OOCSS)
</a>  

OOCSS的設計模式是鼓勵開發者設計出的CSS複用性能夠達到極致，  
最終目的是希望你可以藉由一套CSS來設計日後幾百幾千頁的頁面，  
而不用再去額外新增Class。  

在那之前我來分享一個2008年的專案，  
該專案因為有1~2000頁的HTML需要設計，  
但我底下的人只有兩三個工讀生，更慘的是他們連CSS也不會， 
所以我就設計出了這樣的CSS結構：  
```  
.font-big{font-size:18px}
.font-small{font-size:13px}
.blue{color:blue}
.red{color:red}
.mt10{margin-top: 10px}
.mt20{margin-top: 20px}
.mb10{margin-bottom: 10px}
.mb20{margin-bottom: 20px}
.ml10{margin-left: 10px}
.ml20{margin-left: 20px}
.mr10{margin-right: 10px}
.mr20{margin-right: 20px}
```
設計好以後，  
我就教工讀生一些簡單的HTML tag寫法，  
例如`h1`、`p`，、`ul`、`li`等等的tag，  
再寫一份文件列出所有的樣式class出來，  
所以如果工讀生要設計一個藍色文字標題，margin-bottom:10px的話就可以這樣寫：  
```
<h1 class="font-big blue mb10">文字標題</h1>
```  
一個class就只單純做一個工作，  
利用HTML tag可以一次載入多個Class的特性，  
來去組合出我們要的樣式出來，  
所以我在之後OOCSS設計模式出來後才發現，  
原來這就是OOCSS的特性。  

通常網頁內容中，  
我會觀察有哪些CSS是重複性質比較高的，  
也會把他抽離出來拿來套用在版型上，  
但就不會像上面設計得那麼極端，  
這裡我就拿Bootstrap設計按鈕的例子來分享：  
<img src="../../images/sass/20141018-1.png" height="385" width="816" alt="">
在上圖的按鈕每個class的用處是：  
1.`btn`：解決瀏覽器兼容的CSS Hack、撰寫預設按鈕樣式
2.`btn-promary`：增加`文字顏色`、`背景顏色`、`線條現色`覆蓋預設樣式  
3.`btn-lg`：增加`文字大小`、`padding留白`，覆蓋預設樣式  
像是Bootstrap 就有導入一些OOCSS的觀念，  
每一個Class都有他的任務存在。  

所以你在設計網頁時，  
也可以考慮樣一些常用的設定給獨立出來，  
這樣就可以節省不少重複寫code的負擔，  
讓CSS能夠容量變得更小。  

我個人建議第一次網頁在導入OOCSS的觀念時，  
如果你不是純OOCSS，建議你的class不要拆成五種以上會比較好，  
以避免寫到後面，你看不懂自己在寫些什麼。  

像Facebook就是設計成很純粹的OOCSS，  
我們來看一下他設計的Code：  
<img src="../../images/sass/20141018-2.png" alt="">
你可以從上圖看得出來，  
`_5pb8 _5v9u _29h _303`這幾個class各有它的功能，  
藉由這樣的方式，  
今天如果要新增一個頁面時，  
他就可以藉由目前現有的CSS來設計新頁面，  
就不用再去新增CSS樣式了。  

所以你就可以思考有哪些元件你希望用OOCSS來處理，  
例如間距、留白、Grid寬度、theme等等，  
像是960grid就會把所有的grid設定成class，  
方便網頁設計師只要在html設定class就能把layout設計出來。  
```
.container_12 .grid_1 {width: 60px;}
.container_12 .grid_2 {width: 140px;}
.container_12 .grid_4 {width: 300px;}
.container_12 .grid_5 {width: 380px;}
.container_12 .grid_7 {width: 540px;}
.container_12 .grid_8 {width: 620px;}
.continer_12 .grid_10 {width: 780px;}
.container_12 .grid_11 {width: 860px;}
```
如果你是Sass開發者，  
也可以使用@extend+佔位選擇符(%)，  
將Class都合併起來。  
```
%font-l {font-size: 150%;}
%title-color {color: #313131;}
%mb10 {margin-bottom:10px !important}
.billing-info {
  label {
    @extend %font-l;
    @extend %title-color;
    @extend %mb1-;
  }
}
```

## 補充  
* 使用OOCSS時，盡量不要用後代選擇器(.header ul)
* OOCSS應該是直接命名class，才能夠隨意指定到各html tag上。


## 總結  
1. 適當的使用有助於減少你網頁上重複性的程式碼
2. 團隊導入OOCSS時，建議要寫樣式文件，好讓彼此了解每個class的用處。  
3. 網站規模小時，不建議套用OOCSS設計模式：為了讓一組CSS能夠套用在各個頁面上，勢必需要設定很多獨立功能的CSS，所以光你在設計OOCSS理念的程式碼的時間，你可能就已經寫好了。


