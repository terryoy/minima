# minima

*Minima 是一款通用型 Jekyll 写作主题*。它是 Jekyll 的默认（也是第一个）主题。执行 `jekyll new` 时得到的就是它。

***免责声明：** 此处信息会因你使用的版本不同而有所差异。请优先参考主题 gem 包中自带的 `README.md`，或在浏览器中打开与你版本对应的 Git 标签，例如：https://github.com/jekyll/minima/blob/v2.5.0/README.md*  
*运行 `bundle show minima` 可查看你当前主题版本在本地的路径。*

[主题预览](https://jekyll.github.io/minima/)

![minima theme preview](/screenshot.png)

## 安装

在你的 Jekyll 站点 `Gemfile` 中添加：

```ruby
gem "minima"
```

然后执行：

    $ bundle


## 内容速览

Minima 由 `jekyll new-theme` 命令脚手架生成，因此具备零配置启动一个新 Jekyll 站点所需的全部文件和目录。

### 布局（Layouts）

指 `_layouts` 目录下定义主题标记结构的文件。

  - `default.html` &mdash; 基础布局，为其他布局打底。派生布局通过 `{{ content }}` 注入内容，并通过 [FrontMatter](https://jekyllrb.com/docs/frontmatter/) 中 `layout: default` 关联到该布局。
  - `home.html` &mdash; 落地页 / 首页 / 索引页布局。[[更多信息。](#home-layout)]
  - `page.html` &mdash; 适用于包含 FrontMatter 但不是文章（post）的文档。
  - `post.html` &mdash; 文章布局。

#### Home Layout

`home.html` 是一个灵活的 HTML 布局，用于站点落地页 / 首页 / 索引页。<br/>

##### *主标题与内容注入*

从 Minima v2.2 开始，*home* 布局会在 **`Posts`** 标题**之前**注入 `index.md` / `index.html` 的全部内容。这使你可以在首页专门区域发布与文章列表无关的内容。*建议将该区域标题设为二级标题（`##`）。*

通常 `site.title` 已可作为首页的隐式主标题。但如果你希望显式显示首页标题，只需在文档 front matter 中定义 `title` 变量，它会以 `<h1>` 渲染。

##### *文章列表*

从 Minima v2.2 起，该部分为可选。<br/>
仅当站点存在一篇或多篇有效文章（或启用 `show_drafts` 时存在草稿）时才会自动显示。

该部分默认标题为 `Posts`，并以 `<h2>` 渲染。你可以在文档 front matter 中定义 `list_title` 来自定义该标题。


### Includes

指 `_includes` 目录中的代码片段，可在同一主题 gem 的多个布局（甚至其他 include 文件）中复用。

  - `disqus_comments.html` &mdash; Disqus 评论框标记代码。
  - `footer.html` &mdash; 站点页脚区域定义。
  - `google-analytics.html` &mdash; 插入 Google Analytics 模块（仅生产环境生效）。
  - `head.html` &mdash; 在 *default* 布局中定义 `<head></head>` 的代码块。
  - `header.html` &mdash; 站点主头部区域定义。默认会显示具有 `title` 属性页面的链接。
  - `social.html` &mdash; 根据配置文件中的 `minima:social_links` 数据渲染社交媒体图标。


### Sass

指 `_sass` 目录中定义主题样式的 `.scss` 文件。

  - `minima-classic.scss` &mdash; 被预处理文件 `css/style.scss` 导入的核心文件，定义主题“classic”皮肤的变量默认值。
  - `minima/initialize.scss` &mdash; 定义主题与皮肤无关（*skin-agnostic*）的变量默认值和 sass partial。
  - `minima/custom-variables.scss` &mdash; 用于覆盖变量默认值和 mixin 的钩子。(*注意：不能覆盖样式*)
  - `minima/custom-styles.scss` &mdash; 用于覆盖样式的钩子。(*注意：不能覆盖变量*)
  - `minima/_base.scss` &mdash; reset 与基础 HTML 元素样式定义的 Sass partial。
  - `minima/_layout.scss` &mdash; 各种布局视觉样式定义的 Sass partial。

更多信息见 [skins](#skins) 章节。


### Assets

指 `assets` 目录下的各类资源文件。
其中包含 `css/style.scss`，它会导入 `_sass` 目录中的 sass 文件。这个 `css/style.scss` 会被处理为主题主样式表 `main.css`，并由 `_layouts/default.html` 通过 `_includes/head.html` 引用。

该目录可包含用于管理同类资源的子目录（如 `img`、`fonts`、`svg`），并会原样复制到最终生成的网站目录。


### 插件（Plugins）

Minima 预装了 [`jekyll-seo-tag`](https://github.com/jekyll/jekyll-seo-tag) 插件，以确保你的网站拥有更有用的元标签。请参考其 [usage](https://github.com/jekyll/jekyll-seo-tag#usage) 了解配置方法。


## 使用

在配置文件中包含以下配置：

```yaml
theme: minima
```


### 自定义模板

若要覆盖 minima 默认结构与样式，只需在站点根目录创建对应目录，将你要自定义的文件复制到该目录后进行编辑。
例如，要覆盖 [`_includes/head.html `](_includes/head.html) 以指定自定义样式路径，可创建 `_includes` 目录，将 minima gem 中的 `_includes/head.html` 复制到 `<yoursite>/_includes`，然后开始修改。

站点默认 CSS 现在已移动到 gem 内部新位置：[`assets/css/style.scss`](assets/css/style.scss)。

在 Minima 3.0 中，如果你只需自定义主题颜色，请参考下一节 skins。为了让你的 *CSS 覆盖* 与未来上游版本改动保持同步，你可以把 Sass 变量和 mixin 的覆盖集中放在 `_sass/minima/custom-variables.scss`，其他样式覆盖放在 `_sass/minima/custom.scss`。

无需为了覆盖少量样式而维护整个 partial 文件。

#### Skins

Minima 3.0 支持定义并切换多套配色（或称 *skins*）。

```
.
├── minima.scss
└── minima
    └── _syntax-highlighting.scss
```


皮肤文件是一个命名为 `minima-*` 的 Sass 文件，由 `assets/css/style.scss` 导入。它定义主题与“颜色”相关的变量默认值，并导入两个组件：

  - `minima/initialize.scss` &mdash; 定义主题与皮肤无关的变量默认值和样式 partial。
  - `minima/custom-styles.scss` &mdash; 用于覆盖预定义样式的钩子。(*注意：不能覆盖变量*)

皮肤文件也会内嵌语法高亮相关 Sass 规则，因为这部分主要与颜色相关，需要与当前皮肤协调。

Minima 的默认配色定义在 `_sass/minima-classic.scss`。如需切换到其他可用皮肤，只需在站点配置文件中声明。例如，启用 `_sass/minima-sunrise.scss` 的配置如下：

```yaml
minima:
  skin: sunrise
```

为支持 skins 迁移，部分旧 Sass 变量已弃用，部分变量被**重新定义**，如下表所示：

Minima 2.0      | Minima 3.0
--------------- | ----------
`$brand-color`  | `$link-base-color`
`$grey-*`       | `$brand-*`
`$orange-color` | *已移除*


### 自定义导航链接

可设置你希望显示在导航区域的页面，并配置链接顺序。

例如，只链接到 `about` 与 `portfolio` 页面时，在 `_config.yml` 中添加：

```yaml
header_pages:
  - about.md
  - portfolio.md
```


### 修改默认日期格式

你可以在 `_config.yml` 中通过 `site.minima.date_format` 修改默认日期格式。

```
# Minima 日期格式
# 如需自定义，可参考 http://shopify.github.io/liquid/filters/date/
minima:
  date_format: "%b %-d, %Y"
```


### 添加你自己的 favicon

1. 访问 [https://realfavicongenerator.net/](https://realfavicongenerator.net/) 生成你的 favicon。
2. 在源码目录中 [Customize](#customization) 默认 `_includes/favicons.html`，并插入生成的代码片段。


### 启用评论（Disqus）

可选地，如果你有 Disqus 账号，可以让 Jekyll 在每篇文章下显示评论区。

启用方式：在 Jekyll 站点配置中添加：

```yaml
  disqus:
    shortname: my_disqus_shortname
```

你可以在 [这里](https://help.disqus.com/installation/whats-a-shortname) 了解更多 Disqus shortname。

评论默认启用，但仅在生产环境显示，即 `JEKYLL_ENV=production`。

如果你不希望某篇文章显示评论，可在该文章 YAML Front Matter 中添加 `comments: false`。

:warning: 要让 Disqus 生效，配置文件中必须设置 `url`（如 `https://example.com`）。

### 作者元数据

从 `Minima-3.0` 开始，`site.author` 期望是属性映射（mapping），而不是简单标量值：

```yaml
author:
  name: John Smith
  email: "john.smith@foobar.com"
```

迁移已有元数据时，请更新配置文件及布局/include 中对该对象的引用，示例如下：

Minima 2.x    | Minima 3.0
------------- | -------------------
`site.author` | `site.author.name`
`site.email`  | `site.author.email`


### 社交网络

你可以在配置中添加以下一个或多个选项，为其他站点账号生成对应图标链接。
从 `Minima-3.0` 开始，用户名需放在 `minima.social_links` 下，键名直接使用社交网络名称：

```yaml
minima:
  social_links:
    twitter: jekyllrb
    github: jekyll
    stackoverflow: "11111"
    dribbble: jekyll
    facebook: jekyll
    flickr: jekyll
    instagram: jekyll
    linkedin: jekyll
    pinterest: jekyll
    telegram: jekyll
    microdotblog: jekyll
    keybase: jekyll
    rss: rss

    mastodon:
     - username: jekyll
       instance: example.com
     - username: jekyll2
       instance: example.com

    gitlab:
     - username: jekyll
       instance: example.com
     - username: jekyll2
       instance: example.com

    youtube: jekyll
    youtube_channel: UC8CXR0-3I70i1tfPg1PAE1g
    youtube_channel_name: CloudCannon
```


### 启用 Google Analytics

在 Jekyll 站点配置中添加：

```yaml
  google_analytics: UA-NNNNNNNN-N
```

Google Analytics 仅会在生产环境显示，即 `JEKYLL_ENV=production`。

### 在首页启用摘要（Excerpts）

若要在首页显示文章摘要，在 `_config.yml` 中添加：

```yaml
show_excerpts: true
```


## 参与贡献

欢迎在 GitHub 提交 Bug 报告和 Pull Request：https://github.com/jekyll/minima。该项目致力于提供安全、友好的协作环境，贡献者应遵守 [Contributor Covenant](http://contributor-covenant.org) 行为准则。

## 开发

要搭建此主题的开发环境，请运行 `script/bootstrap`。

要测试主题，请运行 `script/server`（或 `bundle exec jekyll serve`），并在浏览器打开 `http://localhost:4000`。这会启动使用当前主题与内容的 Jekyll 服务。你修改文件后站点会重新生成，刷新浏览器即可看到变化。

## 许可证

该主题以开源方式发布，遵循 [MIT License](http://opensource.org/licenses/MIT) 条款。
