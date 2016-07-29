---
layout: chapter
title: Javascript
section: Extras
permalink: /chapters/javascript/
description: 如何同時撰寫可維護的 CSS 和 Javascript。
---

你可能會想要用 Javascript 在不同的模組（或元件）套用**相同**的行為。這裡舉出的基本範例是兩個模組，都有 **isHidden** 狀態語法，把模組隱藏起來。

**有沒有可能遵循 MaintainableCSS 的標準做到這件事，而且不用重複動作？**

有兩種做法。

## 一、把狀態語法封裝進模組

如果有個建構式 (constructor) 負責顯示（或隱藏）某元素，做法會是在 instantiation 時，指定專屬於該模組的樣式名稱。

	var module1Collapser = new Collapser(element1, {
	  cssHideClass: 'moduleA-isHidden'
	});

	var module2Collapser = new Collapser(element2, {
	  cssHideClass: 'moduleB-isHidden'
	});

然後依照以下的方式重複使用 CSS 樣式：

	/* isHidden */
	.moduleA-isHidden,
	.moduleB-isHidden {
      display: none;
	}

只不過，如果你覺得這個方式可能造成維護上的問題，那可以試試看另一種做法⋯

## 二、建立全域的狀態樣式

如果你覺得第一種做法造成可維護性的問題，那麼這個定義一組全域狀態樣式，讓不同模組重複使用的方式可能會比較好。

	.globalState-isHidden {
      display: none;
	}

在這個情境下，當建構式 `Collapser` 從內部參照全域樣式，你就不必用逗號劃分模組的狀態，也不用指定模組的狀態樣式。

	var module1Collapser = new Collapser(element1);
	var module2Collapser = new Collapser(element2);

這個方式因為要變動的程式碼比較少，看起來**好像**比較容易維護，它仍需要經過思慮與小心使用，要不然同樣會造成麻煩。

例如：可能每一個模組都有其他視覺上的不同之處，讓 **isHidden** 樣式沒出現效果。如果確實有所不同，那麼用上面提到的第一種方法比較好，因為比較容易推導和修改，而不會導致意料之外得要重做的地方。

<!-- display: flex vs display: block -->