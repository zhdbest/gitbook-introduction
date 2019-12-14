### 1. 生成的页面左下角会有一个“Published with Gitbook”或者“本书使用 GitBook 发布”，该如何去除？
这个问题便可以通过定制样式来解决：

1. 在当前项目目录下创建“styles/website.css”

2. 编辑该文件，在该文件中添加如下代码：
    ``` css
    .gitbook-link {
        display: none !important;
    }
    ```

### 2. 生成的页面左侧导航栏，如何使用下划线来划分？
* 效果1：

    ![](http://img.zhaohaodong.com/gitbook-introduction/20191017171106.png)

    这种效果是 SUMMARY.md 文件中章节之间有空行造成的，可以根据这种特性来个性化定制导航栏。上面这种效果的 SUMMARY.md ：
    ``` markdown
    # Summary
    * [简介](README.md)
    * [1. 安装](1.install.md)
    * [2. 初始化](2.init.md)

    * [问题解决](question.md)
    ```

* 效果2：

    ![](http://img.zhaohaodong.com/gitbook-introduction/20191017171226.png)
    
    上面这种效果的 SUMMARY.md ：
    ``` markdown
    # Summary
    * [简介](README.md)
    * [1. 安装](1.install.md)
    * [2. 初始化](2.init.md)
    * [问题解决](question.md)
    ```

### 3. 页面推送至 GitHub 后，打开时，一直加载的问题
通过 F12 可以看到，一直加载的是 livereload.js，而这个 js 是 livereload 插件用于自动刷新页面的，调试时可以使用，发布至生产环境时最好关掉，关掉的方式是在 book.json 中将该插件禁用。

该插件的 js 是“\gitbook\gitbook-plugin-livereload\plugin.js”，其代码如下：
``` javascript
(function() {
  var newEl = document.createElement('script'),
      firstScriptTag = document.getElementsByTagName('script')[0];

  if (firstScriptTag) {
    newEl.async = 1;
    newEl.src = '//' + window.location.hostname + ':35729/livereload.js';
    firstScriptTag.parentNode.insertBefore(newEl, firstScriptTag);
  }

})();
```
这里面会去加载 livereload.js，而且是在 35729 这个端口，而 GitHub 不会给我们开放这个端口并提供服务的。



### 4. 插件 flexible-alerts 连续使用多个时，样式错乱

例如：

```markdown
>[!note]
>第一个



> [!note]
> 第二个



>[!note]
>第二个
```

这样连续三个，其效果如下所示：

>[!note]
>
>第一个



> [!note]
>
> 第二个



>[!note]
>
>第二个



该问题的解决办法就是让每个模块之间有点“东西”，但不能是空格，换行也不行（此处换行不是指`<br>`），但是可以加一些 HTML 元素，例如:

```markdown
>[!note]
>第一个

<p></p>

> [!note]
> 第二个

<p></p>

>[!note]
>第二个
```



效果：

>[!note]
>
>第一个

<p></p>
> [!note]
>
> 第二个

<p></p>
>[!note]
>
>第二个