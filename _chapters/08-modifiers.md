---
layout: chapter
title: 修飾語法 (Modifiers)
section: Core
permalink: /chapters/modifiers/
description: 使用修飾語法，改變只有一些些不同的外觀。
---

修飾語法跟狀態語法很類似，它們都可以改變或是覆蓋模組的樣式設定。在數個幾乎一樣設計，僅有些許不同的模組（或元件）之間非常好用。

以下這兩個範例可以說明得更清楚：

## 範例一：不同的背景圖片

最近我手上的範例是電子商務網站，每一個分類頁面的最上方有標題，而背景圖片根據分類名稱而改變，方式如下：

	<!-- when viewing the "boys" category page -->
	<div class="categoryHeader categoryHeader-boys">

	<!-- when viewing the "girls" category page -->
	<div class="categoryHeader categoryHeader-girls">

The CSS for each header is almost identical except for the modifier overrides:

每一個標題的 CSS 幾乎都一樣，例外的情況用修飾語法覆蓋：

	.categoryHeader {
	    padding-top: 50px;
	    padding-bottom: 50px;
	    /* etc */
	}

	.categoryHeader-boys {
	    background-image: url(/path/to/boys.jpg);
	}

	.categoryHeader-girls {
	    background-image: url(/path/to/girls.jpg);
	}

## 範例二：不同的按鈕顏色

在同一個網站，我們根據產品的顏色設計其頁面，可以在 CMS 裡面，依照情況設定**加入購物車**按鈕的背景顏色。

	<!-- 查看產品外觀是綠色的情況 -->
	<input class="addToBasketButton addToBasketButton-green">

綠色按鈕的 CSS 除了 background-color，其他都一樣，如以下所示：

	.addToBasketButton {
	    padding: 10px 30px;
	    text-align: center;
	    /* etc */
	}

	.addToBasketButton-green {
	    background-color: green;
	}

你可能已經注意到 **green** 這個字。這是因為 green 是設定產品的時候，透過 CMS 輸入的數值（跟上面的分類範例類似），green 只是跟 id 一樣的用法。