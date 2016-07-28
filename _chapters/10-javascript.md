---
layout: chapter
title: Javascript
section: Extras
permalink: /chapters/javascript/
description: 如何同時撰寫可維護的 CSS 和 Javascript。
---

You may want to use Javascript to apply the *same* behaviour to multiple modules (or components). A basic example would be two modules that have the same *isHidden* state which hides the module.

**How might you do this whilst adhering to MaintainableCSS guidelines and without having to repeat yourself?**

There are two approaches you can take.

你可能會想要用 Javascript 在不同的模組（或元件）套用**相同**的行為。這裡舉出的基本範例是兩個模組，都有 **isHidden** 狀態語法，把模組隱藏起來。

**有沒有可能遵循 MaintainableCSS 的標準做到這件事，而且不用重複動作？**

有兩種做法。

## 1. Encapsulating states to the module

If you have a constructor that is responsible for making an element show (or hide) then consider specifying a class name that pertains to the module during instantiation:

## 一、把狀態語法封裝進模組

如果有個建構式 (constructor) 負責顯示（或隱藏）某元素，做法會是在 instantiation 時，指定專屬於該模組的樣式名稱。

	var module1Collapser = new Collapser(element1, {
	  cssHideClass: 'moduleA-isHidden'
	});

	var module2Collapser = new Collapser(element2, {
	  cssHideClass: 'moduleB-isHidden'
	});

Then reuse the CSS styles as follows:

然後依照以下的方式重複使用 CSS 樣式：

	/* isHidden */
	.moduleA-isHidden,
	.moduleB-isHidden {
      display: none;
	}

However, if you find this approach causes maintainability issues for whatever reason then you could try an alternative approach...

只不過，如果你覺得這個方式可能造成維護上的問題，那可以試試看另一種做法⋯

## 2. Creating a global state class

If you find the first approach causes maintainability issues then it might be better to define a global state class for reuse across different modules:

## 二、建立全域的狀態樣式

如果你覺得第一種做法造成可維護性的問題，那麼這個定義一組全域狀態樣式，讓不同模組重複使用的方式可能會比較好。

	.globalState-isHidden {
      display: none;
	}

In this scenario, you no longer need to comma delimit each module state, and you no longer need to specify the module state class during instantiation as the `Collapser` constructor will reference the global class name from within:

在這個情境下，當建構式 `Collapser` 從內部參照全域樣式，你就不必用逗號劃分模組的狀態，也不用指定模組的狀態樣式。

	var module1Collapser = new Collapser(element1);
	var module2Collapser = new Collapser(element2);

Whilst this approach might *seem* to be more maintainable due to there being less code to update, it does require thought and care which in turn can be problematic.

For example it might be that there are other visual differences specific to each module that hang off the *isHidden* class. If there are any differences at all, it may well be better to go with the first approach described above as it's easier to reason about and update without causing unexpected regression.

這個方式因為要變動的程式碼比較少，看起來**好像**比較容易維護，它仍需要經過思慮與小心使用，要不然同樣會造成麻煩。

例如：可能每一個模組都有其他視覺上的不同之處，讓 **isHidden** 樣式沒出現效果。如果確實有所不同，那麼用上面提到的第一種方法比較好，因為比較容易推導和修改，而不會導致意料之外得要重做的地方。

<!-- display: flex vs display: block -->