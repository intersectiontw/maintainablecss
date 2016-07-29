---
layout: chapter
title: 版本控制 (Versioning)
section: Extras
permalink: /maintainablecss/chapters/versioning/
description: 學習 MaintainableCSS 如何在快速演變的網站裡，讓模組升級以及 AB 測試變得非常簡單。
---

當網站功能隨著時間演進，有時候將模組進行版本差異化非常有幫助。舉例來說，你可能想要將兩個版本的模組進行 A/B 測試，觀察哪個有較好的表現。或者網站正在進行重塑品牌形象。

當程式碼裡面的模組有多個版本，它會誘惑你重複使用相同的 HTML 和 CSS。**MaintainableCSS** 再次要求你必須複製，然後賦予獨特的名稱，增進可維護性。

	/* 現有的模組 */
	.someModule {}

	/* 新版本的模組 */
	.someModuleVariant2 {}

你要做的事情就只有：用一個獨特的模組名稱，建立兩個不同的模組。這樣就可以照你的步調各自編輯它們。