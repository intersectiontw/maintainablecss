---
layout: chapter
title:  結構 (Organisation)
section: Extras
permalink: /chapters/organisation/
description: 學習如何整理 CSS 檔案。
---

**可探索性 (Discoverability)** 是撰寫可維護樣式的時候，很重要的一部份。當專案隨著時間成長，它就會越來越重要。這時候有兩種做法可以考慮，我們將依序進行討論。

## 一、在單一資料夾放置 CSS

	/path/to/css
	    /vendor
            some3rdParty.css
            someOther3rdParty.css
	    /yourApp
	        some.css
	        global.css
	        basket.css

第三方的 CSS 檔案放在 `/vendor` 資料夾，而你自行撰寫的 CSS 應該放在 `/yourApp`。這裡的 **/yourApp** 代表這個專案的名稱。

這個方法通常可以簡化配置流程，因為一般來說，bundling、壓縮和其他類似的自動化流程都採用單一目標資料夾。

這是我最常使用的做法，但是不代表這就是最好的。

## 二、根據模組資料夾放置 CSS

這個方式根據模組劃分資料夾，然後放置專屬的 CSS，把所有相關的功能封裝進來。

	/basket
      /controllers
        ...
      /templates
        basket.html
        emptyBasket.html
      /partials
        basketHeader.html
        basketSummary.html
      /js
        ...
      /css
        basket.css
	/header
	  ...

如果你跟我一樣，一直以來都在用第一種方式。這個做法一開始會覺得很詭異，但是它真的很方便。

### 那全域 CSS 怎麼辦呢？

你得用一個資料夾放置全域 CSS，或是一般常用的語法：

	/global
	  /css
        resetPerhaps.css
        global.css
        etc.css
	/basket
	  ...as above...
	/header
       ...

## 31 個 CSS 檔案的問題

不管你決定用哪種做法，都要記得有 31 個 CSS 檔案的限制問題。

有些瀏覽器，像是 IE9，不會讀取第 32 個（包含以上）CSS 檔案。在確定版本這還好，因為你本來就必須要整合 CSS 檔案，減少 HTTP Request。但是在開發過程中，你通常希望以原始檔案進行作業，才容易偵錯。

如果**有編譯的流程**，比如說可能是使用 CSS 預處理器，那就不用擔心。因為檔案在開發過程已經結合在一起。

因為想要輕鬆地偵錯原始碼，而**沒有編譯的流程**，那就要注意到這個問題，可以有這些做法：

**第一種方式**：採用編譯流程，其實也就是你在確定版本要做的事情，有必要的時候在難用的瀏覽器內偵錯。

**第二種方式**是確保不要超過 31 個檔案。這個方式代表你無法採用上面提到的第二種：根據模組放置 CSS 檔案。因為大部份的網站都需要超過 31 個模組。

如果你決定限制 CSS 檔案數量，就必須要花些時間研究在一個 CSS 資料夾內，模組要以何種方式分類。舉例來說，我最近把 **deliveryAddress**、**paymentDetails** 和 **orderConfirmation** 這三個模組放入 `checkout.css`。