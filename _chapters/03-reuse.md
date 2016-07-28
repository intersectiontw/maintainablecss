---
layout: chapter
title: 重複使用 (Reuse)
section: Background
permalink: /chapters/reuse/
description: 學習為什麼要避免重複使用 (reuse)，並且採用能讓 CSS 更易於維護的循環使用 (repetition)。
---

**長話短說：** 不要試著將樣式重複使用。採用複製優先 (duplication-first) 的做法。

> 「DRY 方式 (Don't Repeat Yourself) 常常被誤解為絕對不要重複做一件完全相同的事情兩次⋯。事實上這是非常不切實際的，而且通常對工作效率有反效果，導致刻意抽象、過多考量與工程化 (engineered) 的程式碼。」
<br>&mdash; <cite>Harry Roberts, CSS Wizardy</cite>

<!-- > &ldquo;DRY is often misinterpreted as the necessity to never repeat the exact same thing twice [...]. This is impractical and usually counterproductive, and can lead to forced abstractions, over-thought and [over]-engineered code.&ldquo;
<br>&mdash; <cite>Harry Roberts, CSS Wizardy</cite> -->

Don't take this the wrong way&mdash;MaintainableCSS has various strategies for reuse which I will talk about later. The problem is that trying to reuse the bits *inbetween* the curly braces is problematic. Here's why:

## Because styles change based on breakpoints.

請不要誤解這個說法 &mdash; MaintainableCSS 有各種重複使用的策略，在稍候會進行解釋。試著重複使用大括弧**之間**的東西本身就充滿著問題，就是問題所在。原因是：

## 因為樣式是根據斷點 (breakpoints) 改變樣式

Building responsive sites mean that we style elements differently based on viewport size. Imagine trying to build a 2 column grid that:

- has 50px and 20px padding on large and small screens respectively.
- has 3em and 2em font-size on large and small screens respectively.
- on small screens each column is stacked below each other. Note: "column" is now misleading.

打造響應式的網站代表：我們根據螢幕的大小為元素設定不同的樣式。請想像設計一個兩欄式的網格：

- padding 在大螢幕是 50px，而在小螢幕是 20px。
- font-size 在大螢幕是 3em，而在小螢幕是 2em。
- 在小螢幕每一欄都互相堆疊。請注意：現在「欄」會造成誤解了。

With this in mind how can you utilise these atomic class names: `.grid`, `.col`, `.pd50`, `.pd20`, `.fs2` and `fs3` and achieve these specs?

在這樣的設定之下，你要如何使用基礎樣式名稱 (atomic class names)：`.grid`、`.col`、`.pd50`、`.pd20`、`.fs2` 和 `fs3`，然後達到這個要求？

	<div class="grid">
	  <div class="col pd50 pd20 fs3 fs2">Column 1</div>
	  <div class="col pd50 pd20 fs3 fs2">Column 2</div>
	</div>

You can see this just isn't going to work. You now need some crazy class names such as `fs3large`. This is just the tip of iceberg when it comes to maintenance issues.

Alternatively, take the following semantic mark-up that doesn't attempt to reuse styles:

你馬上就發現這行不通。你甚至需要一些像是 `fs3large` 這樣令人抓狂的樣式名稱。事實上這只是維護議題中的冰山一角。

因此，請遵循下方沒有試著要重複使用樣式的情境式語法：

	<div class="someModule">
	  <div class="someModule-someComponent"></div>
	  <div class="someModule-someOtherComponent"></div>
	</div>

Ensuring this is styled as specified above, is now a simple task with 6 CSS declarations needed in total, 3 of which reside within media queries.

根據上方說明的規格，現在只是總共 6 個 CSS 宣告的簡單工作，其中 3 個在 media queries 裡面。

## Because styles change based on states.

How do you make `<a class="padding-left-20 red" href="#"></a>` to have padding 18px, a slight border, a background of grey and a text colour as a slightly darker shade of red when it's hovered or focused of active i.e. `:hover`,`:focus`, `:active` etc?

The short answer is you can't. Try to avoid having to fix self-induced problems.

## 因為樣式根據狀態改變

當滑鼠移入、聚焦、點擊，也就是 `:hover`、`:focus`、`:active` 的狀態時，你要如何讓 `<a class="padding-left-20 red" href="#"></a>` 是 padding 18px、灰色背景和稍微暗一些的紅色？

簡單來說，不能。請避免得去修好自己造成的問題。

## Because reuse makes debugging more difficult.

When debugging an element, there will be several applicable CSS selectors playing a part making it noisy.

## 因為重複使用讓偵錯更加困難

對一個元素進行偵錯的時候，會有好幾個同時設定的 CSS selector，干擾工作進行。

## Because granular styles aren't worth bothering with.

If you're going to do `<div class="red">` you may as well do `<div style="color: red">` which is more explicit anyway. But we don't want to do this because we don't want to mix concerns.

## 因為瑣碎的樣式不值得花時間專門設定

如果打算這樣寫：`<div class="red">`，那還不如直接寫成：`<div style="color: red">`，它還更直覺。只不過，我們也不打算這樣做，因為不想要混搭指令。

## Because visual class names don't hold much meaning.

Take `red`. Does this mean a red background? Does this mean red text? Does this mean a red gradient? What tint of red does this mean?

## 因為視覺的樣式名稱沒有太大的意義

以 `red` 舉例。它代表紅色的背景？紅色的文字？還是紅色的漸層？這個紅色是怎麼樣的風格呢？

## Because updating a "utility" class applies to all instances.

This sounds good but it isn't. You end up applying changes where you didn't mean to. Think regression. Alternatively, you end up scared to touch this utility class so you end up with `.red2`. Then you end up with redundant code. Obviously this is not fun to maintain.

## 因為修改一個「工具」樣式就會套用到全部

這聽起來很棒，其實不然。總有一天你會改到不想要變的地方，想想要要重做多少工。這導致你害怕修改這些工具樣式，開始出現 `.red2` 這樣的累贅程式碼。維護起來一點都不有趣。

## Because non-semantic class names are hard to find.

If an element has classes based on how it looks such as `.red`, `.col-lg-4` and `.large`, then these classes will be scattered all over the codebase so searching for "red" will yield many results across the HTML templates, making it hard to find the element in question.

If you use semantic class names, a search should yield just one result. And if it yields more than one result, then this should indicate a problem that needs dealing with.

Note: if you have a repeated *component* within a module, then searching might yield several results within 1 file. That is, a module would typically live in a single template.

## 因為非語意化的樣式名稱很難找到

如果有一個元素用它的外觀來定義，例如 `.red`、`.col-lg-4` 和 `.large`，這些樣式就遍佈在程式碼的四處，在 HTML 文件尋找 "red" 出現非常多結果，難以找到你想要的元素。

如果你使用語意化樣式名稱，搜尋只會有一個結果。如果出現多個結果，代表有些問題要處理一下了。

附註：如果你在一個模組裡有重複的**元件**，那一個檔案內就會出現多個搜尋結果。這個意思是說，一個範本裡通常只有一個模組。

## Because reuse causes bloat.

If you attempt to reuse every single *rule* you'll end up with classes such as: `red`, `clearfix`, `pull-left`, `grid` which leads to HTML bloat:

	<div class="clearfix pull-left red etc">

Bloat makes it harder to maintain and degrades performance (albeit in a minor way).

## 因為重複使用造成笨重的感覺

如果打算重複使用每一個**規則**，`red`、`clearfix`、`pull-left`、`grid` 等樣式會讓 HTML 感覺很笨重，例如：

	<div class="clearfix pull-left red etc">

這樣笨重的樣式設定難以維護，降低效能（越少越好）。

## Because reuse breaks semantics.

If you strive to reuse the bits inbetween the curly braces to create "atomic" class names, then you encounter all the problems stated in the chapter about [Semantics](/chapters/semantics/). Read that chapter now, if you haven't already.

## 因為重複使用破壞語意化

如果你用盡可能把大括弧內的每一行都做成可重複使用，也就是「基礎」樣式名稱 ("atomic" class names)，那就會遭遇到所有在[語意化](/chapters/semantics/)章節說過的問題。如果你還沒有準備好，現在就先去讀那一章。

## What if I really want to reuse a style?

It is extremely rare, but there are times when it really does make sense to reuse a style. In this case use the comma in your selectors and place it in a well named file.

For example let's say you wanted a bunch of different modules or components to have red text you might do this:

	/* colours.css */

	/* red text */
	.someSelector,
	.someOtherSelector {
		color: red;
	}

Remember though that if any selector deviates, even a little bit, then remove it from the common list and duplicate. You must be very careful with something like this. Do it for convenience, not for performance. Your mileage may vary.

## 如果我真的想要重複使用呢？

這非常罕見，但是有時候重複使用樣式確實也有道理。這個情況可以用逗號 (,) 分隔 selector，放到適當的檔案名稱裡面。

舉例來說：你想要讓一些不同的模組或元素有紅色的文字顏色，就會這樣做：

	/* colours.css */

	/* red text */
	.someSelector,
	.someOtherSelector {
		color: red;
	}

請記得如果任一 selector 有不同的設定，即使只是一點點，也要從共用的清單裡刪除，然後複製一組。跟這類似的事情你都必需非常地小心。你是為了方便，而不是為了效能，這會讓你的做法天差地遠。

## What about mixins?

CSS preprocessors allow you to create mixins which can be really helpful because they provide the best of both worlds but they should be designed with caution.

You have to be very careful to update a mixin because it propagates in all instances just like utility classes. It can be problematic to edit and instead you create new mixins that are slightly different causing redundancy and maintenance problems.

Also, mixins can become very complicated with lots of params, conditionality and large declarations of styles. All of this makes it complicated and complicated is hard to maintain.

To mitigate, you can make mixins really granular. For example you could have a "red text" mixin which is certainly better. But then again, the declaration of that mixin is basically the same as a declaration of red text&mdash;might as well just declare that instead.

If you need to update it in multiple places, then a search and replace might just do it, depending on your context. And even if you did use a mixin, when red changes to orange, you will have to do a search and replace anyway, because the mixin name will otherwise be misleading.

This does not mean mixins are "bad"&mdash;in fact they can be very helpful. For example, being able to apply *clearfix* rules across different elements at different breakpoints is probably a very helpful thing to do for maintainability. Just make sure to use them with care.

## 那 mixin 怎麼辦呢？

CSS 預處理器 (preprocessors) 的 mixin 功能非常好用，因為提供兩造意見的優點，但是仍得要小心設計。

修改 mixin 的時候跟功能樣式一樣，會一口氣影響所有採用該語法的地方，所以還是要非常地小心。直接修改會造成很多問題，所以你再做一個稍微不同的 mixin，反而讓程式碼冗長還有維護困難。

而且，設定許多參數、條件和宣告的 mixin 會變得非常複雜。複雜就會難以維護。

減輕這種情況的方法是讓 mixin 盡量用在單一用途。例如，「紅色文字顏色」的 mixin 就會好很多。然而，同樣的問題再度產生：此 mixin 基本上跟設定紅色文字一樣，不如就直接設定一組。

如果得要在很多地方修改，那麼就是搜尋、取代就好，端看你的使用情境。即使你採用 mixin，例如要把 red 改為 orange，那還是要進行搜尋、取代，因為 mixin 的名稱可能會造成誤導。

這不代表 mixin 很不好，事實上它們非常好用。舉例來說：它用在不同的元素，在不同的斷點套用 *clearfix* 時，要維護起來非常方便。只要小心使用即可。

## What about performance?

I don't have stats to hand, but I can very confidently say that it's not wise to practice premature optimisation. Let's say you have a very large CSS codebase (100KB or more).

Firstly, I *guess* you *might* save yourself a few KB. Secondly, there are alternative paths to improving performance and thirdly, you probably have redundant code due to a lack of maintainability.

Also consider that one or two images are likely to be far larger than the entire CSS so exerting energy here is probably of little value.

## 那麼效能呢？

我手邊沒有統計資料，但是確信過早實施最佳化 (premature optimization) 並不是個好法子。比如說，你的 CSS 程式碼非常龐大（100KB 以上）。

首先，我**猜**你**可能**有能力自行節省幾 K 的容量；第二：還有很多增進效能的好方法；第三：就是因為缺乏維護性而讓程式碼臃腫肥大。

同時也請考量一兩張圖片就可能比整個 CSS 檔案還要大很多，所以在這花費大量精力帶來的價值很少。

## Is this violating DRY principles?

Attempting to reuse `float: left` as an example, is akin to trying to reuse variable names in different Javascript objects. It's simply not in violation of DRY.

## 它有違反 DRY 原則嗎？

舉例來說，想要重複使用 `float: left` 與在不同的 Javascript 物件重複使用變數名稱類似，並沒有違反 DRY。

## Final thoughts on reuse

Reuse and DRY are such important principles in software engineering but when it comes to CSS, striving to reuse too much ironically makes maintenance *harder*. However, there are times when reuse and abstraction makes sense which is discussed in later chapters.

## 關於「重複使用」的結尾想法

重複使用和 DRY 在軟體工程是很重要的原則，但是用在 CSS 的時候，很諷刺地，過於追求重複使用卻讓維護更為**困難**。當然，重複使用與簡略化也是有合理的時候，這在之後的章節舉行討論。
