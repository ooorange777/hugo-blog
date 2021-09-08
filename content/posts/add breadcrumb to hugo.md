---
title: "Add breadcrumb to hugo"
date: 2021-05-08T12:41:07+08:00
slug: 2021050801
draft: false
tags:
- hugo
isCJKLanguage: true
---

在为`hugo`站点选主题的时候，一眼看中了*hello-friend-ng*，非常喜欢主题的**logo设计**，有种打开console等待输入的感觉。看Demo的时候我以为这就是面包屑导航，结果发现并不是，感觉有点可惜，于是想着自己改一改吧。

就是我这个菜鸡的水平不够，自定义`CSS`结果路径怎么设置都不对，只能直接和`HTML`丢在一起了。

下面就开始吧！

1. 在`主题目录/layouts/partials`下新增一个*breadcrumb.html*

2. 编辑`breadcrumb.html`，代码如下：

   ```html
   <div  class="breadcrumb">
     {{ template "breadcrumbnav" (dict "p1" . "p2" .) }}
   </div>
   {{ define "breadcrumbnav" }}
   {{ if .p1.Parent }}
     {{ template "breadcrumbnav" (dict "p1" .p1.Parent "p2" .p2 )  }}
   {{ else if not .p1.IsHome }}
     {{ template "breadcrumbnav" (dict "p1" .p1.Site.Home "p2" .p2 )  }}
   {{ end }}
   <li{{ if eq .p1 .p2 }} class="active"{{ end }}>
     <a href="{{ .p1.Permalink }}">{{ .p1.Title }}</a>
   </li>
   {{ end }}
   ```

3. 新增`style.css`，具体放在哪里我也不知道，所以我的做法是加入`breadcrumb.html`中，代码如下：

   ```css
   /* breadcrumb */
   .breadcrumb {
       background: #fafafa;
       padding: 4px 15px;
       margin-bottom: 40px;
       list-style: none;
       border-radius: 5px; 
   }
   .breadcrumb>li{
       display: inline-block; 
       opacity: .7;
   }
   .breadcrumb>li+li:before {
       padding: 0 5px; 
       color: #ccc; 
       content: ">"; 
   }
   .breadcrumb li a{text-decoration:none;}
   .dark-theme .breadcrumb {background: #252627;}
   ```

   我调整过的代码如下：

   ```css
   /* breadcrumb */
   .breadcrumb {list-style:none;}
   .breadcrumb li{display:inline-block;font-display: auto;}
   .breadcrumb li+li ::before{padding:0px 0px; content:"/";}
   .breadcrumb li a{text-decoration:none;}
   ```

4. 完成以上步骤后，我们就获得一个*面包屑导航*插件了，可以插入你需要的页面。使用方式，在你需要的页面中，适合的地方插入`{{ partial "breadcrumb.html" . }}`。一般需要导航条的页面有*single.html*和*list.html*

5. 鉴于我自己的需要，我将面包屑导航插入`logo.html`。经过反复试验，插在`<span class="logo__text">`和`<span class="logo__cursor">`中间。

   ```css
   <span class="logo__text">{{ with .Site.Params.Logo.logoText }}{{ . }}{{ else }}hello{{ end }}</span>
   <span class="breadcrumb">{{ partial "breadcrumb.html" . }}</span>
   <span class="logo__cursor" style=
   ```

6. 具体效果请看本站。

---

**参考**

[Hugo 添加面包屑导航](https://immmmm.com/hugo-add-breadcrumb/)