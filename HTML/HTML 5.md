## 本地存储
- localStorange
- sessionStorage

## 离线存储
- appcache

## service worker
Service worker是一个注册在指定源和路径下的事件驱动worker。它采用JavaScript控制关联的页面或者网站，拦截并修改访问和资源请求，细粒度地缓存资源。你可以完全控制应用在特定情形（最常见的情形是网络不可用）下的表现。

Service worker运行在worker上下文，因此它不能访问DOM。相对于驱动应用的主JavaScript线程，它运行在其他线程中，所以不会造成阻塞。它设计为完全异步，同步API（如XHR和localStorage）不能在service worker中使用。出于安全考量，Service workers只能由HTTPS承载
- 后台同步
- 响应推送
## 语义化标签
### 优点
- 提升可访问性
- SEO
- 结构清晰，利于维护
### eg
- <title></title>：简短、描述性、唯一（提升搜索引擎排名）
- <header></header>：页眉通常包括网站标志、主导航、全站链接以及搜索框。
- <nav></nav>：标记导航，仅对文档中重要的链接群使用。
- <main></main>：页面主要内容，一个页面只能使用一次。如果是web应用，则包围其主要功能。
- <article></article>：表示文档、页面、应用或一个独立的容器
- <footer></footer>：页脚，只有当父级是body时，才是整个页面的页脚。

## data-
## classList
## 表单
- email
- url
- number
## audio和video
## websocket
