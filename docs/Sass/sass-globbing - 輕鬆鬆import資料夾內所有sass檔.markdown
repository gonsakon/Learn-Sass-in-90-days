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
以我自己在規劃Sass結構時，  
會採用<a href="https://github.com/gonsakon/Learn-Sass-in-90-days/blob/master/docs/SMACSS/2.Module%20Rules.markdown" target="_blank">Smacss - Module</a>的觀念，  
我會針對該專案上會套用到的表格、表單、按鈕設計專屬的module css，  
所以我在Sass目錄上會再多一個資料夾叫`module`，  
裡面可能就會放：  
* _button.sass
* _table.sass
* _form.sass
 

