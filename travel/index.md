--- 
layout: container-template 
---

<div class="row">
    <div class="col-md-8">
        <div class="panel panel-default shadow1">
            <div class="posts-list">
                {% for post in paginator.posts %}
                <article class="postPreviewBox">
                    <a href="{{ post.url | prepend: site.baseurl }}">
                    <h2 class="postTitle">{{ post.title }}</h2> 
                {% if post.subtitle %}
                <h3 class="postSubTitle">
                    {{ post.subtitle }}
                </h3> 
            {% endif %}
        </a>

        <p class="postMeta">
            Posted on {{ post.date | date: "%B %-d, %Y" }}
        </p>

        <div class="postPreviewContent">
            {{ post.content | truncatewords: 50 | strip_html | xml_escape}}
            <br/><br/>
            <a href="{{ post.url | prepend: site.baseurl }}" class="readMoreLink">&raquo; [Read&nbsp;More]</a>
        </div>

                </article>
            {% endfor %}
            </div>
        </div>
    </div>

    <div class="col-md-4">
        <div class="panel panel-default">
            <div class="panel-heading">
                <span class="text-primary"><b>Recent Posts</b></span>
            </div>
            <div class="panel-body">
                <ul>
                    {% for post in site.posts offset: 0 limit: 5  %}
                        <li>
                            <a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
                        </li>
                    {% endfor %}
                </ul>
            </div>
        </div>

        <div class="panel panel-default">
            <div class="panel-heading">
                <span class="text-primary"><b>Blog Categories</b></span>
            </div>
            <div class="panel-body">
                <div class="panel-group" id="accordion">
                    {% for category in site.categories %}
                    <div class="panel panel-default">
                        <div class="panel-heading">
                            <h4 class="panel-title">
                                <a data-toggle="collapse" data-parent="#accordion" name="{{ category | first }}" 
                                   href="#{{ category | first }}">
                                    {{ category | first }}
                                </a>
                            </h4>
                        </div>
                        
                        {% if forloop.index == 1 %}
                        <div id="{{ category | first }}" class="panel-collapse collapse in">
                            <div class="panel-body">
                                <ul>
                                    {% for posts in category %} {% for post in posts %}
                                    <li><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></li>
                                    {% endfor %} {% endfor %}
                                </ul>
                            </div>
                        </div>
                        {% else %}
                        <div id="{{ category | first }}" class="panel-collapse collapse">
                            <div class="panel-body">
                                <ul>
                                    {% for posts in category %} {% for post in posts %}
                                    <li><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></li>
                                    {% endfor %} {% endfor %}
                                </ul>
                            </div>
                        </div>
                        {% endif %}                       
                        
                    </div>
                    {% endfor %}
                </div>
            </div>
        </div>
        
        
    </div>
</div>



{% if paginator.total_pages > 1 %}
    <ul class="pager main-pager">
        {% if paginator.previous_page %}
            <li class="previous">
                <a href="{{ paginator.previous_page_path | prepend: site.baseurl | replace: '//', '/' }}">&larr; Newer Posts</a>
            </li>
        {% endif %} 
        {% if paginator.next_page %}
            <li class="next">
                <a href="{{ paginator.next_page_path | prepend: site.baseurl | replace: '//', '/' }}">Older Posts &rarr;</a>
            </li>
        {% endif %}
    </ul>
{% endif %}
