# 安装

> gitbook 需要node切换为 V10.15.3，否则无法安装与正常运行

~~~bash
npm install gitbook-cli -g #全局安装gitbook
gitbook -V #查看是否安装正常
~~~

# 常用命令

```bash
gitbook init #初始化文件夹
gitbook install #安装依赖
gitbook serve #运行服务
gitbook build [gitbook项目路径] [编译目录，默认_book] #把文件编译成html格式
```

# 配置及插件使用

> 根目录创建book.json文件并按如下格式配置

```json
{
  //插件
  "plugins": [
        "splitter",              # splitter 侧边栏宽度可调节
        "copy-code-button",      # 快速复制按钮
        "highlight",             # 代码高亮
        "accordion",             # 折叠模块(页面内容可折叠)
        "back-to-top-button",    # 回到顶部按钮

        "search-pro", # search-pro支持中文搜索，在使用此插件之前，需要将默认的search和lunr 插件去掉
        "-search",         
        "-lunr",
        
        "chapter-fold",                   # 左侧目录可折叠
        "expandable-chapters",            # 也是左侧目录折叠的插件，不同的是可以解决chapter-fold插件的bug
        "-expandable-chapters-small",     # 也是折叠菜单的，但是这个插件跟chapter-fold有一样的bug

        "fontsettings",
        "livereload",            # 为GitBook实时重新加载
        "popup",                 # 打开新的页面查看图片
        
        "-sharing",              # 去掉左右分享功能
        "theme-default",
        "theme-comscore",        # 主题插件，修改标题和表格颜色
        "page-treeview"          # 在页面顶部显示目录
  ],
  "title": "常用手册",
  //插件配置
  "pluginsConfig": {
    "chapter-fold": {},
        "page-treeview": {
            "copyright": "Copyright &#169; aleen42",
            "minHeaderCount": "2",
            "minHeaderDeep": "2"
        }
  },
  //自定义样式
  "styles": {
    "website": "website.css"
  }
}
```

# 设置目录层级结构

> SUMMARY.md 就是一个markdown文件的目录结构当中内容遵循如下格式

**星号 空格 方括号 圆括号**

  * 星号：的缩进代表所在条目的层级结构，四个空格为一个层级
  * 方括号：中是链接的名字
  * 圆括号：中是一个文件路径及文件名
  * 默认的 README.md 是说明文件可以编辑内容但不能删除

**SUMMARY.md示例**

```markdown
* [前言](README.md)
* [第一章](chapter1/chapter1.md)
    * [第1节](chapter1/section1.md)
    * [第2节](chapter1/section2.md)
* [第二章](chapter2/chapter2.md)
    * [第1节](chapter2/section1.md)
    * [第2节](chapter2/section2.md)
* [总结](summary.md)
```

