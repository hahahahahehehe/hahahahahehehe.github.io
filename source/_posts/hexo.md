---
title: hexo
date: 2026-09-17 23:57:24
categories: 
  - [前端, hexo]
tags:
  - hexo
  - 个人网站搭建
---

# 一、什么是hexo

Hexo 是一个快速、简洁且高效的博客框架。 Hexo 使用 [Markdown](http://daringfireball.net/projects/markdown/)（或其他标记语言）解析文章，在几秒内，即可利用靓丽的主题生成静态网页

官方网站:https://hexo.io/zh-cn/docs/

# 二、安装hexo

```javascript
npm install -g hexo-cli
```



# 三、初始化hexo

## 3.1 初始化并安装依赖

```javascript
hexo init <folder>
cd <folder>
npm install
```



## 3.2 目录结构

初始化之后，生成的目录结构如下

![image-20260918000417508](/img/hexo/image-20260918000417508.png)

| 文件/目录名  | 作用                                                         |
| ------------ | ------------------------------------------------------------ |
| _config.yml  | 网站的配置文件                                               |
| package.json | 项目依赖文件                                                 |
| scaffolds    | [模版](https://hexo.io/zh-cn/docs/writing#模版（Scaffold）) 文件夹。 当您新建文章时，Hexo 会根据 scaffold 来创建文件 |
| source       | 源文件，资源文件夹。 是存放用户资源的地方。 除 `_posts` 文件夹之外，开头命名为 `_` (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。 Markdown 和 HTML 文件会被解析并放到 `public` 文件夹，而其他文件会被拷贝过去 |
| _drafts      | 草稿箱目录                                                   |
| _posts       | 文件默认存放位置                                             |
| themes       | 主题                                                         |



## 3.3 本地文章生成

在使用`hexo init`之后，本地hexo结构就已经完成了，后面可以生成文章了

### 3.3.1 生成文章

```
hexo new [layout] <title>
```

1、layout可以不写，有默认值，在_config.yml中的default_layout配置决定，默认为post，也就是说，执行`hexo new index`，会在source/_posts下面生成一个index.md。生成的文件名由_config.yml中的new_post_name配置决定,默认是:title.md，而我们的title配置的是index,所以生成的文件就叫index.md.

2、在scaffolds目录下有draft.md，page.md，post.md，layout是什么就会使用什么模板。比如我这边使用的是post的layout，所以我们使用的就是post.md的模板

3、以post.md模板为例，其中categories和tags是我自己加的，里面可以自定义什么参数，参考[模板](https://hexo.io/zh-cn/docs/front-matter),但是别加Front-matter格式的---，否则后面构建的时候可能会报错，测试，发现不加---，也能正常使用

- title
  - 文章标题
- date
  - 文章日期，可以在网站上根据日期进行文章排序
- categories
  - 分类，后面文章可以根据分类进行筛选

​	如果写了

```
categories: 
	- 编程
	- 前端技术
# 会生成对应的父子分类。页面路径会生成 /categories/编程/前端技术/
```



- tags
  - 标签，可以根据标签进行筛选文章

​	如果写了

```
tags: 
	- 博客
	- hexo
# 则是生成了同级多个标签
```



![image-20260918225641028](/img/hexo/image-20260918225641028.png)

在生成了文章之后，我们就可以在这个md文件中去写文章了



### 3.3.2 categories

虽然我们在文章中写了categories，但是，需要创建一个categories页面之后，才能在网站中展示出对应有哪些分类

```
hexo new page categories
```

会生成 `source/categories/index.md`文件，最终会渲染成分类页，也就是下面这个页面

![image-20260918230830108](/img/hexo/image-20260918230830108.png)



### 3.3.3 tags

和categories一致，只是生成的页面命令为

```
hexo new page tags
```

生成 `source/tags/index.md`



### 3.3.4 清理已构建数据

```
hexo clean
```



### 3.3.5构建

```
hexo g  # 同 hexo generate
```

构建之后会将source里面的md文件构建成public目录里面的html文件

### 3.3.56启动本地服务

```
hexo s # 同hexo server
```

可以在本地查看页面渲染有没有问题，没有问题的话，就可以上传到git仓库

### 3.3.6 上传版本库

```
git status # 查看文件状态
git add . # 将当前所有及其子目录加入暂存区
git commit -m"备注" # 将文件加入私有仓库
git push origin master # 将本地仓库上传至github仓库
```

## 3.4 搭建github page

[参考网站](https://hexo.io/zh-cn/docs/github-pages)



# 四、官网配置

## 4.1 配置

[配置](https://hexo.io/zh-cn/docs/configuration)

## 4.2 hexo命令

[命令](https://hexo.io/zh-cn/docs/commands)

