---
title: Hexo文章中如何插入图片
categories: 
- Hexo
tags:
- Hexo
---
在hexo中发表文章时发现自己的图片无法显示，这是因为hexo在解析你的文章时找不到你的图片路径，下面说一下如何配置文章中的图片路径



打开在hexo根目录下的 _config.yml 配置文件，找到 post_asset_folder 属性，默认为 false 改为 true  

在hexo根目录下执行如下命令
``` bash
cnpm install hexo-asset-image
```
此时再执行命令 hexo n article_name 创建新的文章，在 source/_posts 中会生成文章 post_name.md 和同名文件夹 post_name,我们将文章中所使用到的将图片资源均放在 post_name 中，这时就可以在文章中使用相对路径引用图片资源了

``` bash
[img_name](img_name.jpg) #文章中的图片资源路径格式
```