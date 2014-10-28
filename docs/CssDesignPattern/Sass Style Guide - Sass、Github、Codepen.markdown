# Sass Style Guide - Sass、Github、Codepen

## 相關連結
* <a href="http://sass-lang.com/styleguide" target="_blank">Sass styleguide</a>
* <a href="https://github.com/styleguide/css" target="_blank">github Styleguide</a>
* <a href="" target="_blank">CodePen's CSS</a>

##進入主題  
當你所在的組織是一個團隊的時候，  
為了讓大家的程式碼都能保持一致得風格來設計，  
所以都會一同討論並建立Style Guide出來， 
觀察別人的Style Guide也有助於提升自己對程式碼的風格建立，  
這一次我則是挑了三個的不錯的Style Guide供大家參考：  


## Sass 官網  
你現在看到的<a href="http://sass-lang.com/" target="_blank">Sass官網</a>其實已經是改版過的了，    
這次Sass官網也釋出了他們的stylecode，  

#### Typography 
使用@mixin與變數統一管理字體大小行距、粗體、字型：  

```
//字型
@include font-size-small	//編譯出12px與對應的行高
@include font-size-regular	//編譯出16px與對應的行高
@include font-size-large	//以此類推
@include font-size-x-large	
@include font-size-xx-large	
@include font-size-xxx-large	
@include font-size-xxxx-large	
//Weights 粗體
$font-weight-light:300;
$font-weight-regular:400;
$font-weight-bold:600;
//Families 字型
$font-family-text:source-sans-pro, 'Helvetica Neue', Helvetica, Arial, sans-serif;
$font-family-display:source-serif-pro, Georgia, 'Times New Roman', Times, serif;
$font-family-code: source-code-pro, Consolas, 'Andale Mono WT', 'Andale Mono', 'Lucida Console', 'Lucida Sans Typewriter', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Liberation Mono', 'Nimbus Mono L', Monaco, 'Courier New', Courier, monospace;
```
為了保持文字排版能夠遵守垂直韻律，所以每個＠Mixin除了編譯出字型大小外，  
也會編譯出對應的行距出來，  
另外在粗體與字體也會集中變數來管理，  
這點Bootstrap Sass也有做到這一點。  

#### 撰寫習慣  
1. HTML預處理器是`haml`、`erb`、`md`來混用
2. HTML都是用小寫來標記元素和屬性，Self-close empty elements也會用結尾斜線`<br />`。  
3.使用的Framework有`Compass`、`Susy`、`Breakpoint`  

使用到`Susy`的話基本上都會載入`Breakpoint`，  
因為`Susy`的RWD @mixin會使用到`Breakpoint`的功能。  

#### Code Style Guide 撰寫風格  
1. 用連接符連接區塊底下的元素：（snake_case）  
2. 在class命名上使用一般到具體的作法，可瀏覽此篇<a href="http://webdesign.tutsplus.com/tutorials/quick-tip-name-your-sass-variables-modularly--webdesign-13364" target="_blank">文章</a>。  
3. 避免嵌套太深 (.nav ul li a span)  
4. Write comma-delimited selectors on separate lines.    

#### RWD 斷點
```
$mobile-small: 240;
$mobile-large: 320;
$tablet-small: 480;
$tablet-large: 768;
$screen-small: 1024;
$screen-large: 1280;
```
讓我訝異的事情是Sass竟然有支援`240px`，  
現在很少手機在這解析度上了，  
768與1024px是iPad的直、橫式解析度，  
1280是很熱門的桌上PC螢幕解析度。  



## Github  
Github的CSS也是使用SCSS來設計的，  
另外樣式表文件則是使用`KSS`來撰寫，  
`KSS`是只要在SCSS檔案上寫符合KSS規範的註解，  
就能額外編譯出樣式表格式的HTML檔案出來提供網頁設計師參考。   

