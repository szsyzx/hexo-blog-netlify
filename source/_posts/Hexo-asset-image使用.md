---
title: Hexo-asset-image
date: 2021-12-30 11:08:10
categories: 
- Hexo
tags:
- Hexo
---

# Hexo-asset-image 插件的使用

当发布新文章时，使用了 hexo-asset-image 这个插件来使用资源文件夹

## 安装方法为:
``` bash
npm install hexo-asset-image --save
```
在资源文件夹当中可以放置博文需要引用的资源，例如图片等，流程详见官方文档：资源文件夹的使用

使用该插件后新建文章 hexo new "test" ，就会在 _post 文件夹生成与新文章同名的资源文件夹，然后再在文章里使用 Markdown 的引用图片的方式进行引用，在使用 hexo g 后，生成的 html 文件会自动的加上图片的绝对路径


修改 hexo-asset-image 插件的源代码

找到路径 node_modules\hexo-asset-image\index.js ,替换其中的内容为：

``` bash
'use strict';
var cheerio = require('cheerio');

// http://stackoverflow.com/questions/14480345/how-to-get-the-nth-occurrence-in-a-string
function getPosition(str, m, i) {
  return str.split(m, i).join(m).length;
}

var version = String(hexo.version).split('.');
hexo.extend.filter.register('after_post_render', function(data){
  var config = hexo.config;
  if(config.post_asset_folder){
    	var link = data.permalink;
	if(version.length > 0 && Number(version[0]) == 3)
	   var beginPos = getPosition(link, '/', 1) + 1;
	else
	   var beginPos = getPosition(link, '/', 3) + 1;
	// In hexo 3.1.1, the permalink of "about" page is like ".../about/index.html".
	var endPos = link.lastIndexOf('/') + 1;
    link = link.substring(beginPos, endPos);

    var toprocess = ['excerpt', 'more', 'content'];
    for(var i = 0; i < toprocess.length; i++){
      var key = toprocess[i];
 
      var $ = cheerio.load(data[key], {
        ignoreWhitespace: false,
        xmlMode: false,
        lowerCaseTags: false,
        decodeEntities: false
      });

      $('img').each(function(){
		if ($(this).attr('src')){
			// For windows style path, we replace '\' to '/'.
			var src = $(this).attr('src').replace('\\', '/');
			if(!/http[s]*.*|\/\/.*/.test(src) &&
			   !/^\s*\//.test(src)) {
			  // For "about" page, the first part of "src" can't be removed.
			  // In addition, to support multi-level local directory.
			  var linkArray = link.split('/').filter(function(elem){
				return elem != '';
			  });
			  var srcArray = src.split('/').filter(function(elem){
				return elem != '' && elem != '.';
			  });
			  if(srcArray.length > 1)
				srcArray.shift();
			  src = srcArray.join('/');
			  $(this).attr('src', config.root + link + src);
			  console.info&&console.info("update link as:-->"+config.root + link + src);
			}
		}else{
			console.info&&console.info("no src attr, skipped...");
			console.info&&console.info($(this));
		}
      });
      data[key] = $.html();
    }
  }
});
```

然后重新使用 hexo g 进行生成，本地生成的图片链接就会正常，hexo d部署后也能够在网页上正常访问

