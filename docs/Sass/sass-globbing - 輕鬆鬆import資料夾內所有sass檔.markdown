# sass-globbing - 輕鬆import資料夾內所有sass檔  

<a href="https://github.com/chriseppstein/sass-globbing">Sass Globbing Plugin連結</a>  
在這個plugin還沒有出現之前，  
Sass是不支援@import整個資料夾所有的Sass檔案，  
仍必須手動一個一個寫合併語法。  
而sass-globbing也因此誕生出來，  
如標題所言，他能夠指定資料夾，讓裡面的Sass檔都import進來，  

如果你希望import整個資料夾的話，就在要合併的Sass檔案裡面寫：  
```
@import "library/mixins/*"
``` 
如果你的Sass結構長成下面這樣：  
```
|- library
   _color.scss
   |- Mixin
      _retina.scss
   |- Module
   	  _button.scss
   	  _table.scss
   	  _form.scss 
```  
然後希望`library`底下所有的scss檔都@import進來的話，  
就可以寫成這樣：  
```
@import "library/**/*"
```  

相信看到這邊你就看得出來他的好處了，  

以我自己的習慣，  
我自己常用的@Mixin有拆分成1~20個檔，  
有新專案進來時，再視專案性質套入合用的@mixin，  
所以我就可以開個Mixin資料夾，將各個Mixin檔案放進去，讓sass-globbing幫我全部@include即可：
```
@import "Mixin/*"
```

再來以我自己在規劃Sass結構時，  
會採用<a href="https://github.com/gonsakon/Learn-Sass-in-90-days/blob/master/docs/SMACSS/2.Module%20Rules.markdown" target="_blank">Smacss - Module</a>的觀念，   
所以我在Sass目錄上會再多一個資料夾叫`module`，  
裡面可能就會放：  
* _button.sass
* _table.sass
* _form.sass
 
這些都是獨立的模組，所以不會有載入順序衝突的問題，
所以整合import的Sass檔就寫：  
```
@import "module/*"
```

所以我的專案結構就會像是這樣子：  
```
@import compass                     
@import Foundation                         
@import grids
@import "mixin/*"
@import "module/*"
@import layout
@import "page/*" 
```  
`Foundation`是參考MVCSS的架構，  
裡頭會放css reset、全域變數、Base、Tools，  
page是如果這頁獨特性太高時，就不會放到Module。  
這一個專案總共有40幾個Sass檔案，  
但因為sass-globbing的導入，  
讓我節省了不少需要思考先後放置的時間，  
真的是非常方便的plugin！

## 安裝流程  
sass-globbing必須透過Ruby來安裝，  
所以開啟你的指令視窗，輸入：  
```
gem install sass-globbing
```  

再來到你的Sass專案裡面的config.rb輸入：  
```
require 'sass-globbing'
```  
之後再重啟你的Sass專案就ok了。  

如果你是用Fire.app的話，  
他內建本身沒有這功能，  
但你可以到這裡把它整個lib抓下來後，  
再整合到Fire.app裡面，  
這裡也附上<a href="http://fireapp.kkbox.com/doc/tw/extension.html" target="_blank">教學連結 </a>。  

## 注意事項  
在使用sass-globbing時，  
要特別注意`@import`的先後順序，  
你可以看到我上面的結構一定是reset、Base、Mixin先載入，  
後面的Module和page才會吃到前面的設定來進行覆蓋樣式、呼叫@Mixin的動作。   
知道這點後，你就可以開始規劃你的Sass結構如何透過sass-globbing設計出更加靈活的架構了。
