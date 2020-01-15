# 简介

本章节主要介绍一些 gitbook 常用的插件。



##  back-to-top-button

当文章太长时，在文章的底部出现回到顶部的按钮。配置方式如下：

```json
{
    "plugins" : [
        "back-to-top-button"
    ]
}
```



## code

用于一键复制代码。

配置：

```json
{
    "plugins" : [
        "code"
    ]
}
```

效果：

![](http://img.zhaohaodong.com/plugin-code.png)



## popup

本身 gitbook 生成的页面中的图片是不可点击的，可以通过该插件使得图片可点击并在新窗口弹出大图。

配置：

```json
{
    "plugins" : [
        "popup"
    ]
}
```



## search-pro

gitbook 默认插件中包含了搜索的插件`search`，但是该插件一方面查询结果不准确，文章内容难以检索出来，另一方面，查询结果中也不会高亮关键字，这些问题可以使用`search-pro`插件来解决，但是需要注意的是要禁用默认的`search`插件以及`lunr`插件（如果不禁用`lunr`插件，会导致页面就不展示调整字体的按钮）。

配置：

```json
{
    "plugins" : [
        "-search",
        "-lunr",
        "search-pro"
    ]
}
```

效果如下：

![](http://img.zhaohaodong.com/plugin-search-pro.png)

注意，上图就是没有禁用`lnur`插件时的截图，此时页面未展示调整字体的按钮。



## ancre-navigation

该插件有两个作用，一是添加本页的目录到右侧悬浮展示，二是生成一个回到顶部的按钮。

使用该插件时，需注意该插件只会提取前三级标题，并且要从一级标题开始而且不能跨标题。

```markdown
如下可正确解析三级标题作为目录：
# h1
## h2-1
## h2-2
### h3
------------------
如下不会被解析：
## h2
------------------
如下只能解析一级标题：
# h1
### h3
```



配置：

```json
{
    "plugins" : [
        "ancre-navigation"
    ]
}
```

效果：

![](http://img.zhaohaodong.com/gitbook-introduction/plugin-ancre-navigation.png)

注意，可以看到由于我同时使用了`ancre-navigation`和`back-to-top-button`，所以右下角有两个回到顶部按钮。



## alerts

该插件可以将引用做成好看的效果。

配置：

```json
{
    "plugins" : [
        "alerts"
    ]
}
```



### 信息

```kotlin
> **[info] For info**
>
> Use this for infomation messages.
```

> **[info] For info**
>
> Use this for infomation messages.

### 警告

```kotlin
> **[warning] For warning**
>
> Use this for warning messages.
```

> **[warning] For warning**
>
> Use this for warning messages.

### 危险

```kotlin
> **[danger] For danger**
>
> Use this for danger messages.
```

> **[danger] For danger**
>
> Use this for danger messages.

### 成功

```kotlin
> **[success] For success**
>
> Use this for success messages.
```

> **[success] For success**
>
> Use this for success messages.



## flexible-alerts

该插件与`alerts`类似，但是提供了更丰富的配置。

### 默认配置效果

配置：

```json
{
    "plugins" : [
        "flexible-alerts"
    ]
}
```

markdown 文档中引用：

```markdown
> [!note]
> note的
```

效果：

![](http://img.zhaohaodong.com/gitbook-introduction/plugin-flexible-alerts-default.png)

### 自定义配置

配置：

```json
{
    "plugins" : [
        "flexible-alerts"
    ],
    "pluginsConfig": {
        "flexible-alerts" : {
            "style": "flat"
        }
    }
}
```

效果：

>[!note]
>
>note的

除了全局配置，还可以对单个引用块进行定制，假设目前的全局配置为上面的配置，此时我们想要一个默认效果的引用块，可以在 markdown 文档中这样写：

```markdown
>[!note|style:callout|label:Note]
>note的
```

效果：

>[!note|style:callout|label:Note]
>
>note的

`className`也可以由自己指定，样式文件写在总的样式文件中（比如我的是项目根目录下的`styles/website.css`）。

如下，是我创建一个新的样式class及使用的相关代码：

* website.css

  ```css
  .alert.flat.note-new {
      color: #285b2a;
      background-color: #ecf1e8;
      border-style:none;
      border-radius: 0.5em;
  }
  
  .alert.flat.note-new .title {
      color: #3f6a22;
  }
  ```

* markdown 文档

  ```markdown
  >[!note|className:note-new]
  >这是`className`为`note-new`的效果，相较于默认效果，设置了无边框，并添加了边框为圆角。
  ```
* 效果

  >[!note|className:note-new|style:flat]
  >
  >这是`className`为`note-new`的效果，相较于默认效果，设置了无边框，并添加了边框为圆角。



### 引入新的类型

除了默认的四种类型：note、tip、warning、danger 之外，还可以自定义新的类型，如下：

```json
{
  "plugins": [
    "flexible-alerts"
  ],
  "pluginsConfig": {
    "flexible-alerts": {
      "style": "flat",
      "comment": {
        "label": "Comment",
        "icon": "fa fa-comments",
        "className": "info"
      }
    }
  }
}
```

Markdown 文档：

```markdown
> [!COMMENT]
> 这是一条评论
```

效果：

> [!COMMENT]
> 这是一条评论

配置信息中的`icon`是[Font Awesome](http://www.fontawesome.com.cn/faicons/)的图标。

更多关于该插件的使用和配置，可参考 [github](https://github.com/zanfab/gitbook-plugin-flexible-alerts)。



## versions-select

可通过该插件来设置书的版本，配置如下：

```json
{
  "plugins": [ "versions-select" ],
  "pluginsConfig": {
    "versions": {
      "options": [
        {
          "value": "http://react-redux-firebase.com/history/v1.4.0/",
          "text": "Version v1.4.0"
        },
        {
          "value": "http://react-redux-firebase.com/history/v2.0.0/",
          "text": "Version v2.0.0"
        }
      ]
    }
  }
}
```

效果：

![](http://img.zhaohaodong.com/gitbook-introduction/plugin-versions-select.png)



## advanced-emoji

该插件提供了 emoji 表情的支持，配置如下：

```json
{
    "plugins": [
        "advanced-emoji"
    ]
}
```

emoji 表情地址：https://www.webfx.com/tools/emoji-cheat-sheet/

使用时如下：

<p>:one:</p>  

<p>:two:</p>  

<p>:smile:</p>

效果如下：

 :one:  

:two:   

:smile:

