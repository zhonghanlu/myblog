---
title: My hexo was born

date: 2022年8月15日15:08:16

description: 本站的建站小过程

keywords: HEXO

tags: 
  - HEXO
  - CI
  - SEO

categories: 
  - 建站
  - 教程

sticky: 1
---

### 初衷

​	一直想拥有自己一个博客，为了这个博客我甚至还在慕课上特意学了一丢丢前端，只可惜实在学不下去。最终听从公司大哥的意见直接使用模板建站吧，哈哈哈哈，最终还是倒在了懒。这一篇是这个博客的第一篇文章，记录下建站过程

### 博客选型

​	刚开始在做博客选型时，就直接想着硬着头皮租个服务器，前后端全部干，一个人完完全全定制出一个专属的博客，但是倒在了懒的上面，我不想动，我又想要，所以你动吧

![image-20220815132409288](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815132409288.png)

​	最终考虑到了模板博客上面，看了眼我们公司大哥的一个博客其实也不错，就更加下定决心考虑模板博客了（我们公司大哥的博客在友链里面）

### 实际技术知识

​	到了最关键的地方，看完我这篇博客你能学会什么呢？其实内容还是很多的，我大概列举下了以下几点

   + Hexo的基础使用

   + GitHub的pages的使用

   + Github中的CI——Actions

   + Github最贴切的CI——Travis CI

   + Github做图床

   + 将网站进行百度SEO

   + 网站进行双部署，CDN加速

   + themes中butterfly的使用

   + 域名的使用等.....

     此处不一一列举了

### 实操

#### 第一步安装Hexo

安装Hexo的前提为已经将Hexo和nodejs安装完成了

创个myblog进行下载Hexo

```javascript
npm install -g hexo-cli
```

用`hexo -v`查看一下版本

至此就全部安装完了。

接下来初始化一下hexo

```javascript
hexo init myblog
```

这个myblog可以自己取什么名字都行，然后

```javascript
cd myblog //进入这个myblog文件夹
npm install
```

新建完成后，指定文件夹目录下有：

- node_modules: 依赖包
- public：存放生成的页面
- scaffolds：生成文章的一些模板
- source：用来存放你的文章
- themes：主题
- ** _config.yml: 博客的配置文件**

```javascript
hexo clean //清楚缓存等   有cdn时需要将cdn的缓存清了
hexo g  //会生成js html等
hexo server //启动服务
```

大概长这样：

![image-20220815134238132](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815134238132.png)

至此安装完成！！！ *★,°*:.☆(￣▽￣)/$:*.°★* 。

#### 配置Github

登上自己的同性交友网站，进行创建仓库，此处创建仓库时，建议仓库名和github的名字一致，方便后续的gitpages访问（其实这一块，我第一次是一摸一样的整，但是没成功，于是乎我又换种方式整了）

![image-20220815134614152](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815134614152.png)

创建完仓库github这部分差不多结束了，后面就牵扯到了提交问题

我这一块的处理是将生成的静态页面放在仓库的gh-pages分支上的，例如

![image-20220815135029638](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815135029638.png)

源码是放在master上的

![image-20220815135103149](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815135103149.png)

这是上传成功的一个大致模板样子，还需要再仓库的setting中设置下pages的分支选择

![image-20220815135245042](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815135245042.png)

设置完此分支基本上就大功告成了。有点需要注意的是，我访问github使用ssh密钥方式访问的，如过使用https访问的话需要进行配置token，这个token也很好找，在头像下面有个setting进入随机会有有个devpl...啥的，进去就能看见token的获取，名字随便填，生成完之后需要将token保存下来，此token只会显示这一次。仓库的秘钥设置下，名字记住便于后面Actions的自动部署。

![image-20220815135602133](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815135602133.png)

#### 将hexo部署到GitHub

​	准备就绪，就可以将hexo部署到GitHub上了

我们就可以将hexo和GitHub关联起来，也就是将hexo生成的文章部署到GitHub上，打开站点配置文件 `_config.yml`，翻到最后，修改为

```javascript
deploy:
  - type: 'git'
    repo: git@github.com:zhonghanlu/myblog.git
    branch: gh-pages
  - type: baidu_url_submitter
```

先安装deploy-git ，也就是部署的命令,这样你才能用命令部署到GitHub。

```javascript
npm install hexo-deployer-git --save
```

然后

```javascript
hexo clean
hexo generate
hexo deploy
```

其中 `hexo clean`清除了你之前生成的东西，也可以不加。
 `hexo generate` 顾名思义，生成静态文章，可以用 `hexo g`缩写
 `hexo deploy` 部署文章，可以用`hexo d`缩写

成功就像git正常push一样，没报错就ok了，如果报错了基本上就是github的基础提交问题

过一会儿就可以在`http://yourname.github.io` 这个网站看到你的博客了！！

#### CI

​	将hexo c && hexo g && hexo s && hexo d && gulp 进行自动化部署

由于提交一次，推送一次过于麻烦，有自动化的工具为啥不用嘞？

所以我在这儿选了两种自动化的方式，一种是Travis CI（这个玩意贼鸡儿狗，贼恶心，我哐哐配置好了，各种各样的原因，我都解决了，最后跟我说收费了，就只有1000积分，一次五分，wqnmd），我选择免费因为我是白嫖党

![image-20220815140531257](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815140531257.png)

第二种方式就是Github Actions  力荐，这个真的贼好用

就是这个小玩意

![image-20220815140655255](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815140655255.png)

这个小玩意咋用来？？

非常简单跟我来

首先在你文件的 .github文件夹下建一个workflows文件夹，注意一定要正确无误，这个yml的名字就随便取一下吧

![image-20220815140828012](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815140828012.png)

![image-20220815140847924](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815140847924.png)

文件内容大致如下：

```yaml
name: HEXO CI
 
on:
  push:
    branches:
    - master
 
jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [14.x]
 
    steps:
      - uses: actions/checkout@v1
 
      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v1
        with:
          node-version: ${{ matrix.node-version }}
 
      - name: Configuration environment
        env:
          HEXO_DEPLOY_PRI: ${{secrets.HEXO_DEPLOY_PRI}}
        run: |
          mkdir -p ~/.ssh/
          echo "$HEXO_DEPLOY_PRI" > ~/.ssh/id_rsa
          chmod 600 ~/.ssh/id_rsa
          ssh-keyscan github.com >> ~/.ssh/known_hosts
          git config --global user.name "zhonghanlu"
          git config --global user.email "1420865757@qq.com"
      - name: Install dependencies
        run: |
          npm i -g hexo-cli
          npm i
      - name: Deploy hexo
        run: |
          hexo clean && hexo generate && hexo deploy
```

至此，GitHub 的Actions就完成了，推送一次看看，在Actions中就可以查看到，fail了会发邮件给你的哦

成功了：

![image-20220815141131279](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815141131279.png)

失败了：

![image-20220815141205531](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815141205531.png)

其实工作原理很简单：就是监听你的提交和你的那个workflows文件中的yml文件进行处理的，我这一块还加入了github的pages一个部署

Travis CI的原理也是很简单：就多了一部的GitHub的授权问题

#### GitHub图床

​	如果网站中的图片全是网络上的资源，网站会很慢很慢，或者是本地资源也会很慢，甚至可能丢失，所以我这一块采用图床处理。网络上的图床有很多

![image-20220815141722922](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815141722922.png)

我这一块采用同行交友网站，不要问我为什么，因为他免费！！！

具体操作就是创建一个GitHub创建一个空的仓库

然后在GitHub上下载那个picgo这个rela..包，进行安装即可，安装完成进行配置下github就可以了比如

这儿的token就是上面申请的token

![image-20220815141939488](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815141939488.png)

然后在typora中进行设置图像设置   文件-》偏好设置-》图像

![image-20220815142044290](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815142044290.png)

然后就可以进行上传测试了，上传成功后，仓库内也会产生一个对应的照片，就相当于一个文件存储功能，但是这个文件大小有上限（能用，就是有点小），像极了你女朋友说你的样子

![image-20220815142238733](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815142238733.png)

此处的加速使用的是国内某大佬映射过去的地址，之前的地址被DNS玷污了，唉多好的一个被玷污了，真可恶，我没赶上

#### 网站进行百度SEO

​	百度的seo，说的简单点就是能让百度搜到我们的网站，其实就是让百度收录下我们的网站，非常慢非常慢，有人就喜欢非常慢，我在某种程度上也是很慢

首先查看网站收录情况 `site:你的网站

安装 sitemap

```javascript
npm install hexo-generator-baidu-sitemap --save
```

根目录_config.yaml添加如下的配置（注意每行的空格）生成对应xml文件

```yaml
# sitemap
sitemap:
 path: sitemap.xml
baidusitemap:
 path: baidusitemap.xml
```

```yaml
url: https://zhonghanlu.club/
root: /
permalink: archives/:abbrlink.html
abbrlink:
 alg: crc32  # 算法：crc16(default) and crc32
 rep: hex   # 进制：dec(default) and hex
```

我这一块顺带生成了那个页面持久化，好像需要装插件，但我忘记了；就想好像需要戴套，但我忘记了

博客根目录中的 source 文件夹下，添加蜘蛛协议 “robots.txt” 的文件，内容如下：

```yaml
User-agent: *
Allow: /
Allow: /categories/
Allow: /tags/
Allow: /archives/
Allow: /about/

Disallow: /vendors/
Disallow: /js/
Disallow: /css/
Disallow: /fonts/
Disallow: /vendors/
Disallow: /fancybox/

