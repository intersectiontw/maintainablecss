---
layout: chapter
title: IDs
section: Background
permalink: /chapters/ids/
description: 學習為何用 ID 當作設定樣式的連結會造成許多問題，還有正確的替代方案。
---

**長話短說：** **請勿**用 ID 進行樣式設定。

**為什麼** 我們不應該把 ID 用在 CSS？

## 因為優先權的問題 (specificity)

根據權重順序，[ID 的優先權高於樣式](http://www.w3.org/TR/css3-selectors/#specificity)。因此，樣式名稱 (style names)裡的設定無法輕易蓋過在 ID 裡的。

當你需要對 HTML 加上額外的意義時，例如狀態語法，這就會造成問題，這部分我專門寫了一章進行討論。

	#someModule {
	    color: red;
	}

	.someModule-override {
	    color: blue;
	}

如果在元素同時加上 ID 和樣式，顏色永遠是 red。

	.someModule {
	    color: red;
	}

	.someModule-override {
	    color: blue;
	}

現在就會變成 blue 了。

## 但是，有時候一定得用 ID？

有時候，ID 是必要的。例如表單控制就是以 ID 連結 label。文件內的錨點也是靠 ID 移動過去，這些都能夠增進使用者經驗。應該要為額外的動作正確使用它，而不是用在設定樣式。

## 關於 "ID" 的結尾想法
避免用 ID 當做進行樣式設定的連結，但是在其它用途就安心使用。在使用 ID 時，也要用跟樣式一樣的命名慣例，這在其它章節有進行說明。