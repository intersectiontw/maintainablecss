---
layout: chapter
title: FAQ
section: Extras
permalink: /maintainablecss/chapters/faqs/
description: 所有對 MaintainableCSS 的疑問在這裡解答。
---

找不到你要的答案嗎？在 [Github](https://github.com/adamsilver/maintainablecss.com/issues/new) 開一個 Issue 給我吧，我會儘快回覆你。感謝囉！

正體中文翻譯的問題請往這邊走：

## 什麼時候該用？

MaintainableCSS 的做法適合打造源遠流長、膾炙人口的響應式網站，並且打算將規模擴大。隨著時間演進的網站也很有用。

## 如果我不想用呢？

如果你不喜歡，請自便，或是採用你喜歡的部分。不過也請你告訴我哪裡不夠好，還有為什麼，因為我喜歡探索新事物，這樣可以共同學習成長。

## 這跟[請填入方法名稱]不是一樣嗎？

這些準則是經過打造許多不同類型的網站，並且根據許多經驗以及一起工作過的人影響，所產生的成果。

也就是說，我自己也認為：很明顯地跟 BEM 和 ECSS 相當類似。所以如果你正在使用其他習慣的方法，就繼續用下去。這邊隨時在需要時為您服務。

## 我可以翻譯你的書籍嗎？

目前已經有正體中文版（就是這裡）和[日文版](http://coliss.com/articles/build-websites/operation/css/maintainable-css-by-adam.html)，德文和西班牙文版正在進行中。你可以翻譯成其他語言，請跟我聯繫。

## 我一定要讓所有元素都有樣式名稱嗎？

簡單來說，不用。

大部分的情況，透過樣式名稱提供和鎖定元素比較好，因為可以讓程式碼一致、容易推理、高效能且輕巧。如果你打算這樣做：`.module h2`，並不會造成世界末日。

其實也有可能一定得這麼做，因為你可能使用 Markdown（或是類似的工具），就有機會**得要**鎖定元素，而不是樣式名稱，如以下所示：

	.someModule h1 {}
	.someModule h2 {}
	.someModule p {}
	.someModule ul {}

## 為什麼我一定要用在元件之前用模組名稱當作前綴詞？

好問題。事實上我之前也習慣不寫前綴詞，但是遇到很多麻煩⋯

	<div class="basket">
	    <div class="heading">

CSS 就會是這樣子：

	/* 模組 module */
	.basket {}

	/* basket 模組的標題元件 (heading component of basket module) */
	.basket .heading {}

第一個問題是在查看 HTML 的時候，會難以分辨模組和元件，讓維護變得有點困難。

第二個問題是使用 `.basket .heading`，**元件**會意料之外地繼承叫做 `.heading` 的**模組**樣式，我們希望樣式都經過封裝，限制於模組之內。

有個類似的情況：我最近打造的商店有**運送與退貨**模組，以及運送與退貨**頁面**，以下這樣的 CSS 就會造成問題：

	/* module */
	.productDetails .deliveryAndReturns {}

	/* page */
	.deliveryAndReturns {}

The page styles intefered with the module styles.
頁面的樣式就被模組的樣式干擾了。

## 如果有個泛用的樣式，要用在很多地方怎麼辦？例如：按鈕。

根據你的視覺設計需求而決定按鈕會造成非常多問題，因為以位置來看，它們通常有不同的間距、排版方向 (floating) 和其他的外觀規則，更不用提響應式網站的 Media queries。

非常**簡單**的例子：一個模組裡面，主要按鈕可能在容器裡向右對齊，而一些文字則是向左對齊。另一個模組裡面，它可能是固定寬度，置中對齊，有小一號的文字，下方設定 `margin-bottom` 留白。

這樣子，提取出共通的規則就會非常難以決定，因為你不會想要例外覆蓋 (override)，甚至更糟的是不敢更新一組提取出來的 CSS 語法。

然而，如果你決定這樣的提取是有用的，有兩種方式可以做。

第一，用逗號分隔不同的按鈕，讓它們套用相同的樣式，就像以下：

	.basket-removeButton,
	.another-loginButton,
	.another-deleteButton {
      /*共通樣式 common styles*/
	}

第二種做法是將按鈕做成模組：

	.primaryButton {
	  /*共通樣式 common styles*/
	}

最近的案子裡，事實上我用介於這兩者之間的方式。當時正在打造結帳流程，每頁都有一個「繼續到下一步驟」的按鈕，外觀都一樣。還有另外稱為「回到上一步驟」的超連結，所以我就這樣做：

	.checkoutActions-continueButton {
	  /*...*/
	}

	.checkoutActions-backButton {
	  /*...*/
	}

這個做法代表我把提取出來的地方分段，變成兩個一樣的模組，增進可維護性，也不會影響其他相似（但不是完全一樣）的按鈕。

## 那 h1 元素之類的繼承要怎麼做？

如果 `h1` （幾乎每次）在所有頁面、所有模組裡都是一樣的，就可以放寬心像這樣設定樣式：

	h1 {
      font-size: ...;
	  color: ...;
	}

然而，在我的經驗裡，**幾乎很少**有這種情況。所以我不建議這樣做，仍要讓樣式封裝在模組內，像這樣：

	/* <h1 class="module-heading"> */
	.module-heading {
	  font-size: ...;
	  color: ...;
	}

## 我要在哪裡放響應式網頁設計的 Media Queries？

一般來說，螢幕要為內容設計，而不是反過來。這個意思是，一個模組的斷點由模組本身決定，而且也**不是**由一組預先設定好的斷點決定，例如 "small"、"medium" 和 "large"。這樣的做法限制設計的可能性，而且有可能造成無謂地降低使用者經驗。

所以，所有的樣式，即使是那些包覆在 Media queries 裡面的，應該要緊接著放置在一般樣式旁邊：

	.basket {}

	@media(min-width: 500px) {
        .basket {}
	}

	@media(min-width: 1000px) {
	    .basket {}
	}

	.basket-heading {}

## 我要在哪裡放置修飾和狀態語法？

就跟 Media queries 一樣，狀態和修飾語法應該放在緊接著他們所屬元素的位置。

	.basket {}

	.basket-isHidden {}

	.basket-heading {}

	.basket-heading-someModifier {}

## 我應該加上註解嗎？

如果你採用許多模組放在單一 CSS 檔案的做法，用顯眼註解隔開的做法很棒：

	/********************************************
	* Basket
	********************************************/

	.basket {}

	.basket-heading {}

	/********************************************
	* Thinger
	********************************************/

	.thinger {}

	.thinger-details {}

## 這裡還是找不到答案嗎？

在 [Github](https://github.com/adamsilver/maintainablecss.com/issues/new) 開一個 Issue 給我吧，我會儘快回覆你。感謝囉！

正體中文翻譯的問題請往這邊走：