记得替换成你的域名

Sitemap: http://域名/sitemap.xml
Sitemap: http://域名/baidusitemap.xml
```

主动推送

```javascript
npm install hexo-baidu-url-submit --save
```

_config.yaml

```yml
baidu_url_submit:
  count: 100 # 提交最新的一个链接
  host:  '' # 在百度站长平台中注册的域名
  token: '' # 请注意这是您的秘钥
  path: baidu_urls.txt # 文本文档的地址，新链接会保存在此文本文档里
```

域名和秘钥可以在站长工具平台的连接提交中的接口调用地址中找到，即对应host与token后面的字段。

![image-20220815143553722](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815143553722.png)

修改deploy

```yaml
deploy:
  - type: 'git'
    repo: git@github.com:zhonghanlu/myblog.git
    branch: gh-pages
  - type: baidu_url_submitter
```

紧接着就是百度官网的添加收录了，此处不过多赘诉

#### 双部署，CDN加速

​	双部署，为啥需要双部署呢，因为我们整个站是访问github，github这个访问速度有目共睹的啊，贼鸡儿慢

所以我们需要再次挂载到本国的，coding，再加上好招云进行免费的CDN加速，再加上gulp进行静态页面压缩，你就说这一套下来，我们国人访问的速度快不快就完事了。但是这一部分我没有做全，我此处暂且不做笔记了，大概的思路如此，我这可以提供个gulp的js文件

```js
var gulp = require('gulp');
var minifycss = require('gulp-minify-css');
var uglify = require('gulp-uglify');
var htmlmin = require('gulp-htmlmin');
var htmlclean = require('gulp-htmlclean');
var imagemin = require('gulp-imagemin');
var babel = require('gulp-babel');

// 压缩css文件
gulp.task('minify-css', function (done) {
    return gulp.src('./public/**/*.css')
        .pipe(minifycss())
        .pipe(gulp.dest('./public'));
    done();
});

// 压缩html文件
gulp.task('minify-html', function (done) {
    return gulp.src('./public/**/*.html')
        .pipe(htmlclean())
        .pipe(htmlmin({
            removeComments: true,
            minifyJS: true,
            minifyCSS: true,
            minifyURLs: true,
        }))
        .pipe(gulp.dest('./public'));
    done();
});

// 压缩js文件
gulp.task('minify-js', function (done) {
    return gulp.src(['./public/**/*.js', '!./public/**/*.min.js'])
        .pipe(babel({
            //将ES6代码转译为可执行的JS代码
            presets: ['es2015'] // es5检查机制
        }))
        .pipe(uglify())
        .pipe(gulp.dest('./public'));
    done();
});

// 压缩 public/images 目录内图片(Version>3)
gulp.task('minify-images', function (done) {
    gulp.src('./public/images/**/*.*')
        .pipe(imagemin([
            imagemin.gifsicle({interlaced: true}),
            imagemin.jpegtran({progressive: true}),
            imagemin.optipng({optimizationLevel: 5}),
            imagemin.svgo({
                plugins: [
                    {removeViewBox: true},
                    {cleanupIDs: false}
                ]
            })
        ]))
        .pipe(gulp.dest('./public/images'));
    done();
});

//4.0以后的写法
// 执行 gulp 命令时执行的任务
gulp.task('default', gulp.series(gulp.parallel('minify-html', 'minify-css', 'minify-js', 'minify-images')), function () {
    console.log("----------gulp Finished----------");
    // Do something after a, b, and c are finished.
});

```

#### butterfly的使用

这个主题配置简单的很，直接github上面搜，他的readme文档上讲的非常清楚，万变不离一，慢慢摸索。

一个小提示，万物皆是Markdown，不会的操作啥的直接点击右边联系我，或者评论都可以帮助你解决

#### 域名

域名需要先买个，腾讯云的.com.club等，可以整个.org的域名更专业点。我的友链那个我公司大哥的域名就是.org，去年7八月份国内就取消了org的域名购买，所以只能翻墙了，亲，翻墙不仅能看p站还能购物哦

配置嘎嘎简单

我这直接用腾旭云演示了，上图：

![image-20220815145545439](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815145545439.png)

github配置下自己的域名即可：

![image-20220815145700099](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815145700099.png)

如果配置完这些内容生成了CNAME文件则不需要手动进行创建，如果没有，则需要在source目录进行手动创建CNAME文件里面填入自己的域名

![image-20220815145833076](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815145833076.png)

在_config.yml文件中进行配置为自己的域名

```yaml
url: https://zhonghanlu.club/
root: /
```

配置完即可！！！



目前就这些就可以愉快的编写博客啦！！！

写的很匆忙，欢迎指正补充，评论区见。

没备案嗷，谨慎操作嗷！！！

![image-20220815150100000](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220815150100000.png)



