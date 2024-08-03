---
title: 静态文件缓存方案
date: 2020-11-08 13:07:14
updated: 2020-11-08 13:07:14
tags:
categories:
---


优化网站性能的一种途径是优化静态资源性能，优化静态资源性能有以下几种途径：
CDN；压缩js，css，图片体积；通过http头使浏览器缓存静态资源 我的网站采用的方案是压缩js和css，然后设置http头缓存静态资源

首先设置http头让浏览器缓存
```
Cache-Control:max-age=315360000, public
Expires:Thu, 31 Dec 2037 23:55:55 GMT
```

上面的http头是静态文件意思缓存1年（3652460*60），2037年23时55分55秒过期。 这样浏览器就不会重新从服务器下载这里静态资源。

chrome Network截图

如图上面显示(form disk cache)因为不走网络所以占用的时间非常少，我的网站本来就是部署在还美国的主机，流量本来就很慢，所以静态资源缓存可以优化网站性能。 静态文件缓存做好了，接下来是在文件修改之后通知浏览器下载更新的文件。 我现在是用构建工具group来处理的，用它来压缩js、css文件，还有计算它们的md5值用来重命名文件名，这样就可以确保不同的内容有独一无二的文件名了。 group基于node.js所以必须先安装node.js，然后安装group。 安装grount-cli
``` bash
npm install -g grunt-cli
```
安装成功 在你需要你项目package.json的devDependencies里面添加grunt需要依赖
```
"grunt": "",
"grunt-contrib-cssmin": "^2.0.0",
"grunt-contrib-levin-usemin": "",
"grunt-contrib-uglify": "^2.2.0",
"grunt-rev": "",
"html-webpack-plugin": "^2.28.0"
```
然后
``` bash
npm install
```
我的Gruntfile.js是
``` javascript
// javascript
module.exports = function(grunt) {
    grunt.initConfig({
        rev: { // 配置任务rev 计算js和css文件的md5值并重命名
            options: {
                encoding: 'utf8',
                algorithm: 'md5',
                length: 8
            },
            assets: {
                src: [
                 'public/javascripts/**/*.js', // 目标js文件
                 'public/stylesheets/**/*.css', // 目标css文件
                ]
            }
        },
        usemin: {
            css:{
                files:{
                    src:['public/stylesheets/**/*.css']
                }
            },
            js:['public/javascripts/**/*.js'],
            html:['views/**/*.ejs'],
            options:{
                assetsDirs: ['static', 'public/'],
                patterns: {
                    js: [[/(\\/public\\/images\\/[\\/\\w-]+\\.jpg)/, 'replace image in js']]
                }
            }
        }
    });

    grunt.loadNpmTasks('grunt-rev'); // 引入grunt的插件 ‘grunt-rev’
    grunt.loadNpmTasks('grunt-contrib-levin-usemin'); // 引入grunt的插件 ‘grunt-contrib-levin-usemin’

    grunt.registerTask('default', ['rev', 'usemin']); // 注册任务default，default任务列表里有2个任务rev和usemin
};
```