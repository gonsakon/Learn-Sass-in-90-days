# Source Maps

Sass 3.3新增的Source Maps主要功能就是讓瀏覽器能夠支援下圖效果：
![](/images/sass/20141010-1.png)  
透過上圖，就能知道該CSS程式碼是在哪一隻Sass檔的第幾行，  
他的原理是當Sass編譯出CSS檔案後，  
會再編譯出一個對應的.map檔，  
如果你有開啟Source Map的設定，  
你會發現編譯出來的CSS檔案最下面會有一行程式碼：
```
/*# sourceMappingURL=all.css.map */
```
網頁瀏覽器讀取到這行，就會找到對應map檔，  
利用map裡面的資訊逆推去找對應的Sass程式碼，  
所以.map也可以是說做為中間的溝通媒介，  
接下來就來繼續講該如何開啟Sourcemap的設定：

##步驟一 Chrome開啟Source maps的設定
這裡的範例是使用chrome，  
首先開啟chrome dev tools後，  
再找到齒輪icon，  
進入`Settings > General > Sources > Enable CSS source maps`，  
這樣就能讓瀏覽器支援Source Maps的功能，如下圖，  
![](/images/sass/20141010-2.png)  
## 步驟二 在config.rb新增source maps設定，  
寫過Sass的開發者都知道，  
根目錄會產生出一個config.rb的設定，  
在裡面增加一行code，如下：
```
sourcemap = true
```
新增後，再重新watch開啟專案，  
在html裡面寫個元素，再到Sass裡面寫對應html，  
打開瀏覽器就能看到效果嘍！

除了能看到效果外，  
chrome瀏覽器還能追蹤變數與@Mixin，  
假設下圖我要尋找背景的變數顏色的話，  
你就按住Command鍵，滑鼠滑到對應位置會顯示下底線，如下圖，  
![](/images/sass/20141010-3.png)  
點進去後你就會發現他就跑到對應的變數去了，  
是不是相當方便呢？
![](/images/sass/20141010-4.png)  
## 總結
如果你希望能在瀏覽器修改，就能同時修改本地端的檔案，  
影片教學內有附上流程，再搭配此<a href="http://www.slideshare.net/sfismy/sass-38039962" target="_blank">簡報</a>，  
這樣你就能透過瀏覽器來即時更新Sass資料嘍^_^

##youtube影片教學  
<a href="https://www.youtube.com/watch?v=7oxs6y2MInk&list=UU7A-C1EwjVfGbCOK5u8AlwA" target="_blank">![](/images/sass/20141010-5.png)</a>  
