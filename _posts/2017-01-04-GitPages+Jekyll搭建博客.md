---
layout: post
title:  "使用Github Page和Jekyll搭建博客站点"
date:   2017-01-04 19:34:32 +0800
categories: 个人
---

## 1.去github开通 GitHub Pages
[这里](https://pages.github.com/)

## 2.把新建的pages工程pull到本地
```shell
git clone https://github.com/x13945/x13945.github.io
```

## 3. 准备jekyll相关东西
```shell
sudo gem install jekyll bundler
sudo bundle install github-pages
```

## 4. 用jekyll重新初始化pages工程目录
```shell
cd path_to_pages_dir
jekyll new . --force
```

## 5. 初步使用jekyll预览博客
```shell
bundle exec jekyll serve
```
然后我们就可以在浏览器输入[http://127.0.0.1:4000](http://127.0.0.1:4000)来查看我们的博客了.当然,这个时候还是一片荒芜,只有一下jekyll给出的默认信息.之后,在我们修改博客内容的时候,这条命令会自动刷新我们的修改.因此算是比较方便.

> 如果在github pages里保有初始化github page仓库时的`index.html`,请手动删除.不然访问[http://127.0.0.1:4000](http://127.0.0.1:4000)的时候会看不到我们的博客.

## 6. 使用github pages而不是jekyll来处理我们的网站
按照`Gemfile`中的描述
```
# If you want to use GitHub Pages, remove the "gem "jekyll"" above and
# uncomment the line below. To upgrade, run `bundle update github-pages`.
```
修改信息.

## 7. 修改站点信息
修改`about.md`和`_config.yml`来修改我们站点的一下默认属性.

## 8.发布第一篇博客
我们可以在`_posts`目录下新建一个md文件,注意文件名的格式是:yyyy-mm-dd-博客-名字.md.当然也可以参考`_posts`目录下的那个初始例子文件,一般叫做`welcome-to-jekyll.markdown`.
然后记得在md文件的开头处加入类型下面的东东,

```
---
layout: post
title:  "2016年终总结"
date:   2017-01-04 19:34:32 +0800
categories: 个人
---
```

以便于jekyll对文章进行分类显示.

## 结语
大致这么多了.大家开心就好了.:)