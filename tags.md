---
layout: page
title: 标签
permalink: /tags/
---

{%- assign date_format = site.minima.date_format | default: "%Y-%m-%d" -%}
{%- assign sorted_tags = site.tags | sort -%}

{%- if sorted_tags.size > 0 -%}
  <p>共 {{ sorted_tags | size }} 个标签。</p>

  <ul class="tag-cloud">
    {%- for tag in sorted_tags -%}
      {%- assign tag_name = tag[0] -%}
      {%- assign tag_posts = tag[1] -%}
      <li>
        <a href="#{{ tag_name | slugify }}">#{{ tag_name }}</a>
        <span>({{ tag_posts | size }})</span>
      </li>
    {%- endfor -%}
  </ul>

  {%- for tag in sorted_tags -%}
    {%- assign tag_name = tag[0] -%}
    {%- assign tag_posts = tag[1] -%}
    <section class="tag-section" id="{{ tag_name | slugify }}">
      <h2>#{{ tag_name }}</h2>
      <ul class="tag-posts">
        {%- for post in tag_posts -%}
          <li>
            <span class="post-meta">{{ post.date | date: date_format }}</span>
            <a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a>
          </li>
        {%- endfor -%}
      </ul>
    </section>
  {%- endfor -%}
{%- else -%}
  <p>当前还没有可显示的标签。你可以在文章 Front Matter 中添加，例如：<code>tags: [jekyll, minima]</code>。</p>
{%- endif -%}
