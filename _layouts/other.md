<!DOCTYPE HTML>
<html dir="ltr" lang="zh-Hant-TW">
	<head>
	    <title>{{ page.title }} | {{ site.name }}</title>
	    {% include head.html %}
	</head>
	<body>
		{% include header.html %}
        <div class="content">
			<h1>{{page.title }}</h1>
           	{{ content }}
        </div>
        {% include subscribeForm.html %}
        {% include footer.html %}
	</body>
</html>