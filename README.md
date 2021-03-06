# HEAD

[![CC0](https://img.shields.io/badge/license-CC0-green.svg)](https://creativecommons.org/publicdomain/zero/1.0/)
[![Contributors](https://img.shields.io/github/contributors/joshbuchea/head.svg)](https://github.com/joshbuchea/HEAD/graphs/contributors)

一份关于任何 **可以** 写入到你的文档中 `<head>` 部分的清单。

## 目录

- [最小推荐](#最小推荐)
- [网页元素](#网页元素)
- [HTML 文档之 Head 最佳实践](#HTML-文档之-Head-最佳实践)
- [Meta 标签](#meta-标签)
  - [基本常用](#基本常用)
  - [SEO优化](#SEO优化)
  - [移动设备](#移动设备)
  - [网页相关](#网页相关)
  - [其他](#其他)
- [Link 链接](#Link-链接)
- [JS 链接](#JS-链接)
- [网站图标](#网站图标)
- [社交](#社交)
  - [Facebook Open Graph](#facebook-open-graph)
  - [Twitter Card](#twitter-card)
  - [Twitter Privacy](#twitter-privacy)
  - [Google+ / Schema.org](#google--schemaorg)
  - [Pinterest](#pinterest)
  - [Facebook Instant Articles](#facebook-instant-articles)
  - [OEmbed](#oembed)
- [浏览器 / 平台](#浏览器--平台)
  - [Apple iOS](#apple-ios)
  - [Google Android](#google-android)
  - [Google Chrome](#google-chrome)
  - [Microsoft Internet Explorer](#microsoft-internet-explorer)
- [国内的浏览器](#国内的浏览器)
  - [360 浏览器](#360-浏览器)
  - [QQ 移动浏览器](#qq-移动浏览器)
  - [UC 移动浏览器](#uc-移动浏览器)
- [应用链接](#应用链接)
- [其他资源](#其他资源)
- [相关项目](#相关项目)
- [其他格式](#其他格式)
- [翻译](#翻译)
- [贡献](#贡献)
  - [贡献者](#贡献者)
- [作者](#作者)
- [参考资料](#参考资料)
- [许可](#许可)

## 最小推荐

以下是构成任何 Web 页面（网站/应用程序）的基本要素：

```html
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<!--
  以上 2 个 meta 标签 *必须* 放在 <head> 标签内 最前面，以确保正确的文档呈现；
  其他任何 head 元素 *必须* 在这些标签之后。
-->
<title>页面标题</title>
```

**[⬆ 返回顶部](#目录)**

## 网页元素

有效的 `<head>` 元素包括 `meta`、`link`、`title`、`style`、`script`、`noscript` 和 `base`。

这些元素提供了如何通过如浏览器，搜索引擎，网络爬虫等网络技术来感知和呈现文档的信息。

```html
<!-- 设置此文档的字符编码，以便 UTF-8 范围中的所有字符（如 emoji）都能正确显示 -->
<meta charset="utf-8">

<!-- 设置文档标题 -->
<title>页面标题</title>

<!-- 设置文档中所有相对链接的基础链接 -->
<base href="https://example.com/page.html">

<!-- 链接一个外部 CSS 文件 -->
<link rel="stylesheet" href="styles.css">

<!-- 用于文档内的 CSS -->
<style>
  /* ... */
</style>

<!-- JavaScript & No-JavaScript 标签 -->
<script>
  // function(s) go here
</script>
<noscript>
  <!--无 JS 时显示-->
</noscript>
```

**[⬆ 返回顶部](#目录)**


## HTML 文档之 Head 最佳实践

#### 语言

在 `html` 标签中通过 `lang` 属性进行明确的语言声明，将会有助于翻译，英文、简体中文和繁体中文网页所属性值如下：

```html
<html lang="en">
<html lang="zh-Hans">
<html lang="zh-Hant">
```

#### 编码

请在 `<head>` 中第一行统一使用 `utf-8` 编码声明。

```html
<meta charset="utf-8">
```

#### Base 元素

尽量不使用 `<base>` 元素，绝对地址和 URL 对于开发者和用户来说都更好。

```html
<!-- Bad -->
<base href="/blog/">
<link href="hello-world" rel="canonical">

<!-- Good -->
<link href="/blog/hello-world" rel="canonical">
```

#### Viewport

设置 `viewport` 的宽度为设备宽度，默认缩放比为 1（允许用户缩放），设置 `viewport-fit=cover` 以兼容 iPhone X 全面屏“刘海”的显示。

```html
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
```

#### DNS 预读取

DNS 预读取是一项使浏览器主动去执行域名解析的功能，其范围包括当前文档内的所有链接，这能够减少用户点击链接时的延迟。

```html
<meta http-equiv="x-dns-prefetch-control" content="on">
<link rel="dns-prefetch" href="//www.google-analytics.com">
<link rel="dns-prefetch" href="//fonts.googleapis.com">
```

#### 预加载

指示浏览器预先请求当前页面所需要的关键性资源。

```html
<link rel="preload" href="/css/main.css" as="style">
<link rel="preload" href="/js/main.js" as="script">
```

#### 预请求

指示浏览器预先请求用户即将浏览页面所需要的关键性资源。

```html
<link rel="prefetch" href="/img/css-sprite.png">
<link rel="prefetch" href="/fonts/icons.woff2">
```

#### 渲染偏好

对于国内各种双核浏览器，通过设置 `renderer` 头要求它们使用 webkit 内核；对于 IE 浏览器，通过设置 `IE=edge` 要求它使用最新的版本；对于百度搜索强制转码的流氓做法，通过 `no-transform` 禁止其自动转码；指示浏览器对类似电话、邮箱或地址的内容不要自作聪明的瞎识别（移动端）。

```html
<meta name="renderer" content="webkit"> <!-- 用在360中 -->
<meta name="force-rendering" content="webkit"> <!-- 用在其它 -->
<meta http-equiv="X-UA-Compatible" content="IE=edge"> <!-- 针对 IE 浏览器 -->
<meta http-equiv="Cache-Control" content="no-transform"> <!-- 针对百度搜索 -->
<meta name="format-detection" content="telephone=no,email=no,adress=no">
```

#### 文档信息

HTML 文档的一些元数据，包括：作者、描述、关键词和生成工具；设置 `robots` 为 `index,follow` 指示搜索引擎爬虫该页面需要进入索引，并且页面内的所有链接都要继续跟踪；设置 `referrer` 为 `origin-when-cross-origin` 指示浏览器在进行跨域跳转时，其 `referrer` 值将统一为域名，而非具体的 URL 地址。

```html
<meta name="author" content="米老朱">
<meta name="description" content="米老朱的个人博客">
<meta name="keywords" content="米老朱,极客,博客,WEB,开发,产品设计">
<meta name="generator" content="Hugo 0.32">
<meta name="robots" content="index,follow">
<meta name="referrer" content="origin-when-cross-origin">
```

#### Icons

虽说所有浏览器都还支持过时的 favicon.ico 格式，但在 HTML5 时代，我们应该使用更好的 PNG icon with sizes 方案。同时为了兼容老旧浏览器，我们可以将生成好的 favicon.ico 文件放在网站的根目录下面，通常浏览器会自动请求并加载它，并不需要额外通过 link 标签引入。

```html
<meta name="theme-color" content="#db5945"> <!-- 主题颜色 -->
<meta name="application-name" content="米老朱的博客"> <!-- 应用名称 -->
<meta name="apple-mobile-web-app-capable" content="yes"> <!-- 隐藏状态栏 -->
<meta name="apple-mobile-web-app-status-bar-style" content="black"> <!-- 状态栏颜色 -->
<meta name="apple-mobile-web-app-title" content="米老朱的博客"> <!-- iOS 下的应用名称 -->
<meta name="msapplication-tooltip" content="米老朱的博客"> <!-- Hover 的提示信息 -->
<meta name="msapplication-TileColor" content="#db5945"> <!-- 磁贴背景颜色 -->
<meta name="msapplication-TileImage" content="/img/logo-144.png"> <!-- 磁贴图标 -->
<meta name="msapplication-config" content="/browserconfig.xml"> <!-- 磁贴配置文件 -->
<link rel="icon" type="image/png" href="/img/logo-16.png" sizes="16x16"> <!-- Browser Favicon -->
<link rel="icon" type="image/png" href="/img/logo-32.png" sizes="32x32"> <!-- Taskbar Shortcut -->
<link rel="icon" type="image/png" href="/img/logo-96.png" sizes="96x96"> <!-- Desktop Shortcut -->
<link rel="icon" type="image/png" href="/img/logo-128.png" sizes="128x128"> <!-- Chrome Web Store -->
<link rel="icon" type="image/png" href="/img/logo-196.png" sizes="196x196"> <!-- Chrome for Android Home Screen -->
<link rel="icon" type="image/png" href="/img/logo-228.png" sizes="228x228"> <!-- Opera Coast Icon -->
<link rel="apple-touch-icon" href="/img/logo-120.png"> <!-- iPhone -->
<link rel="apple-touch-icon" href="/img/logo-152.png" sizes="152x152"> <!-- iPad -->
<link rel="apple-touch-icon" href="/img/logo-180.png" sizes="180x180"> <!-- iPhone Plus -->
<link rel="apple-touch-icon" href="/img/logo-167.png" sizes="167x167"> <!-- iPad Pro -->
<link rel="mask-icon" href="/img/logo.svg" color="green"> <!-- Safari Pinned Tab Icon -->
```

微软为了让 Metro UI 更好看，引入了 `browserconfig.xml` 文件，主要用于定制网站固定磁铁的图标和背景颜色，其格式如下所示：

```xml
<?xml version="1.0" encoding="utf-8"?>
<browserconfig>
   <msapplication>
     <tile>
        <square70x70logo src="/img/logo-70.png"/>
        <square150x150logo src="/img/logo-150.png"/>
        <wide310x150logo src="/img/logo-310x150.png"/>
        <square310x310logo src="/img/logo-310.png"/>
        <TileImage src="/img/logo-144.png"/>
        <TileColor>#db5945</TileColor>
     </tile>
   </msapplication>
</browserconfig>
```

favicon.ico 实际上是一个图片容器，里面至少应该包含 16x16，32x32，48x48 三个尺寸的 png 图片，我们可以使用 [ImageMagick](https://github.com/ImageMagick/ImageMagick) 工具在本地直接生成（生成之前需要对 png 图片进行压缩以减小尺寸）。

```bash
$ convert favicon-16.png favicon-32.png favicon-48.png favicon.ico
```

*注意：apple-mobile-web-app-status-bar-style 值默认状态栏为白色，可设置为 black（黑色） 或者 black-translucent（灰色半透明）；mask-icon 引入的 svg 文件必须只有一个图层，并且 `viewBox` 属性应该为 "0 0 16 16"。*

#### Twitter Cards

Twitter 卡片用于将网站内容以更加优雅漂亮的方式分享到 [twitter.com](https://twitter.com/) 网站，从形式上说，分为：summary, summary_large_image, app, player 四种形式，通常我们的站点只需要 summary 这种形式。

```html
<meta name="twitter:card" content="summary">
<meta name="twitter:site" content="@melaozhu">
<meta name="twitter:title" content="此处为分享标题">
<meta name="twitter:description" content="此处为分享描述">
<meta name="twitter:image" content="此处为分享配图">
```

配置上线后，你可以通过这个 [Card validator](https://cards-dev.twitter.com/validator) 工具检查是否正确显示。

#### Facebook Open Graph

[Open Graph](http://ogp.me/) 是一套开放的网页标注协议，通过 meta 标签标注网页的类型，主要由 Facebook 推动，已经成为社交分享领域的事实标准。如果你希望明确告诉社交网络或搜索引擎你的网页类型，你应该添加这些 meta 标签。

```html
<meta property="og:type" content="article">
<meta property="og:title" content="此处为分享标题">
<meta property="og:description" content="此处为分享描述">
<meta property="og:image" content="此处为分享配图">
<meta property="og:url" content="此处为分享的链接地址">
```

#### 固定链接

对于一份文档存在多个 URL 的情况，通过 `rel="canonical"` 指定唯一的固定链接。

```html
<link rel="canonical" href="https://laozhu.me/">
```

#### RSS 链接

对于支持 RSS 订阅的页面，可针对 RSS 阅读器提供可订阅的源文件。

```html
<link rel="alternative" href="/index.xml" title="米老朱的博客" type="application/atom+xml">
```

#### Polyfill

可以专门为老旧的 IE 浏览器引入 Polyfill 方案，举个例子，为了让 IE6-IE8 浏览器能够使用 HTML5 标签和 Media Query 特性，我们需要引入 [html5shiv](https://github.com/aFarkas/html5shiv) 和 [response.js](https://github.com/scottjehl/Respond) 这两个库。

```html
<!--[if lt IE 9]>
<script src="//cdn.bootcss.com/html5shiv/3.7.3/html5shiv.min.js"></script>
<script src="//cdn.bootcss.com/respond.js/1.4.2/respond.min.js"></script>
<![endif]-->
```

其他的 Polyfill 方案写法类似。

#### 打印样式表

对于可打印的页面（如文章页面），可提供针对打印机的样式表，使得网站用户可以将文章打印下来阅读。

```html
<link rel="stylesheet" href="/css/print.css" media="print">
```

#### 交替样式表

定义交替样式表的时候，指定其 `title` 属性，以方便用户在浏览器中根据名称选择替代样式，交替样式表多用于多主题切换的站点。

```html
<link href="default.css" rel="stylesheet">
<link href="high-contrast.css" rel="alternate stylesheet" title="High contrast">
```

#### 参考链接

1. [HTML Best Practices](https://github.com/hail2u/html-best-practices)
2. [Favicon Cheatsheet](https://github.com/audreyr/favicon-cheat-sheet)
3. [DNS 预读取](https://developer.mozilla.org/zh-CN/docs/Controlling_DNS_prefetching)
4. [Prefetching, preloading, prebrowsing](https://css-tricks.com/prefetching-preloading-prebrowsing/)
5. [Favicons, Touch Icons, Tile Icons, etc. Which Do You Need?](https://css-tricks.com/favicon-quiz/)
6. [Here's Everything You Need to Know About Favicons in 2017](https://sympli.io/blog/2017/02/15/heres-everything-you-need-to-know-about-favicons-in-2017/)
7. [Configuring Web Applications](https://developer.apple.com/library/content/documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html)
8. [Creating Pinned Tab Icons](https://developer.apple.com/library/content/documentation/AppleApplications/Reference/SafariWebContent/pinnedTabs/pinnedTabs.html)
9. [“The Notch” and CSS](https://css-tricks.com/the-notch-and-css/)
10. [Alternative style sheets](https://developer.mozilla.org/en-US/docs/Web/CSS/Alternative_style_sheets)

**[⬆ 返回顶部](#目录)**

## Meta 标签

>标签提供关于HTML文档的元数据。元数据不会显示在页面上，但是对于机器是可读的。它可用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他 web 服务。 —— W3School

meta标签共有两个属性，分别是http-equiv属性和name属性，content中的内容是对属性填入类型的具体描述。

name属性主要用于描述网页，比如网页的关键词，叙述等。

http-equiv属性常用来做http协议上的一些限制，其作用是把 content 属性关联到 HTTP 头部。

### 基本常用

```html
<!-- 声明文档使用的字符编码 -->
<meta charset="utf-8">
<!-- 优先使用 IE 最新版本和 Chrome -->
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
<!-- 页面描述 -->
<meta name="description" content="网页描述">
<!-- 页面关键词 -->
<meta name="keywords" content="">
<!-- 网页作者 -->
<meta name="author" content="name, email@gmail.com">
<!-- 为移动设备添加 viewport -->
<meta name="viewport" content="width=device-width, initial-scale=1">
<!-- 启用360浏览器的极速模式(webkit) -->
<meta name="renderer" content="webkit">

<!-- 搜索引擎抓取 -->
<meta name="robots" content="index,follow">
<!-- 不让百度转码 -->
<meta http-equiv="Cache-Control" content="no-siteapp">

<!-- 添加智能 App 广告条 Smart App Banner（iOS 6+ Safari） -->
<meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL">
<!-- 设置苹果工具栏颜色 -->
<meta name="apple-mobile-web-app-status-bar-style" content="black">
<!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
<meta name="HandheldFriendly" content="true">
<!-- 微软的老式浏览器 -->
<meta name="MobileOptimized" content="320">
<!-- uc强制竖屏 -->
<meta name="screen-orientation" content="portrait">
<!-- QQ强制竖屏 -->
<meta name="x5-orientation" content="portrait">
<!-- UC强制全屏 -->
<meta name="full-screen" content="yes">
<!-- QQ强制全屏 -->
<meta name="x5-fullscreen" content="true">
<!-- UC应用模式 -->
<meta name="browsermode" content="application">
<!-- QQ应用模式 -->
<meta name="x5-page-mode" content="app">
<!-- windows phone 点击无高光 -->
<meta name="msapplication-tap-highlight" content="no">
<!-- 设置页面不缓存 -->
<meta http-equiv="pragma" content="no-cache">
<meta http-equiv="cache-control" content="no-cache">
<meta http-equiv="expires" content="0">
```

### SEO优化

```html
<!-- 页面关键词，每个网页应具有描述该网页内容的一组唯一的关键字。标记不应超过 874 个字符。 -->
<meta name="keywords" content="tag1,tag2,tag3">

<!-- 针对页面的简短描述（限制 150 字符）-->
<!-- 此内容*可能*被用作搜索引擎结果的一部分。 -->
<meta name="description" content="150 words">

<!-- 标注网页作者 -->
<meta name="author" content="xxx,xxx@qq.com">

<!-- 标注版权信息 -->
<meta name="copyright" content="Lxxyx">

<!-- 定义搜索引擎的抓取和索引行为 -->
<!--
    robots用来告诉爬虫哪些页面需要索引，哪些页面不需要索引。
    content的参数有all,none,index,noindex,follow,nofollow。默认是all。
    具体参数如下：
    1.none : 搜索引擎将忽略此网页，等价于noindex，nofollow。
    2.noindex : 搜索引擎不索引此网页。
    3.nofollow: 搜索引擎不继续通过此网页的链接索引搜索其它的网页。
    4.all : 搜索引擎将索引此网页与继续通过此网页的链接索引，等价于index，follow。
    5.index : 搜索引擎索引此网页。
    6.follow : 搜索引擎继续通过此网页的链接索引搜索其它的网页。
-->
<meta name="robots" content="none"><!-- 所有搜索引擎 -->
<meta name="googlebot" content="index,follow"><!-- 仅对 Google 有效 -->

<!--
    页面重定向和刷新
    content内的数字代表时间（秒），既多少时间后刷新。
    如果加url,则会重定向到指定网页（搜索引擎能够自动检测，也很容易被引擎视作误导而受到惩罚）。
-->
<meta http-equiv="refresh" content="0;url=">

<!--
    搜索引擎爬虫重访时间
    说明：如果页面不是经常更新，为了减轻搜索引擎爬虫对服务器带来的压力，可以设置一个爬虫的重访时间。
    如果重访时间过短，爬虫将按它们定义的默认时间来访问
-->
<meta name="revisit-after" content="7 days">
```

### 移动设备

```html
<!--
    能优化移动浏览器的显示。
    如果不是响应式网站，不要使用initial-scale或者禁用缩放。
    width：宽度（数值 / device-width）（范围从200 到10,000，默认为980 像素）
    height：高度（数值 / device-height）（范围从223 到10,000）
    initial-scale：初始的缩放比例 （范围从>0 到10）
    minimum-scale：允许用户缩放到的最小比例
    maximum-scale：允许用户缩放到的最大比例
    user-scalable：用户是否可以手动缩 (no,yes)
    minimal-ui：可以在页面加载时最小化上下状态栏。（已弃用）
    注意，很多人使用initial-scale=1到非响应式网站上，这会让网站以100%宽度渲染，用户需要手动移动页面或者缩放。
    如果和initial-scale=1同时使用user-scalable=no或maximum-scale=1，则用户将不能放大/缩小网页来看到全部的内容。
 -->
<meta name="viewport" content="width=device-width, initial-scale=1">

<!-- WebApp全屏模式：伪装app，离线应用。 -->
<meta name="apple-mobile-web-app-capable" content="yes">

<!-- 是否启用 WebApp 全屏模式 -->
<meta name="apple-mobile-web-app-capable" content="yes">

<!--
    隐藏状态栏/设置状态栏颜色
    只有在开启WebApp全屏模式时才生效。
    content的值为default | black | black-translucent 。
-->
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">

<!-- 添加到主屏幕后的标题 -->
<meta name="apple-mobile-web-app-title" content="标题">

<!-- 忽略数字自动识别为电话号码 -->
<meta content="telephone=no" name="format-detection">

<!-- 忽略识别邮箱 -->
<meta content="email=no" name="format-detection">

<!--
    添加智能 App 广告条 Smart App Banner
    在网页上方显示一个app banner，提供app store下载
-->
<meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL">

<!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
<meta name="HandheldFriendly" content="true">
<!-- 微软的老式浏览器 -->
<meta name="MobileOptimized" content="320">
<!-- uc强制竖屏 -->
<meta name="screen-orientation" content="portrait">
<!-- QQ强制竖屏 -->
<meta name="x5-orientation" content="portrait">
<!-- UC强制全屏 -->
<meta name="full-screen" content="yes">
<!-- QQ强制全屏 -->
<meta name="x5-fullscreen" content="true">
<!-- UC应用模式 -->
<meta name="browsermode" content="application">
<!-- QQ应用模式 -->
<meta name="x5-page-mode" content="app">
<!-- windows phone 点击无高光 -->
<meta name="msapplication-tap-highlight" content="no">
```

### 网页相关

```html

<!-- 申明编码 -->
<meta charset="UTF-8">

<!-- 优先使用 IE 最新版本和 Chrome -->
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
<!-- 关于X-UA-Compatible -->
<meta http-equiv="X-UA-Compatible" content="IE=6"><!-- 使用IE6 -->
<meta http-equiv="X-UA-Compatible" content="IE=7"><!-- 使用IE7 -->
<meta http-equiv="X-UA-Compatible" content="IE=8"><!-- 使用IE8 -->

<!--
    浏览器内核控制
    国内浏览器很多都是双内核（webkit和Trident），webkit内核高速浏览，IE内核兼容网页和旧版网站。而添加meta标签的网站可以控制浏览器选择何种内核渲染。
    国内双核浏览器默认内核模式如下：
    1. 搜狗高速浏览器、QQ浏览器：IE内核（兼容模式）
    2. 360极速浏览器、遨游浏览器：Webkit内核（极速模式）
-->
<meta name="renderer" content="webkit|ie-comp|ie-stand">

<!--
    cache-control、Pragma、Expires
    将这三个属性并列在一起，是因为其跟HTTP头有着同样的属性。从字面上看，加上相应的属性能够让浏览器缓存相应的html内容，
    但是，现实是残酷的，这些标签往往不会生效，甚至在HTML5规范中，http-equiv中的属性并不包括这三个，在meta标签设置缓存无效，
    如果我们需要进行缓存控制的话，还是寄希望与HTTP headers上。
-->
<meta http-equiv="cache-control" content="max-age=180">
<meta http-equiv="cache-control" content="no-cache">
<meta http-equiv="expires" content="0">
<meta http-equiv="expires" content="Tue, 01 Jan 1980 1:00:00 GMT">
<meta http-equiv="pragma" content="no-cache">

<!--
    禁止浏览器从本地计算机的缓存中访问页面内容
    这样设定，访问者将无法脱机浏览。
-->
<meta http-equiv="Pragma" content="no-cache">

<!--
    Cache Control: 指定请求和响应遵循的缓存机制, 指导浏览器如何缓存某个响应以及缓存多长时间.
    no-cache: 先发送请求，与服务器确认该资源是否被更改，如果未被更改，则使用缓存。
    no-store: 不允许缓存，每次都要去服务器上，下载完整的响应。（安全措施）
    public: 缓存所有响应，但并非必须。因为max-age也可以做到相同效果
    private: 只为单个用户缓存，因此不允许任何中继进行缓存。（比如说CDN就不允许缓存private的响应）
    maxage: 表示当前请求开始，该响应在多久内能被缓存和重用，而不去服务器重新请求。
            例如：max-age=60表示响应可以再缓存和重用 60 秒。
 -->
<meta http-equiv="cache-control" content="no-cache">

<!-- Windows 8 磁贴颜色 -->
<meta name="msapplication-TileColor" content="#000">
<!-- Windows 8 磁贴图标 -->
<meta name="msapplication-TileImage" content="icon.png">

<!-- 转码申明用百度打开网页可能会对其进行转码（比如贴广告），避免转码可添加如下meta  -->
<meta http-equiv="Cache-Control" content="no-siteapp">
```

### 其他

```html
<!--
    处于安全方面的考虑，浏览器的同源策略在一定程度上保护了用户安全，
    但是像script、link、img等标签是不受同源策略的影响，而这些因素会给我们的用户带来安全风险，这个时候，该属性就出马了。
    在浏览器中，通过设置该属性来声明哪些动态资源允许被加载以此减少XSS攻击。
    该属性的内容包括了对script、style、font、media等静态资源的控制
-->
<!-- 允许控制资源从何处加载。在 <head> 中尽可能地靠前放置，因为该标签仅适用于在其之后声明的资源。-->
<meta http-equiv="Content-Security-Policy" content="default-src 'self'">


<!--
    让a标签在HTTPS环境下进行DNS预解析，以此来提升网站性能。
    HTML页面中的a标签会自动启用DNS提前解析，但是在HTTPS上却失效了，因此可以启动这个属性
-->
<!-- 通过设置为 "off" 完全退出 DNS 预取 -->
<meta http-equiv="x-dns-prefetch-control" content="on/off">


<!-- Web 应用的名称（仅当网站被用作为一个应用时才使用）-->
<meta name="application-name" content="应用名称">

<!-- Chrome、Firefox OS 和 Opera 的主题颜色 -->
<meta name="theme-color" content="#4285f4">

<!-- 告诉 Google 不显示网站链接的搜索框 -->
<meta name="google" content="nositelinkssearchbox">

<!-- 告诉 Google 不提供此页面的翻译 -->
<meta name="google" content="notranslate">

<!-- 验证网址所有权 -->
<meta name="google-site-verification" content="verification_token"><!-- Google Search Console -->
<meta name="yandex-verification" content="verification_token"><!-- Yandex Webmasters -->
<meta name="msvalidate.01" content="verification_token"><!-- Bing Webmaster Center -->
<meta name="alexaVerifyID" content="verification_token"><!-- Alexa Console -->
<meta name="p:domain_verify" content="code from pinterest"><!-- Pinterest Console -->
<meta name="norton-safeweb-site-verification" content="norton code"><!-- Norton Safe Web -->

<!-- 确定用于构建页面的软件（如 - WordPress、Dreamweaver）-->
<meta name="generator" content="program">

<!-- 关于你的网站主题的简短描述 -->
<meta name="subject" content="你的网站主题">

<!-- 基于网站内容给出一般的年龄分级 -->
<meta name="rating" content="General">

<!-- 允许控制 referrer 信息如何传递 -->
<meta name="referrer" content="no-referrer">

<!-- 禁用自动检测和格式化可能的电话号码 -->
<meta name="format-detection" content="telephone=no">

<!-- 该项已经被废除了。在客户端存储 cookie，web 浏览器的客户端识别 -->
<meta http-equiv="set-cookie" content="name=value; expires=date; path=url">

<!-- 指定要显示在一个特定框架中的页面 -->
<meta http-equiv="Window-Target" content="_value">

<!-- 地理标签 -->
<meta name="ICBM" content="latitude, longitude">
<meta name="geo.position" content="latitude;longitude">
<meta name="geo.region" content="country[-state]"><!-- 国家代码 (ISO 3166-1): 强制性, 州代码 (ISO 3166-2): 可选; 如 content="US" / content="US-NY" -->
<meta name="geo.placename" content="city/town"><!-- 如 content="New York City" -->
```

- 📖 [Google 可以识别的 Meta 标签](https://support.google.com/webmasters/answer/79812?hl=zh-Hans)
- 📖 [WHATWG Wiki: Meta 拓展](https://wiki.whatwg.org/wiki/MetaExtensions)
- 📖 [ICBM - 维基百科](https://en.wikipedia.org/wiki/ICBM_address#Modern_use)
- 📖 [地理标记 - 维基百科](https://en.wikipedia.org/wiki/Geotagging#HTML_pages)

**[⬆ 返回顶部](#目录)**

## Link 链接

```html
<!-- 指向一个外部 CSS 样式表 -->
<link rel="stylesheet" href="https://example.com/styles.css">

<!-- 有助于防止出现内容重复的问题 -->
<link rel="canonical" href="https://example.com/article/?page=2">

<!-- 链接到当前文档的一个 AMP HTML 版本 -->
<link rel="amphtml" href="https://example.com/path/to/amp-version.html">

<!-- 链接到一个指定 Web 应用程序“安装”凭据的 JSON 文件 -->
<link rel="manifest" href="manifest.json">

<!-- 链接到关于页面所有者的信息 -->
<link rel="author" href="humans.txt">

<!-- 指向一个适用于链接内容的版权申明 -->
<link rel="license" href="copyright.html">

<!-- 给出可能的你的另一种语言的文档位置参考 -->
<link rel="alternate" href="https://es.example.com/" hreflang="es">

<!-- 提供了关于作者或其他人的信息 -->
<link rel="me" href="https://google.com/profiles/thenextweb" type="text/html">
<link rel="me" href="mailto:name@example.com">
<link rel="me" href="sms:+15035550125">

<!-- 链接到一个描述历史记录、文档或其他具有历史意义的材料的集合的文档 -->
<link rel="archives" href="https://example.com/archives/">

<!-- 链接到层次结构中的顶级资源 -->
<link rel="index" href="https://example.com/article/">

<!-- 提供了自我引用 - 当文档有多个可能的引用时非常有用 -->
<link rel="self" type="application/atom+xml" href="https://example.com/atom.xml">

<!-- 分别是一系列页面中的第一个，最后一个，上一个和下一个页面 -->
<link rel="first" href="https://example.com/article/">
<link rel="last" href="https://example.com/article/?page=42">
<link rel="prev" href="https://example.com/article/?page=1">
<link rel="next" href="https://example.com/article/?page=3">

<!-- 当使用第三方服务来维护博客时使用 -->
<link rel="EditURI" href="https://example.com/xmlrpc.php?rsd" type="application/rsd+xml" title="RSD">

<!-- 当另一个 WordPress 博客链接到你的 WordPress 博客或文章时形成一个自动化的评论 -->
<link rel="pingback" href="https://example.com/xmlrpc.php">

<!-- 当你在自己的页面上链接到一个 url 时通知它 -->
<link rel="webmention" href="https://example.com/webmention">

<!-- 启用通过 Micropub 客户端发布你的域名 -->
<link rel="micropub" href="https://example.com/micropub">

<!-- 打开搜索 -->
<link rel="search" href="/open-search.xml" type="application/opensearchdescription+xml" title="Search Title">

<!-- Feeds -->
<link rel="alternate" href="https://feeds.feedburner.com/example" type="application/rss+xml" title="RSS">
<link rel="alternate" href="https://example.com/feed.atom" type="application/atom+xml" title="Atom 0.3">

<!-- 预取，预载，预浏览 -->
<!-- 更多信息：https://css-tricks.com/prefetching-preloading-prebrowsing/ -->
<link rel="dns-prefetch" href="//example.com/">
<link rel="preconnect" href="https://www.example.com/">
<link rel="prefetch" href="https://www.example.com/">
<link rel="prerender" href="https://example.com/">
<link rel="preload" href="image.png" as="image">
```

- 📖 [链接关系](https://www.iana.org/assignments/link-relations/link-relations.xhtml)

**[⬆ 返回顶部](#目录)**

## JS 链接

1 js文件放在head里面和放在body里面的区别

首先放在head里面，script 标签如果沒加上 async属性的話，會 block 住浏览器，就是要下载完这个js文件才会进行下一步操作，如果文件很小还好，如果是比较大的，就会有阻塞的效果，影响用户体验。

浏览器解析网页时是一行行解析的，就是说解析到head里面的js文件时就会停下来，而我们的Dom结构是在head下面的body标签里面，就是说我们得等js文件下载完成才能看到body的内容，那我们选择放在body底部的话，浏览器就会优先加载dom，解析到body底部的js时才去下载，但是在下载之前我们已经能看到body的内容，浏览体验就会好一点，

那有人会问，放在body头部和底部有什么区别呢？其实放在body头部的话就和放在head里面一样的啦

2 js文件放在head里面避免弊端

有两个属性可以解决js文件同步下载的问题： defer和async

defer：
如果一个script加了defer属性，即使放在head里面，它也会在html页面解析完毕之后再去执行，也就是类似于把这个script放在了页面底部。
```html
<script defer src="test.js"></script>
```

async：
对于async，这个是html5中新增的属性，它的作用是能够异步的加载和执行脚本，不因为加载脚本而阻塞页面的加载。一旦加载到就会立刻执行。有 async，加载和渲染后续文档元素的过程将和 script.js 的加载与执行并行进行（异步）。但是很有可能不是按照原本的顺序来执行的。如果js前后有依赖性，用async，就很有可能出错。
```html
<script async src="test.js"></script>
```

3 最好把js文件放在哪

现在浏览器做了一些优化，即使把js放在head里面也不会有大问题，所以我们可以将必要的js放在head里面，比较大的js放在body的底部，但是最简单最好方法就是放在body底部，W3C是将js放在head里面；

更多[defer和async的区别](https://segmentfault.com/q/1010000000640869)

**[⬆ 返回顶部](#目录)**

## 网站图标

```html
<!-- 针对 IE 10 及以下版本 -->
<!-- 如果将 `favicon.ico` 放在根目录下，则无需标签 -->

<!-- 我们目前需要提供的最大的网站图标尺寸 -->
<link rel="icon" sizes="192x192" href="/path/to/icon.png">

<!-- Apple 触摸图标 (尺寸同样是 192x192) -->
<link rel="apple-touch-icon" href="/path/to/apple-touch-icon.png">

<!-- Safari 固定选项卡图标 -->
<link rel="mask-icon" href="/path/to/icon.svg" color="blue">
```

- 📖 [所有关于网站图标（和触摸图标）的信息](https://bitsofco.de/all-about-favicons-and-touch-icons/)
- 📖 [创建固定选项卡图标](https://developer.apple.com/library/content/documentation/AppleApplications/Reference/SafariWebContent/pinnedTabs/pinnedTabs.html)
- 📖 [网站图标对照表](https://github.com/audreyr/favicon-cheat-sheet)
- 📖 [网址图标 & 浏览器颜色表](https://developers.google.com/web/fundamentals/design-and-ux/browser-customization/)

**[⬆ 返回顶部](#目录)**

## 社交

### Facebook Open Graph

```html
<meta property="fb:app_id" content="123456789">
<meta property="og:url" content="https://example.com/page.html">
<meta property="og:type" content="website">
<meta property="og:title" content="Content Title">
<meta property="og:image" content="https://example.com/image.jpg">
<meta property="og:description" content="Description Here">
<meta property="og:site_name" content="Site Name">
<meta property="og:locale" content="en_US">
<meta property="article:author" content="">
```

- 📖 [Facebook 的 Open Graph 的标记](https://developers.facebook.com/docs/sharing/webmasters#markup)
- 📖 [Open Graph 协议](https://ogp.me/)
- 🛠 [页面验证 - Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/)

### Twitter Card

```html
<meta name="twitter:card" content="summary">
<meta name="twitter:site" content="@site_account">
<meta name="twitter:creator" content="@individual_account">
<meta name="twitter:url" content="https://example.com/page.html">
<meta name="twitter:title" content="Content Title">
<meta name="twitter:description" content="Content description less than 200 characters">
<meta name="twitter:image" content="https://example.com/image.jpg">
```

- 📖 [名片入门指南 - Twitter 开发者](https://dev.twitter.com/cards/getting-started)
- 🛠 [页面验证 - Twitter Card Validator](https://cards-dev.twitter.com/validator)

### Twitter Privacy
如果你在自己的网站中嵌入了推文，Twitter 可以使用你网站上的信息为 Twitter 用户定制内容和建议。 [更多关于 Twitter 隐私选项的信息](https://dev.twitter.com/web/overview/privacy#what-privacy-options-do-website-publishers-have).
```html
<!-- 禁止 Twitter 使用你网站上的信息用于提供个性化的目的 -->
<meta name="twitter:dnt" content="on">
```

### Google+ / Schema.org

```html
<html lang="" itemscope itemtype="https://schema.org/Article">
  <head>
    <link rel="author" href="">
    <link rel="publisher" href="">
    <meta itemprop="name" content="内容标题">
    <meta itemprop="description" content="内容描述少于 200 个字符">
    <meta itemprop="image" content="https://example.com/image.jpg">
```

**注意:** 这些 meta 标签需要在 `<html>` 中添加 `itemscope` 和 `itemtype` 属性。

- 🛠 请在 [结构化数据测试工具](https://developers.google.com/structured-data/testing-tool/) 上测试你的页面

### Pinterest

根据他们的[帮助中心](https://help.pinterest.com/en/articles/prevent-people-saving-things-pinterest-your-site)可知，Pinterest 允许你禁止他人保存你网站里的内容。`description` 为可选。

```html
<meta name="pinterest" content="nopin" description="Sorry, you can't save from my website!">
```

### Facebook Instant Articles

```html
<meta charset="utf-8">
<meta property="op:markup_version" content="v1.0">

<!-- 你的文章的 Web 版网址 -->
<link rel="canonical" href="https://example.com/article.html">

<!-- 用于该文章的样式 -->
<meta property="fb:article_style" content="myarticlestyle">
```

- 📖 [创建文章 - Instant Articles](https://developers.facebook.com/docs/instant-articles/guides/articlecreate)
- 📖 [代码示例 - Instant Articles](https://developers.facebook.com/docs/instant-articles/reference)

### OEmbed

```html
<link rel="alternate" type="application/json+oembed"
  href="https://example.com/services/oembed?url=http%3A%2F%2Fexample.com%2Ffoo%2F&amp;format=json"
  title="oEmbed Profile: JSON">
<link rel="alternate" type="text/xml+oembed"
  href="https://example.com/services/oembed?url=http%3A%2F%2Fexample.com%2Ffoo%2F&amp;format=xml"
  title="oEmbed Profile: XML">
```

- 📖 [oEmbed 格式](https://oembed.com/)

**[⬆ 返回顶部](#目录)**

## 浏览器 / 平台

### Apple iOS

```html
<!-- 智能应用 Banner -->
<meta name="apple-itunes-app" content="app-id=APP_ID,affiliate-data=AFFILIATE_ID,app-argument=SOME_TEXT">

<!-- 禁用自动检测和格式化可能的电话号码 -->
<meta name="format-detection" content="telephone=no">

<!-- 添加到主屏幕 -->
<!-- 启动图标 (大于等于 180x180px) -->
<link rel="apple-touch-icon" href="/path/to/apple-touch-icon.png">

<!-- 启动屏幕图片 -->
<link rel="apple-touch-startup-image" href="/path/to/launch.png">

<!-- 启动图标的标题 -->
<meta name="apple-mobile-web-app-title" content="应用标题">

<!-- 启用独立（全屏）模式 -->
<meta name="apple-mobile-web-app-capable" content="yes">

<!-- 状态栏外观（除非启用独立模式，否则无效） -->
<meta name="apple-mobile-web-app-status-bar-style" content="black">

<!-- iOS 应用深层链接 -->
<meta name="apple-itunes-app" content="app-id=APP-ID, app-argument=http/url-sample.com">
<link rel="alternate" href="ios-app://APP-ID/http/url-sample.com">
```

- 📖 [配置 Web 应用程序](https://developer.apple.com/library/content/documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html)

### Google Android

```html
<meta name="theme-color" content="#E64545">

<!-- 添加到主屏幕 -->
<meta name="mobile-web-app-capable" content="yes">
<!-- 更多信息：https://developer.chrome.com/multidevice/android/installtohomescreen -->
```

### Google Chrome

```html
<link rel="chrome-webstore-item" href="https://chrome.google.com/webstore/detail/APP_ID">

<!-- 禁用翻译提示 -->
<meta name="google" content="notranslate">
```

### Microsoft Internet Explorer

```html
<!-- 强制 IE 8/9/10 使用其最新的渲染引擎 -->
<meta http-equiv="x-ua-compatible" content="ie=edge">

<!-- 通过 Skype Toolbar 浏览器扩展功能禁用自动检测和格式化可能的电话号码 -->
<meta name="skype_toolbar" content="skype_toolbar_parser_compatible">

<!-- Windows 磁贴 -->
<meta name="msapplication-config" content="/browserconfig.xml">
```

最低要求的的 `browserconfig.xml` 配置：

```xml
<?xml version="1.0" encoding="utf-8"?>
<browserconfig>
  <msapplication>
    <tile>
      <square70x70logo src="small.png"/>
      <square150x150logo src="medium.png"/>
      <wide310x150logo src="wide.png"/>
      <square310x310logo src="large.png"/>
    </tile>
  </msapplication>
</browserconfig>
```

- 📖 [浏览器配置模式参考](https://msdn.microsoft.com/en-us/library/dn320426.aspx)

**[⬆ 返回顶部](#目录)**

## 国内的浏览器

### 360 浏览器

```html
<!-- 选择渲染引擎 -->
<meta name="renderer" content="webkit|ie-comp|ie-stand">
```

### QQ 移动浏览器

```html
<!-- 在指定方向上锁定屏幕（锁定横/竖屏） -->
<meta name="x5-orientation" content="landscape/portrait">
<!-- 全屏显示此页面 -->
<meta name="x5-fullscreen" content="true">
<!-- 页面将以“应用模式”显示（全屏等）-->
<meta name="x5-page-mode" content="app">
```

### UC 移动浏览器

```html
<!-- 在指定方向上锁定屏幕（锁定横/竖屏） -->
<meta name="screen-orientation" content="landscape/portrait">

<!-- 全屏显示此页面 -->
<meta name="full-screen" content="yes">

<!-- 即使在“文本模式”下，UC 浏览器也会显示图片 -->
<meta name="imagemode" content="force">

<!-- 页面将以“应用模式”显示（全屏、禁止手势等） -->
<meta name="browsermode" content="application">

<!-- 在此页面禁用 UC 浏览器的“夜间模式” -->
<meta name="nightmode" content="disable">

<!-- 简化页面，减少数据传输 -->
<meta name="layoutmode" content="fitscreen">

<!-- 禁用的 UC 浏览器的功能，“当此页面中有较多文本时缩放字体” -->
<meta name="wap-font-scale" content="no">
```

- 📖 [UC 浏览器文档](https://www.uc.cn/download/UCBrowser_U3_API.doc)

**[⬆ 返回顶部](#目录)**

## 应用链接

```html
<!-- iOS -->
<meta property="al:ios:url" content="applinks://docs">
<meta property="al:ios:app_store_id" content="12345">
<meta property="al:ios:app_name" content="App Links">

<!-- Android -->
<meta property="al:android:url" content="applinks://docs">
<meta property="al:android:app_name" content="App Links">
<meta property="al:android:package" content="org.applinks">

<!-- 页面回退 -->
<meta property="al:web:url" content="https://applinks.org/documentation">
```

- 📖 [应用链接文档](https://applinks.org/documentation/)

**[⬆ 返回顶部](#目录)**

## 其他资源

- 📖 [HTML5 样板文档：HTML 标签](https://github.com/h5bp/html5-boilerplate/blob/master/dist/doc/html.md)
- 📖 [HTML5 样板文档：扩展和定制](https://github.com/h5bp/html5-boilerplate/blob/master/dist/doc/extend.md)

**[⬆ 返回顶部](#目录)**

## 相关项目

- [Atom HTML Head 片段](https://github.com/joshbuchea/atom-html-head-snippets) - Atom `HEAD` 片段包
- [Sublime Text HTML Head 片段](https://github.com/marcobiedermann/sublime-head-snippets) - Sublime Text `HEAD` 片段包
- [head-it](https://github.com/hemanth/head-it) - `HEAD` 片段的 CLI 接口
- [vue-head](https://github.com/ktquez/vue-head) - 在 Vue.js 中操作 `HEAD` 标签的 meta 信息

**[⬆ 返回顶部](#目录)**

## 其他格式

- 📄 [PDF](https://gitprint.com/joshbuchea/HEAD/blob/master/README.md)

**[⬆ 返回顶部](#目录)**

## 翻译

- 🇺🇸 [英语/English](https://github.com/joshbuchea/HEAD)
- 🇨🇳 [简体中文/Chinese (Simplified)](https://github.com/Amery2010/HEAD)
- 🇩🇪 [德语/German](https://github.com/Shidigital/HEAD)
- 🇧🇷 [巴西葡萄牙语/Brazilian Portuguese](https://github.com/Webschool-io/HEAD)
- 🇮🇹 [意大利语/Italian](https://github.com/Fakkio/HEAD)
- 🇯🇵 [日语/Japanese](https://coliss.com/articles/build-websites/operation/work/collection-of-html-head-elements.html)
- 🇰🇷 [韩语/Korean](https://github.com/Lutece/HEAD)
- 🇷🇺 [俄罗斯语/Russian/Русский](https://github.com/Konfuze/HEAD)
- 🇪🇸 [西班牙语/Spanish](https://github.com/alvaroadlf/HEAD)
- 🇹🇷 [土耳其语/Turkish/Türkçe](https://github.com/mkg0/HEAD)

**[⬆ 返回顶部](#目录)**

## 贡献

**开启一个 issue 或一个 pull 请求来提出修改或补充。**

### 指南

** HEAD ** 仓库由两个分支组成：

#### 1、`master`

对该分支包含的 `README.md` 文件的修改会自动反映在 [gethead.info](https://gethead.info/) 网站上。 所有对照表内容的更改都应该针对此文件。

请按照下列步骤 pull 请求：

- 只修改一个标签，或一次一组相关的标签
- 对属性使用双引号
- 请不要在自我闭合的元素中使用斜线 —— 即便 HTML5 规范中说，他们是可选的
- 考虑在文档中加入链接以支持你所提到的变化

#### 2. `gh-pages`

该分支负责 [gethead.info](https://gethead.info/) 网站。我们使用 [Jekyll](https://jekyllrb.com/) 通过 [GitHub Pages](https://pages.github.com/) 服务来部署 `README.md` Markdown 文件。所有网站相关的修改必须集中在这里。

你可能需要通过 [Jekyll 文档](https://jekyllrb.com/docs/home/) 来了解 Jekyll 是如何在该分支上工作的。

### 贡献者

列出所有超级棒的 [贡献者们](https://github.com/joshbuchea/HEAD/graphs/contributors).

## 作者

**[Josh Buchea](https://joshbuchea.com/)**

### 翻译者

**[子丶言](https://xiangfa.org/)**

### 参考资料

- [那些你不知道的meta标签](https://juejin.im/post/5c288546e51d451a6b51554a)
- [常用meta整理](https://segmentfault.com/a/1190000002407912)
- [HTML meta标签总结与属性使用介绍](https://segmentfault.com/a/1190000004279791)
- [合适的meta，你选对了吗?](https://juejin.im/post/5c08bb31518825371057fcd0)
- [HTML 文档之 Head 最佳实践](https://laozhu.me/post/html-head-best-practices/)
## 协议

![CC0](https://i.creativecommons.org/p/zero/1.0/88x31.png "CC0")

**[⬆ 返回顶部](#目录)**
