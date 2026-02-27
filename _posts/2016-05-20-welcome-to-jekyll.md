---
layout: post
tags: [jekyll, quickstart]
---
你会在 `_posts` 目录中找到这篇文章。现在就可以编辑它并重新构建站点来查看变化。构建站点有很多方式，最常见的是运行 `jekyll serve`，它会启动一个 Web 服务器，并在文件更新时自动重新生成站点。

要添加新文章，只需在 `_posts` 目录下新增一个遵循 `YYYY-MM-DD-name-of-post.ext` 命名规范的文件，并包含必要的 front matter。你可以查看这篇文章的源码，了解其工作方式。

Jekyll 也对代码片段提供了强大支持：

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

更多信息请查看 [Jekyll 文档][jekyll-docs]，了解如何更好地使用 Jekyll。Bug 或功能请求请提交到 [Jekyll 的 GitHub 仓库][jekyll-gh]。如果你有问题，也可以在 [Jekyll Talk][jekyll-talk] 提问。

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
