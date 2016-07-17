---
layout: chapter
title: 語意化 (Semantics)
section: Background
permalink: /chapters/semantics/
description: 為何要依據它是什麼而取名，而不是他的外表，或是可以進行什麼動作。這是撰寫良好架構與易於維護 CSS 程式碼的基礎。
---

**長話短說:** 依照它**是什麼**命名，而不是**長相如何**或**可以做什麼**。 

## 短話長說

語意化 HTML (Semantic HTML) 不只關於我們如何使用元素 (elements) — 它很直覺，例如超連結就要用 `<a>`；表格呈現的資料就要用 `<table>`；一個段落就要用 `<p>`⋯等等。

更重要的是，它還關係到我們增加的樣式名稱（與 ID），它們提供**額外**與 CSS（和 Javascript）的連結，能夠適當強化功能。
More importantly, it's about the class names (and IDs) we add, that provide *additional* hooks for CSS (and Javascript) to enhance as appropriate.

說到命名，很多人容易不經思考就增加樣式名稱，但是命名非常重要。
It's easy to add class names without thought as to their naming but naming is very important.

> 「資訊科學裡只有兩件難事：Cache Invalidation 和命名。」
<br>&mdash; <cite>Phil Karlton</cite>

這是因為人類擅長於理解與人類的溝通，但是不擅於理解縮寫的、沒有情境的抽象物品。

## 好與不好的樣式名稱範例

試著找出非情境式與情境式樣式名稱之間的不同⋯

	<!-- 不好 -->
	<div class="red pull-left">
	<div class="grid row">
	<div class="col-xs-4">

這樣完全不清楚這些 HTML *代表*的意義。*可能*可以*知道*這些東西看起來如何（在小或大的螢幕），但是頂多就這樣。

	<!-- 好 -->
	<div class="header">
	<div class="basket">
	<div class="product">
	<div class="searchResults">

這裡我就很清楚知道我在看什麼。我知道這些 HTML 所代表要做的事情。

Here I know exactly what I am looking at. I know the intention of what this HTML represents. And I have no idea how it looks&mdash;that's what CSS is responsible for. Semantic class names mean something to both HTML *and* CSS (and JS).

So **why** else should we use semantic class names?

## Because it's easier to understand.

Whether you're looking at the HTML or the CSS, you know what you're affecting. With visual class names you end up having to sprinkle several class names on to each element, ending up with a vague understanding of the intention of these visual class names. This is hard to maintain.

## Because we are building responsive websites.

Styles often need changing based on viewport size. For example, you might float elements on big screens and not on small screens. So if you have a class called `clearfix` but you don't clear on small screens, then you now have misleading code.

If you use semantic class names, then you can style them differently based on media queries making it easier to maintain.

## Because semantic class names are easier to find.

If an element has classes based on how it looks such as `.red`, `clearfix` and `.pull-left`, then these classes will be scattered all over the codebase&mdash;so if you’re trying to hunt for a particular piece of HTML, the class name is not going to help you.

On the other hand, if your class names are semantic, a search will find the HTML in question. Or more typically, if you're beginning your search via the HTML (think: inspecting an element) then finding unique CSS selectors based on the class name will be far easier.

## Because you don't want unexpected regression.

If you have utility non-semantic classes that describe the look then when you edit one of these classes, they will propagate to every single element with that class. Knowing CSS as you do, do you feel comfortable that the propagation didn't cause unexpected problems elsewhere?

Semantic class names are unique, so when editing one, you *can* feel comfortable that your change only applies to the module in question as you intended, making maintenance easier.

## Because you don't want to be afraid to update code.

Directly linked with the previous point about regression, when you don't feel comfortable touching code, you end up causing problems or being afraid to touch it at all. Therefore you end up with redundant code, increasing maintenance issues.

## Because it helps automated functional testing.

Automated functional tests work by searching for particular elements, interacting with them (typing in text, clicking buttons and links etc) and verifying based on that.

If you have visual class names all over the HTML, then there is no reliable way to target particular elements and act upon them.

## Because it provides meaningful hooks for Javascript to enhance.

Just like these hooks help automated testing, they are also useful to enhance behaviour with Javascript. Visual class names can't be used as a reliable way to target modules or components.

## Because of general maintenance concerns.

If you name something based on what it is, you won't have to touch the HTML again i.e. a heading is always a heading, no matter what it *looks* like.

The styling might change but you only have to update the CSS. This is otherwise known as Loose Coupling and this improves maintainability.

## Because utility classes increase noise when debugging.

When debugging an element, there will be several applicable CSS selectors making it noisey to debug.

## Because the standards recommend it.

On using the class attribute, HTML5 specs say in 3.2.5.7:

> "[...] authors are encouraged to use values that describe the nature of the content, rather than values that describe the desired presentation of the content."

## Because you get a performance bump.

This is a *very* small benefit but when you have one class name per element, you end up with smaller HTML. With visual classes you end up with multiple class names per element and that can add up.

## Because it adheres to the reuse rule.

If you don't use semantic class names, then you will likely be breaking the rules of reuse. Read the next chapter to find out more.

<!--## Why? Because visual class names might declare the same property!

It's likely that several different utility classes could refer to the same property meaning order matters and performance degrades.

Think of an example of this.
-->

## Final thoughts about semantics

Semantic class names are a corner stone of *MaintainableCSS*. Without this, everything else makes little sense. So name something based on what it is and everything else follows.