### 擷取部分撰寫風格：
1. 統一用兩個空白來作推進  
1. 冒號後面加一個空格 ( color: #fff  )  
2. 中括號前面加一個空格 ( .header {} )  
3. 用//來取代/**/ 註解  
4. 不要將@import架構擴展到三層以上  
5. 公用的變數與@mixin放在`global`資料夾。  
6. 使用顏色變數時用hex color`#000`，除非是使用rgba()  

再來Github的SCSS結構長得像是如下：  
```
styles
├── components
│   ├── comments.scss
│   └── listings.scss
├── globals
│   ├── browser_helpers.scss
│   ├── responsive_helpers.scss
│   └── variables.scss
├── plugins
│   ├── jquery.fancybox-1.3.4.css
│   └── reset.scss
├── sections
│   ├── issues.scss
│   └── profile.scss
└── shared
    ├── forms.scss
    └── markdown.scss
```
`components`是網頁上的組件，`globals`是全域設定，  
所以可看到裡面會有variables，`plugin`有點像是`Smacss`的vendor，  
意思是則第三方的插件所帶來的CSS設定，例如jquery動畫、css framework，  
`sections`是針對每個頁面產生各別客製化的SCSS檔。  

值得一提的是Github有設計兩種版本CSS，  
各別是給IE9以上跟以下的使用者看的。 

#### Class naming conventions  
CSS樣式都寫在前綴`is-`上，不會寫到`js-`上面，例：`<img class="js-img" />`，  
這樣才不會導致你在修改CSS與HTML 結構時，不小心動到js的設定。  

#### Specificity (classes vs. ids)
Github有使用ID來設定樣式，  
這裡它有強調`ID`要確定在頁面上只會顯示一個區塊才可以使用，  
像是header表頭或footer表尾，否則都是用class。


## Codepen  
Codepen是一個線上網路寫程式碼的服務，  
在最近也支援了Susy這個Framework，  
我們也來看看它們的CSS寫法，  
有些內容我看不懂意思就直接提供英文內容了。：  

1. 使用SCSS  
2. 使用Autoprefixer(是一個瀏覽器前綴兼容plugin，在sublime上也有)  
3. 使用 Rails Asset Pipeline(JS與CSS壓縮工具)  
4. The SCSS file that represents the CSS file that actually gets loaded is just a table of contents.  
5. codepen有一個風格樣式，但大多數只是因為一致性看起來不錯  
6. 不用任何特別的結構，除了use classes a bunch ”以外  
7. 在每個頁面上只會使用2~3個CSS檔案  
8. 是使用`@mixin`來寫RWD效果，以方便隨時關閉。  
9. 有在程式碼裡面使用註解  
10. 一些統計數據    
11. CSS部分只有作者一人來設計，總共三人合作開發  
12. What the future might be like for us.  

在codepen上，作者有使用這些 Sass功能：  
1. @import  
2. @mixin  
3. nesting  
4. variables  
5. @extend  
6. math  
7. loops  

作者提到說以前他也是有在用Compass，  
但後來發現它也只有在用CSS3 Mixin的功能，  
所以後來就改用使用Autoprefixer，  
因為他不希望一堆@include都是為了前綴。  

Codepen的SCSS結構：  
```
// General Dependencies
@import "global/colors";
@import "global/bits";

// Base
@import "global/reset";
@import "global/layout";

// Areas
@import "global/header";
@import "global/footer";

// Patterns
@import "global/typography";
@import "global/forms";
@import "global/toolbox";
@import "global/buttons";
@import "global/modals";
@import "global/messages";
@import "global/badges";

// Third-Party Components
// (none at the moment)
```
比較特別的地方是作者把Layout的區塊放在`area`，  
將表頭與表尾的設計獨立成一個scss檔案，  
針對文字排版(typography)、表單、`modals`、按鈕有個別作設定。  
另外作者提到有時候會因為一些意外狀況，    
所以設計了一個`shame`的scss檔案，將程式碼暫時放在這裡：    
```
@import "shame";
```  
這個想法其實在MVCSS的inbox還挺像的，  
inbox的觀念是如果有還不是很了解團隊Sass結構的人，  
可以先將css寫在inbox的CSS區塊裡面，  
之後再整理到規範文件裡面。   

另外較有趣的數據是，codepen總共有160個獨立SCSS文件，  
但作者從來不怕找不到檔案，因為sublime有很強大的搜尋功能。  
最後提供codepen scss檔案的容量大小：  
1. SCSS文件共13345行
2. global.css文件11.8k
3. page.css文件5.5k
4. editor.css文件6.2k

除此之外codepen下方還有針對`撰寫風格`、`Media Queries`做詳細的解說，有興趣的朋友可以再到最上面的連結瀏覽。  
