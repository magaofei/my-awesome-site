---
title: ruby on rails学习
layout: post
---



# ruby on rails学习

（**档案／资料夹 ：**用途 ）

**app/ ：** 包含你应用程式的 controllers、models、views。你要改的东西大多是这些。

**config/ ：** 设定应用程式的执行阶段规则、路由设定（routes）、资料库等等。

**db/ ：**显示你目前资料库的 schema（结构定义），以及资料库的 migrations。

**public/ ：**这是唯一一个资料夹会是放什么就出现什么的。如果你把档案放里面，server 会直接回传，不会经过 Rails 的处理。

**app/assets/ ：**你会要把图片、JavaScript、stylesheets (CSS) 还有其他静态档案放在里面。现代的 Rails 应用程式使用一种叫做 Assets Pipeline 的东西，把在这资料夹里面的所有 JavaScript 和 CSS 档合并成一个档案来加速。

`rails new` 还建立了其他很多东西。大概可以写一本书来讲，所以我们现在先无视它们。



### new topics

这些网页到底怎么建出来，又是如何连在一起的呢？Rails 的 scaffold 帮你处理好了。

我们来仔细瞧瞧 rails 帮我们建立的档案：

- `app/models/topic.rb`
- 这个档案里面有我们的 topic model 的程式码。如果你仔细看，他其实几乎是空白的。 对资料的新增、读取、更新、删除操作在 Rails 是内建的。
- `app/views/topics`
- 这个资料夹里面有我们的 topics model 的 view 的程式码。 你刚刚使用的表单的程式码就放在这里面。Rails 会帮你建好这些档案作为 scaffold 的一部分。
- 如果你以前写过 HTML，这些程式你应该不陌生。 Rails 的 view 只是 HTML 加上一些用来显示资料库来的资料的程式。
- `app/views/topics/index.html.erb`
  - 这个程式是用在列出所有 topics 的页面。
  - index 是用来表示一个网站或网站的一部分的“预设”页面。当你打开 [http://localhost:3000/topics](http://localhost:3000/topics) 的时候，topics 的 index 页面会传送到你的电脑上。 
- `app/views/topics/show.html.erb`
  - 是当你在 `Listing topics` 按一下 `show` 时会看到的页面。 
- `app/views/topics/new.html.erb`
  - 是当你按一下 `New Topic` 时会看到的页面。
  - `app/views/topics/edit.html.erb`
  - 是当你按一下 `Edit` 时会看到的页面。 
- `app/views/topics/_form.html.erb`
  - 你或许注意到了，新增 topic 和编辑 topics 的页面长得很像。这是因为他们都使用了这个档案来显示表单。 这种档案称作 `partial`，因为他只有网页里面一部分的内容。Partial 的档名一定是底线开头的。 
  - 挑战题：你可以找到 partial 是在 new.html.erb 和 edit.html.erb 的哪一行程式被引用的吗？ 
- `app/controllers/topics_controller.rb`
  - 这称为 controller 档，Rails 自动透过 scaffold 产生的。
  - 如果你打开来看，你会看到每一个 view ，除了 _form.html.erb 之外都对应到一个 method（开头是 def）。