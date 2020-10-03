# Building Website With Hugo




## 建站记录 Hugo framework

https://swallowblack.github.io/

### 1. Install hugo on mac

Follow the official hugo installation guide:

https://gohugo.io/getting-started/installing/



Download Hugo extended version 

https://github.com/gohugoio/hugo/releases



Install into your bin directory

export the hugo PATH(e.g., ~/bin) to your existing PATH

<!--more-->

### 2. Theme Lovelt installation and configuration

Follow the theme LoveIt official guide:

https://hugoloveit.com/zh-cn/theme-documentation-basics/#5-%E6%90%9C%E7%B4%A2

### 3. 站点配置

#### 评论 （Valine）

1. LeanCloud 注册和创建app（我选择的国际版）

https://leancloud.app/

2. 在站点配置文件填写相关内容

将上一步得到的appID, appKey填入站点配置文件。

#### 站内搜索 （主题默认）

此版本竟然自带搜索，很省心，只需使用主题的默认配置即可。

3. menu bar

```shell
[menu]
  [[menu.main]]
    identifier = "posts"
    # 你可以在名称 (允许 HTML 格式) 之前添加其他信息, 例如图标
    pre = ""
    # 你可以在名称 (允许 HTML 格式) 之后添加其他信息, 例如图标
    post = ""
    name = "所有文章"
    url = "/posts/"
    # 当你将鼠标悬停在此菜单链接上时, 将显示的标题
    title = ""
    weight = 1
  [[menu.main]]
    identifier = "tags"
    pre = ""
    post = ""
    name = "标签"
    url = "/tags/"
    title = ""
    weight = 2
  [[menu.main]]
    identifier = "categories"
    pre = ""
    post = ""
    name = "分类"
    url = "/categories/"
    title = ""
    weight = 3
  [[menu.main]]
    identifier = "github"
    pre = "<i class=\"fab fa-github fa-fw\"></i>"
    post = ""
    name = ""
    url = "https://github.com/swallowblack"
    title = "GitHub"
    weight = 4
  [[menu.main]]
    identifier = "rss"
    pre = "<i class=\"fa fa-rss fa-fw\"></i>"
    post = ""
    name = ""
    url = "https://swallowblack.github.io/posts/index.xml"
    title = "RSS"
    weight = 5

```



