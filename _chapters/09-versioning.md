---
layout: chapter
title: 版本控制 (Versioning)
section: Extras
permalink: /chapters/versioning/
description: 學習 MaintainableCSS 如何在快速演變的網站裡，讓模組升級以及 AB 測試變得非常簡單。
---

Sometimes versioning modules can be helpful when the features of a website evolve over time. For example you may want to A/B test two versions of a module to see what performs better. Or the website might be going through a brand refresh.

When you have multiple versions of a module in your codebase, it can be tempting to again reuse the same HTML and CSS to do this. *MaintainableCSS* again dictates that you duplicate and provide a unique name to aid maintainability.

當網站功能隨著時間演進，將模組進行版本差異化有時候非常有幫助。舉例來說，你可能想要將兩個版本的模組進行 AB 測試，觀察哪個有較好的表現。或者網站正在進行重塑品牌形象。

當程式碼裡面的模組有多個版本，它會誘惑你重複使用相同的 HTML 和 CSS。**MaintainableCSS** 再次要求你必須複製，然後賦予獨特的名稱，增進可維護性。

	/* 現有的模組 */
	.someModule {}

	/* 新版本的模組 */
	.someModuleVariant2 {}

All you have to do is create two separate modules with a unique module name and you can edit each one independently and in your own time.

你要做的事情就只有：用一個獨特的模組名稱，建立兩個不同的模組。這樣就可以照你的步調各自編輯它們。