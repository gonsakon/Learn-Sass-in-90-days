#使用animate.scss增強網頁瀏覽體驗

<a href="https://www.youtube.com/watch?v=mgvKAwC6NpQ&feature=youtu.be" target="_blank">![](/images/sass/20141012-1.png)</a> 

##範例程式碼
* <a href="http://daneden.github.io/animate.css/" target="_blank">animate.css</a>
* <a href="https://github.com/tgdev/animate-sass" target="_blank">animate sass版本</a>
*  <a href="https://github.com/gonsakon/animate-sass" target="_blank">Github 範例程式碼</a>

## 進入主題  
這個章節則是提供一個案例，  
讓大家了解如何使用Sass來管理程式碼，
Animate是我有在使用的CSS3 animation framework之一，  
CSS與Sass架構也相當易懂直覺，所以拿它來當範例剛剛好，  
首先我們就來看它<a href="https://github.com/gonsakon/animate-sass" target="_blank">官網Github</a>的教學，  
要看各個動畫效果可<a href="https://github.com/daneden/animate.css" target="_blank">點此</a>  
### 步驟一：載入 animate.css
```
<head>
  <link rel="stylesheet" href="animate.min.css">
</head>
```
### 步驟二：當有事件觸發時，可透過js/jQuery來動態載入Animate設定好的Class，讓該元素具有動畫效果
```
$('#yourElement').addClass('animated bounceOutLeft');
```

### 其他補充
animate可以自訂動畫過程與什麼時候播放
```
#yourElement {
  -vendor-animation-duration: 3s;  //過程總計要播放幾秒
  -vendor-animation-delay: 2s;     //過幾秒才開始播放動畫效果
  -vendor-animation-iteration-count: infinite;
}
```

## 設計流程  
像這種CSS3 animate 動畫效果，  
相當適合用在事件觸發的時候來使用，  
舉一些例子：  
* 當欄位輸入不正確時，使用`shake`效果讓他左右搖晃，傳達輸入錯誤的資訊  
* 點選關閉按鈕時，該HTML元素使用`bounceOutUp`使他往上滑消失不見。
* 當滑鼠滾輪滾到下面一定位置時，使用`fadeInLeft`讓某元素從左淡入出來
在我的影片與Github範例檔，  
有介紹如何做一個Login的介面出來，  
各位也可以從中瀏覽其開發流程。  

## 利用Sass管理Animate.css
使用Sass管理的優點有：
* Animate.css有二三十種動畫效果，如果你全部載入的話，未壓縮前是7x kb
* 可透過變數來統一管理所有細節

這裡我則找到一位開發者將他編譯成Sass的格式，  
Gitghub位置請<a href="https://github.com/tgdev/animate-sass" target="_blank">點此</a> ，  
請配合此連結再瀏覽下述內容：
先來介紹一下他的Sass架構：
```
//_animate.scss檔案
@import "helpers/mixins","helpers/settings";
@import	"animations/attention-seekers/bounce",
		"animations/attention-seekers/flash",
		"animations/attention-seekers/pulse",
		"animations/attention-seekers/shake",
		"animations/attention-seekers/swing",
		"animations/attention-seekers/wiggle",
		"animations/attention-seekers/wobble",
		"animations/attention-seekers/tada";
...後續皆是CSS動畫效果

```
剛開始在使用他時，  
編譯出來發現竟然都是空的，  
後來看了helpers/settings才發現，  
它使用了布林值來去管理要載入的動畫效果CSS，  
每個animate css效果都用了if條件包起來，  
像我們來看animations/bounce-enter/_bounceIn.scss：
```
@if $use-bounceIn == true {

	@-webkit-keyframes bounceIn {
		0% {
			opacity: 0;
			-webkit-transform: scale(0.3);
		}

		50% {
			opacity: 1;
			-webkit-transform: scale(1.05);
		}

		70% {
			-webkit-transform: scale(0.9);
		}

		100% {
			-webkit-transform: scale(1);
		}
	}
	..後面程式碼皆為瀏覽器前綴
}
```
你可以發現他的動畫都被一個if的條件包起來，  
再來我們回頭瀏覽`helpers/settings`這個scss檔，  
裡面變數則有這行：  
```
$use-bounceIn:	false !default;
```
從這邊你就可以猜出個端倪了，  
這位開發者他預設是把所有的設定都變成false，  
這樣就不會載入所有的CSS3 動畫程式碼，  
而是在專案有用到時，再到`_setting.scss`去將該功能改為true，  
如果你整個網站只有用到三四個功能，  
這樣編譯出來的CSS自然只有個位數kb而已，  

所以它的Sass架構就做到了：  
1.將設定都放到settings.css來做變數的統一管理  
2.用`@if`、`true & false`來做有用到的code才載入的功能。  

 
