---
title: "Hugo Blog搭建过程"
date: "2022-01-28"
description: "hugo博客搭建"
slug: "test-post"
# image: "cover.jpg"
categories:
    - 博客搭建
tags:
    - Hugo
    - Stack
---

# hugo博客搭建过程
## 安装hugo
```powershell
choco install hugo-extended -confirm
```
## 安装stack主题
```powershell
hugo new site blog
cd blog
git clone https://github.com/CaiJimmy/hugo-theme-stack/ themes/hugo-theme-stack
cp -r themes/hugo-theme-stack/exampleSite/content ./content
cp themes/hugo-theme-stack/config.yaml ./config.yaml
```
## 修改配置文件
```yaml
baseurl: https://lixiaojun2914.github.io
languageCode: zh-cn
theme: hugo-theme-stack
paginate: 5
title: My Blog

# Change it to your Disqus shortname before using
disqusShortname: hugo-theme-stack

# Emoji
enableEmoji: true

# GA Tracking ID
googleAnalytics:

# Theme i18n support
# Available values: en, fr, id, ja, ko, pt-br, zh-cn, zh-tw, es, de, nl, it, th, el, uk
DefaultContentLanguage: zh-cn

# Set hasCJKLanguage to true if DefaultContentLanguage is in [zh-cn ja ko]
# This will make .Summary and .WordCount behave correctly for CJK languages.
hasCJKLanguage: false

permalinks:
    post: /p/:slug/
    page: /:slug/

params:
    mainSections:
        - post
    featuredImageField: image
    rssFullContent: true
    favicon:

    footer:
        since: 2020
        customText:

    dateFormat:
        published: Jan 02, 2006
        lastUpdated: Jan 02, 2006 15:04 MST

    sidebar:
        emoji: 🍥
        subtitle: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
        avatar:
            enabled: true
            local: true
            src: img/avatar.png

    article:
        math: true
        toc: true
        readingTime: true
        license:
            enabled: true
            default: Licensed under CC BY-NC-SA 4.0

    comments:
        enabled: true
        provider: waline

        disqusjs:
            shortname:
            apiUrl:
            apiKey:
            admin:
            adminLabel:

        utterances:
            repo:
            issueTerm: pathname
            label:

        remark42:
            host:
            site:
            locale:

        vssue:
            platform:
            owner:
            repo:
            clientId:
            clientSecret:
            autoCreateIssue: false

        # Waline client configuration see: https://waline.js.org/en/reference/client.html
        waline:
            serverURL: https://blog-waline-lixiaojun2914.vercel.app
            lang: zh-CN
            visitor: true
            avatar:
            emoji:
                - https://cdn.jsdelivr.net/gh/walinejs/emojis/weibo
            requiredMeta:
                - name
                - email
            placeholder:
            locale:
                admin: Admin

        twikoo:
            envId:
            region:
            path:
            lang:

        # See https://cactus.chat/docs/reference/web-client/#configuration for description of the various options
        cactus:
            defaultHomeserverUrl: "https://matrix.cactus.chat:8448"
            serverName: "cactus.chat"
            siteName: "" # You must insert a unique identifier here matching the one you registered (See https://cactus.chat/docs/getting-started/quick-start/#register-your-site)
            
        giscus:
            repo:
            repoID:
            category:
            categoryID:
            mapping:
            lightTheme:
            darkTheme:
            reactionsEnabled: 1
            emitMetadata: 0

        gitalk:
            owner: 
            admin:  
            repo: 
            clientID: 
            clientSecret: 
        
        cusdis:
            host: 
            id: 
    widgets:
        enabled:
            - search
            - archives
            - tag-cloud

        archives:
            limit: 5

        tagCloud:
            limit: 10

    opengraph:
        twitter:
            # Your Twitter username
            site:

            # Available values: summary, summary_large_image
            card: summary_large_image

    defaultImage:
        opengraph:
            enabled: false
            local: false
            src:

    colorScheme:
        # Display toggle
        toggle: true

        # Available values: auto, light, dark
        default: auto

    imageProcessing:
        cover:
            enabled: true
        content:
            enabled: true

### Custom menu
### See https://docs.stack.jimmycai.com/configuration/custom-menu.html
### To remove about, archive and search page menu item, remove `menu` field from their FrontMatter
menu:
    main:
        - identifier: home
          name: Home
          url: /
          weight: -100
          params:
              ### For demonstration purpose, the home link will be open in a new tab
              newTab: true
              icon: home
    
    social:
        - identifier: github
          name: GitHub
          url: https://github.com/lixiaojun2914
          params:
            icon: brand-github
            
related:
    includeNewer: true
    threshold: 60
    toLower: false
    indices:
        - name: tags
          weight: 100

        - name: categories
          weight: 200

markup:
    goldmark:
        renderer:
            ## Set to true if you have HTML content inside Markdown
            unsafe: false
    tableOfContents:
        endLevel: 4
        ordered: true
        startLevel: 2
    highlight:
        noClasses: false

```
## 添加文章
```powershell
hugo new post/new_article/index.md
```
```md
---
title: "测试文章"
description: "文章简介"
date: "2020-08-10 01:00:00+0200"
slug: "test-post"
image: "cover.jpg"
categories:
    - 博客
tags:
    - Hugo
    - Stack
---

![图片 1](Design-V1.jpg)   

![图片 2](Design-V2.jpg)
```
## 生成静态文件
```powershell
hugo -D
```