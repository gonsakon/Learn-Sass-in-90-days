# span[mixin]
##程式碼連結

* [sassmeister-susy2 span mixin about of](http://sassmeister.com/gist/448934cde32366806a1d)
###Grid Widths
```
.box{
  @include span(25%)
  /*
  如果沒設定Grid，CSS會編譯出：
  float:left
  width:25%
  */
}

.box{
  @include span(1) //依照Grid設定，產生一欄寬度
}

```
###last
當 `gutter-position`是`right`、或`after` 時， 
如果你今天要設計一個左1右12滿版的版型，
這部份[官網](http://susy.readthedocs.org/en/latest/toolkit/#row-edges)也有提到。
```
.left{@include span(1)}
.right{@include span(11 last)}
```
susy2的`last`與`omega`的功能是一樣的，  
但在susy2也有保留些susy1的語意，  
所以你也可以把last改為omega，  
功能也會正常work。

### context `of`
```
.box{
  @include span(10 of 12) 
}
```
`of`是依照你的父元素設定的欄寬來跑。  

這裡舉個例子，  
如果你要設計成這樣子的話，  
你的`.agi`寬度不能直接寫`span(3)`， 
因為你要設定的寬度是`.content`的3欄，  
而不是`.container`的3欄，  
所以你的`at1`必須寫成：
```
.at1{@include span(3 of 9)}

//或包在.content裡面
.content{
  @include span(9){
    .at1{
      @include span(3);
    }
  };
}
```
上面和下面的程式碼，  
結果是一樣的，  
可以到此[範例程式碼](http://sassmeister.com/gist/448934cde32366806a1d)來瀏覽， 
你可以看到範例程式碼我為了讓他可以依序排列下來，  
用了`nth-child(3n)`的CSS設定，  
這意思則是說每到第三個div就會用[last mixin](http://susy.readthedocs.org/en/latest/toolkit/#last)清除掉gutter。  


