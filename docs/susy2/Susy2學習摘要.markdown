# Susy2學習摘要 
在你即將開始進入Susy2的世界前，  
可先瀏覽<a href="https://github.com/gonsakon/Learn-Sass-in-90-days/blob/master/docs/susy2/17.%E4%BD%BF%E7%94%A8Susy2%E5%89%8D%EF%BC%8C%E4%BD%A0%E5%BF%85%E9%A0%88%E8%A6%81%E6%87%82%E7%9A%84CSS%E8%A7%80%E5%BF%B5.markdown" target="_bloank">17.使用Susy2前，你必須要懂的CSS觀念</a> ，  
如果這些觀念還不是很清楚，  
建議先把這些基礎打好後再投入學習，  
學習曲線才不會這麼高。  

## Grid settings
當你學得越來越深入後，  
你會發現Susy2的核心會一直在Grid settings上打轉，  
尤其是`Gutter-position`的部份，  
像是`after`、`before`、`inside`、`split`都是相當常見的Grid設計方式，  
我會建議你至少要懂`after`、`inside`、`split`的排版邏輯，  
這樣之後學習上會比較得心應手些。  

Compass Vertical Rhythm是實踐文字排版上一個優良方案，  
如果你看了第三章還是不了解垂直韻律，  
可以瀏覽此<a href="http://www.slideshare.net/sfismy/vertical-rhythm" target="_blank">簡報</a>，  
再搭配第三章提供的<a href="https://www.youtube.com/watch?v=O3g9DK6DQS0&feature=youtu.be" target="_blank">影片教學</a>就會易懂些了，  
Susy2 Grid systme搭配Compass Vertical Rhythm的組合，  
讓你的網頁排版能夠遵循著規則在設計頁面，相當推薦！  

##版型設定  
當你慢慢對Grid settings熟悉後，  
就可以開始用他來排一些Grid出來，  
像是我的教學章節中，有拿<a href="https://github.com/gonsakon/Learn-Sass-in-90-days/blob/master/docs/susy2/4.markdown">960Grid</a>來編譯出相同的
Grid出來，   
如果你在以前就有使用過一些Grid system，  
那就試著透過Susy2把他實踐出來，  
這樣有助於你對Grid Settings有更加的了解。  

Susy2在透過`Grid settings`設定上相當靈活，
你在實作中會慢慢發現，  
有好幾種設定方式都可以達成你要的效果，  
所以在投入的過程中，就可以開始找出你習慣的設定方式，  

建立出你要的Grid以後，  
排版的細節可以瀏覽<a href="https://github.com/gonsakon/Learn-Sass-in-90-days/blob/master/docs/susy2/11.shorthand(%E7%B0%A1%E5%AF%AB).markdown" target="_blank">shorthand(簡寫)
</a>與12~14章介紹各個提供排版的功能，  
在設計的過程中，忘了語法也可以瀏覽<a href="https://github.com/gonsakon/Learn-Sass-in-90-days/blob/master/docs/susy2/15.Susy2%20%E8%AA%9E%E6%B3%95%E9%80%9F%E8%A8%98%E8%A1%A8.markdown" target="_blank">速記表</a>來查詢。

另外如果你希望一個版型同時擁有兩個以上的Grid樣式的話，  
可以使用<a href="https://github.com/gonsakon/Learn-Sass-in-90-days/blob/master/docs/susy2/9.%E4%BD%BF%E7%94%A8with%20layout%E8%AE%93%E7%89%88%E5%9E%8B%E5%90%8C%E6%99%82%E5%AD%98%E5%9C%A8%E5%85%A9%E7%A8%AE%E4%BB%A5%E4%B8%8A%E7%9A%84Grid.markdown">with-layout</a>的Mixin，Sass Bites也有在<a href="https://www.youtube.com/watch?v=rBKfH8UTn7w" target="_blank">youtube</a>分享過此功能的實作方式。


## RWD排版流程
Susy2的RWD排版方式有載入 <a href="http://breakpoint-sass.com/" target="_blank">breakpoint</a>這個Sass framework，  
所以建議先把`breakpoint`搞懂後，  
再來使用Susy2的`susy-breakpoint`會比較容易進入狀況。  
在6~10章的篇幅，也詳細介紹了Susy2在RWD上的靈活性，  
你可以視你的專案狀況，來客製化你想要的RWD Grid，  

而並非像是Bootstrap與Pure，  
都只能固定幾個columns，gutter也都不能變動，  
在Susy2的世界，你能夠在每個斷點上設定你想要改為幾個columns，  
要不要有gutter、是否要變動為不對稱(Asymmetrical)的版型，  
再透過`with-layout`的Mixin，  
你甚至能設定一個網頁上有多種的Grid，各遇到RWD斷點時透過Grid settings來設定呈現方式，  
這就是Susy2最大魅力所在，Enjoy it！
 



