---
title: "（译）Hugo 的全文 RSS"
date: 2019-08-01T08:00:00+08:00
author: "Junian Triajianto, Hilton Chain（译）"
---

刚开始使用 Hugo 的时候，我发现它有一个很叫人不爽的默认设定：生成的 RSS 订阅源里只有文章的标题和部分文章（变量 `Summary` , 或者说 `!--more--` 标签标记之前的内容），这样可能会造成一些不便。~~而我又因为完全没理解 Hugo 的工作原理不知道该怎么办。~~

所幸有[这篇文章](https://www.godo.dev/tutorials/hugo-full-text-rss/)(或者说下文的原文)帮助我~~渡过难关。~~

## 许可证相关
原文使用 [CC-BY 4.0](http://creativecommons.org/licenses/by/4.0/) 授权，代码部分使用 [MIT许可证](https://www.godo.dev/p/about.html#mit-license)；我在这里的译文则使用 [CC-BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)，代码部分仍然是 MIT许可证。

## 正文
在我的博客之旅中，我不时会把博文同步到其它站点，这些站点之一便是 [CodeProject](https://codeproject.com/)。我得想这些站点提交 RSS 订阅源并在其中加上一个链接标签，之后他们便会拉取带有这个标签的博文。

然而，Hugo 默认只会在 RSS 订阅源中显示文章的”摘要“。因而在我的博文达到一定长度的时候，它并不会包括整篇文章。~~这可真叫人头疼。~~

其实这也并不是什么大问题啦，很简单就可以解决的。

首先，我们需要创建一个 RSS 订阅源的模板，据 Hugo 的文档所述，我们只需要把这个模板文件放到 `/layouts/_default/rss.xml` 即可。

其次，从 Hugo 的网站上拷贝一份[默认的 RSS 模板](https://gohugo.io/templates/rss/#the-embedded-rss-xml)写到里边，下面这些代码也便是 Hugo 提供的默认 RSS 模板。
``` rss
<rss version="2.0" xmlns:atom="http://www.w3.org/2005/Atom">
  <channel>
    <title>{{ if eq  .Title  .Site.Title }}{{ .Site.Title }}{{ else }}{{ with .Title }}{{.}} on {{ end }}{{ .Site.Title }}{{ end }}</title>
    <link>{{ .Permalink }}</link>
    <description>Recent content {{ if ne  .Title  .Site.Title }}{{ with .Title }}in {{.}} {{ end }}{{ end }}on {{ .Site.Title }}</description>
    <generator>Hugo -- gohugo.io</generator>{{ with .Site.LanguageCode }}
    <language>{{.}}</language>{{end}}{{ with .Site.Author.email }}
    <managingEditor>{{.}}{{ with $.Site.Author.name }} ({{.}}){{end}}</managingEditor>{{end}}{{ with .Site.Author.email }}
    <webMaster>{{.}}{{ with $.Site.Author.name }} ({{.}}){{end}}</webMaster>{{end}}{{ with .Site.Copyright }}
    <copyright>{{.}}</copyright>{{end}}{{ if not .Date.IsZero }}
    <lastBuildDate>{{ .Date.Format "Mon, 02 Jan 2006 15:04:05 -0700" | safeHTML }}</lastBuildDate>{{ end }}
    {{ with .OutputFormats.Get "RSS" }}
        {{ printf "<atom:link href=%q rel=\"self\" type=%q />" .Permalink .MediaType | safeHTML }}
    {{ end }}
    {{ range .Pages }}
    <item>
      <title>{{ .Title }}</title>
      <link>{{ .Permalink }}</link>
      <pubDate>{{ .Date.Format "Mon, 02 Jan 2006 15:04:05 -0700" | safeHTML }}</pubDate>
      {{ with .Site.Author.email }}<author>{{.}}{{ with $.Site.Author.name }} ({{.}}){{end}}</author>{{end}}
      <guid>{{ .Permalink }}</guid>
      <description>{{ .Summary | html }}</description>
    </item>
    {{ end }}
  </channel>
</rss>
```

最后，再找到 `<description>` 标签（是 `<item>` 标签的子标签！），可见其默认状态下标记的内容是 `.Summary`。

``` rss
<description>{{ .Summary | html }}</description>
```

现在我们只需要把它替换成 `.Content`。

``` rss
<description>{{- .Content | html -}}</description>
```

好了！现在你的 Hugo 站点就可以在 RSS 订阅源中显示完整内容了~

下面是最终的 `rss.xml` 文件，这是为伸手党准备的。~~自然包括译者了~~

``` rss
<rss version="2.0" xmlns:atom="http://www.w3.org/2005/Atom">
  <channel>
    <title>{{ if eq  .Title  .Site.Title }}{{ .Site.Title }}{{ else }}{{ with .Title }}{{.}} on {{ end }}{{ .Site.Title }}{{ end }}</title>
    <link>{{ .Permalink }}</link>
    <description>Recent content {{ if ne  .Title  .Site.Title }}{{ with .Title }}in {{.}} {{ end }}{{ end }}on {{ .Site.Title }}</description>
    <generator>Hugo -- gohugo.io</generator>{{ with .Site.LanguageCode }}
    <language>{{.}}</language>{{end}}{{ with .Site.Author.email }}
    <managingEditor>{{.}}{{ with $.Site.Author.name }} ({{.}}){{end}}</managingEditor>{{end}}{{ with .Site.Author.email }}
    <webMaster>{{.}}{{ with $.Site.Author.name }} ({{.}}){{end}}</webMaster>{{end}}{{ with .Site.Copyright }}
    <copyright>{{.}}</copyright>{{end}}{{ if not .Date.IsZero }}
    <lastBuildDate>{{ .Date.Format "Mon, 02 Jan 2006 15:04:05 -0700" | safeHTML }}</lastBuildDate>{{ end }}
    {{ with .OutputFormats.Get "RSS" }}
        {{ printf "<atom:link href=%q rel=\"self\" type=%q />" .Permalink .MediaType | safeHTML }}
    {{ end }}
    {{ range .Pages }}
    <item>
      <title>{{ .Title }}</title>
      <link>{{ .Permalink }}</link>
      <pubDate>{{ .Date.Format "Mon, 02 Jan 2006 15:04:05 -0700" | safeHTML }}</pubDate>
      {{ with .Site.Author.email }}<author>{{.}}{{ with $.Site.Author.name }} ({{.}}){{end}}</author>{{end}}
      <guid>{{ .Permalink }}</guid>
      <description>{{- .Content | html -}}</description>
    </item>
    {{ end }}
  </channel>
</rss>
```

下次我会写更多 Hugo 方面的 hack 的！~~可不是我！~~

## 参考
* [Full-text RSS feed](https://discourse.gohugo.io/t/full-text-rss-feed/8368/3) - Hugo Discussion
