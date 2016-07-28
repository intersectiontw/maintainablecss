---
layout: chapter
title: 慣例 (Conventions)
section: Core
permalink: /chapters/conventions/
description: 學習 MaintainableCSS 採用之撰寫模組、元件與狀態語法的簡易慣例。
---

慣例（或是共識）是工程師之間爭辯的來源，其中最重要的就是可讀性與一致性。因此，**MaintainableCSS** 採用以下這些慣例：

	/* 方形括號代表任選 (optional) */
	.<moduleName>[-<componentName>][-<state>] {}

這裡是一些「搜尋結果」實際情況的範例：

	/* 模組語法的容器或最上層 */
	.searchResults {}

	/* 模組的元件 */
	.searchResults-heading {}
	.searchResults-item {}

	/* 狀態語法：例如描述 AJAX 讀取中 */
	.searchResults-isLoading {}

每一個樣式名稱都是語意化的；模組、元件與狀態都以橫槓隔開；都以小駝峰式命名法 (lowerCamelCase) 方式區分大小寫。

這些慣例在接下來所有章節都會看到。