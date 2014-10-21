# MVCSS - Manifest、Vendor

##程式碼連結
* <a href="http://mvcss.github.io/" target="_blank">MVCSS</a>
* <a href="http://mvcss.ycnets.com/" target="_blank">MVCSS中文翻譯</a>   

## Manifest  
這個章節主要是聊MVCSS的Sass結構與命名方式，  
首先我們就來看到Sass結構：  
```
application.sass
foundation/
  _reset.sass
  _helpers.sass
  _config.sass
  _base.sass
  _tools.sass
components/
structures/
vendor/
```  
`application.sass`整合所有的import的Sass檔案，  
編譯後`application.css`會被包括在每一頁上，  
同時也可以被壓縮。  
#### Manifest-Import
分布在Foundation中的`reset`、`helpers`、`config`、`base`依序先後導入：  
```
// *************************************
//
//   Project Name
//   -> Manifest
//
// *************************************

// -------------------------------------
//   Foundation
// -------------------------------------

@import "foundation/reset"
@import "foundation/helpers"
@import "foundation/config"
@import "foundation/base"

// -------------------------------------
//   Components
// -------------------------------------

// Component imports

// -------------------------------------
//   Structures
// -------------------------------------

// Structure imports

// -------------------------------------
//   Vendor
// -------------------------------------

// Third-party style imports, if needed

// -------------------------------------
//   Foundation - Tools
// -------------------------------------

@import "foundation/tools"

// -------------------------------------
//   Inbox
// -------------------------------------
```  
在MVCSS裡面有提到一個不錯的觀念，  
也就是在整個Sass結構的最下面有個Inbox，  
這個地方主要是拿來給開發人員暫時寫Sass程式碼用的，  
因為有的時候我們和其他開發人員合作時，  
可能對方不懂你的Sass結構，  
所以就不曉得該如何把code放在對的位置上，  
這時候你就可以請對方暫時寫在Inbox上面，  
到後期再把他整合到你的結構上。  

以我自己在開發也是一樣，  
不過我的例子比較常發生在合作對象不懂Sass，  
所以我會請他自己再添入一個CSS檔案，  
不要直接改我編譯出來個CSS檔案，  
等到最後專案要結束後再把對方的CSS納入到我的Sass結構來。  

## Vendor
Vendor主要的用途是用來整合第三方的plugin與Framwork用的，  
有些Framework可能是`.css`檔案，  
但其實也不用擔心，畢竟`scss`支援純css寫法，  
所以只要把副檔名改成`scss`就可以安心`@import`到vendor裡面。  

有的時候一個大型專案網站動輒就載入了許多jQuery 動畫效果plugin，  
相對載入的CSS檔案也會變多，  
但只要透過Vendor的觀念，  
我們就能把第三方plugin都整合在一隻CSS檔案裡面，
這樣的作法就有助於讓網站請求數降低。  

其實除了CSS外，js理應也要有相同的觀念。  

PS：MVCSS指出，雖然`_reset.sass`也包含第三方的程式碼，  
但他整合到`Foundation` 之中，  
這樣有助於檔案載入權重順序比較不會出現衝突與潛在問題發生。