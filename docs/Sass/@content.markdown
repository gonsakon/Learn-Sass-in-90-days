# @content

## 進入主題

@content的用途主要是拿來傳遞內容到Mixin裡面去的， 
像是一般的Mixin大家所認知的就是他能夠傳遞變數進去，  
如下程式碼：   
```
@mixin bg($text-color,$bg-color){
  background: $bg-color;
  color: $text-color;
}
.box{
  @include bg(#fff,#000)
}
//編譯出來的CSS
.box{
  background: 000;
  color: #fff;
}
```
但如果你使用了@content的話，  
就能在Mixin裡面繼續寫額外的東西，  
舉例：  
```
@mixin bg($text-color,$bg-color){
  background: $bg-color;
  color: $text-color;
  @content;    //多了一個@content
}
.box{
  @include bg(#fff,#000){
    border: 1px solid lighten(#000, 10);  //將額外的程式碼寫在@include中括號裡面
  }
}
//編譯出來的CSS
.box {
  background: #000;
  color: #fff;
  border: 1px solid #1a1a1a;  //對應@content所放位置編譯於此行
}

```
我們現在已經知道@content能額外將程式碼帶進放置的位置去，
現在來講解@content還有什麼實用的功能。

## 選擇器的繼承與覆蓋

有的時候我們為了去針對特定瀏覽器去做兼容性的語法時，  
都會寫CSS hack上去，  
例如這個例子：  
```
@mixin ie8{
  .ie8 & {
    @content
  }
}
.box{
  width:50px
  @include ie8{
    width:150px
  }
}
//編譯出來的CSS
.box {
  width:50px
}
.ie8 .box {
  width:150px
}
```
有些網頁設計師在設計網頁時，  
都會搭配像是[modernizr](http://modernizr.com/)的js，  
它的功能是如果你今天是使用ie8瀏覽網頁時，  
他會在html的tag上面加上一個class名稱為'ie8'，  
所以今天我們在寫針對ie8的設定時，  
就可以寫 `.ie8 .box`來去覆蓋掉`.box`的設定，  
所以往後我要寫針對.ie8的hack就只要呼叫`ie8`這個Mixin就可以了。  

## 狀態
有的時候我們在設計網頁時，  
時常會需要針對狀態來去做設定，  
像是譬如說今天一個a連結，  
當滑鼠滑過去的時候會觸發a:hover事件，  
當user點選時會出發a:active的事件，  
有的時候當該連結或頁籤被點選後，  
會觸發javascript事件，動態在該連結上加上個`.active`的class，  
像這些林林總總的都可稱為狀態上的改變，  
所以也可以這樣來規劃@mixin與@content，   
```
@mixin link{  //連結樣式
  &:link,&:visited{  
    @content;
  } 
} 
@mixin link-hover{ //被點擊後的樣式
  &:hover, &:focus, &:active,&.active{
    @content;
  } 
} 
.box{ 
  height:50px;  
  @include link{color:#fff};  
  @include link-hover{color:#000};  
}
//編譯出的CSS
.box {
  height: 50px;
}
.box:link, .box:visited {
  color: #fff;
}
.box:hover, .box:focus, .box:active {
  color: #000;
} 
```
透過這樣的方式，  
我們就不用每次都還必須手寫`hover`、`active`、`focus`的樣式了， 
只要透過Mixin他就會自動幫我們處理狀態的部份。  


## @content也可以寫二個以上
像譬如我們時常需要寫瀏覽器前綴詞來進行兼容時，
也可以像這樣寫：
```
@mixin keyframes($animation) {
    @-webkit-keyframes $animation{
        @content;
    }
    @-moz-keyframes $animation{
        @content;
    }
    @-ms-keyframes $animation{
        @content;
    }
    @-o-keyframes $animation{
        @content;
    }
    @keyframes $animation{
        @content;
    }
}
```
這樣子編譯出來就會針對各瀏覽器去寫CSS3動畫效果。  



## RWD斷點設計
當然如果你沒有在用任何RWD Grid Framework，  
你也可以自己寫一個：  
```
//透過斷點變數統一管理
$pc:1024px;
$mobile:767px;
@mixin rwd($width) {
  @media only screen and (max-width: $width) {
    @content;
  }
}
.box{
  float:left;
  width: 30%;
  @include rwd($mobile) {
    float: none;
    width: 100%;
  }
}
//編譯出來的CSS
.box {
  float: left;
  width: 30%;
}
@media only screen and (max-width: 767px) {
  .box {
    float: none;
    width: 100%;
  }
}

```
這樣一來，你就可以透過變數來統一管理你的media query。
