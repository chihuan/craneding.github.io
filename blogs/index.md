---
layout: default
---

<div tabindex="-1" id="content" class="bs-docs-header">
    <div class="container">
        <h1>博客</h1>

        <p>没错，这满满都是技术类的文章。把自己看到的、学到的都记录下来，也是自己一本不错的备忘录!</p>
    </div>
</div>

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
