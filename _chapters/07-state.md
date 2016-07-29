---
layout: chapter
title: 狀態語法 (State)
section: Core
permalink: /chapters/state/
description: 學習如何根據狀態提供模組和元件不同的樣式，例如顯示、隱藏和讀取中。
---

通常在畫面比較豐富的使用者介面，得要根據狀態 (state) 設定模組或元件的樣式，讓它們之間看起來不一樣。像是：**顯示**、**隱藏**、**使用中 (active)**、**非使用中 (inactive)**、**關閉 (disabled)**、**讀取中**和**讀取完成**⋯等。這件事情得要用額外的樣式名稱進行溝通。

## 「封裝」狀態語法 (encapsulating state)

假設有個模組稱之為 **myModule**。就套用稱為 `isActive` 的樣式，如以下程式碼：

	<div class="myModule isActive">

但是 `isActive` 非常有可能用在其他不同的模組，而且對於不同的模組來說，「使用中」的意義也會不一樣，這就違反了 **MaintainableCSS** 的基本規則，也就是說：它沒有分裝進對應的模組。 

## 將狀態套用至模組

假設有個模組稱之為 **myModule**。

	.myModule {}

Here are some states we might need to apply to `myModule`.

這裡有一些狀態設定，有可能要套用到 `myModule`。

	.myModule-isDisabled {}
	.myModule-isActive {}
	.myModule-hasProducts {}
	.myModule-isHidden {}
	.myModule-isLoading {}

And the HTML needs to be as follows:

HTML 得要這樣子撰寫：

	<div class="myModule myModule-isDisabled">
	    <p class="myModule-title">

## 將狀態套用至元件

如果你只想要在 **title** 元件套用狀態，那就把 `myModule-title-isDisabled` 加入此標題元件，方法如下：

	<div class="myModule">
       <p class="myModule-title myModule-title-isDisabled">

Phew, that was easy.

呼，幸好就是這麼簡單。
