---
layout: home
---

<div class="container bs-docs-container index-content">
    <div class="row">
        <div class="col-md-9">
            <ul class="artical-list">
            {% for post in site.categories.blog %}
                <li>
                    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
                    <div class="title-desc">{{ post.description }}</div>
                </li>
            {% endfor %}
            </ul>
        </div>
        <div class="col-md-3">
	    <div class="bs-docs-sidebar hidden-print hidden-xs hidden-sm affix">
		
	    </div>     
        </div>
    </div>
</div>
