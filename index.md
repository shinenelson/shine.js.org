Hi, I'm shine.

I'm a person who loves the web. I try to make the web better in the little ways I can.

<div>
	{% for post in site.posts %}
		<h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
			{{ post.excerpt }}
	{% endfor %}
</div>
