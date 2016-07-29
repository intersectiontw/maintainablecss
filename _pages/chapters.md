---
layout: chapters
id: chapters
permalink: /chapters/
title: "Chapters"
---

{% assign prefaceChapters = site.chapters | where:'section', 'Preface' %}
{% assign backgroundChapters = site.chapters | where:'section', 'Background' %}
{% assign coreChapters = site.chapters | where:'section', 'Core' %}
{% assign extraChapters = site.chapters | where:'section', 'Extras' %}

# Chapters

## 前言

<ol>
  {% for chapter in prefaceChapters %}
    <li><a href="{{ chapter.url }}">{{ chapter.title }}</a></li>
  {% endfor %}
</ol>

## 背景

{% assign backgroundStart = prefaceChapters.size | plus: 1 %}

<ol start="{{backgroundStart}}">
  {% for chapter in backgroundChapters %}
    <li><a href="{{ chapter.url }}">{{ chapter.title }}</a></li>
  {% endfor %}
</ol>

## 核心

{% assign coreStart = backgroundStart | plus: backgroundChapters.size %}

<ol start="{{coreStart}}">
	{% for chapter in coreChapters %}
		<li><a href="{{ chapter.url }}">{{ chapter.title }}</a></li>
	{% endfor %}
</ol>

## 附錄

{% assign extrasStart = coreStart | plus: coreChapters.size %}

<ol start="{{extrasStart}}">
	{% for chapter in extraChapters %}
		<li><a href="{{ chapter.url }}">{{ chapter.title }}</a></li>
	{% endfor %}
</ol>