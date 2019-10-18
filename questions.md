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