---
title: Gulp学习笔记
date: 2019-01-18 11:21:32
tags:
---

个人理解gulp是前端开发过程中对代码进行构建的工具，是自动化项目的构建利器，可以方便我们进行项目开发的工具。

>她能自动化地完成 
javascript/coffee/sass/less/html/image/css 等文件的的测试、检查、合并、压缩、格式化、浏览器自动刷新、部署文件生成，并监听文件在改动后重复指定的这些步骤。

1. 安装
```javascript
npm install -g gulp
```
一般除了安装gulp外还会安装一些gulp的其他插件比如`gulp-uglify`,`gulp-contact`...

2. gulpfile.js

gulpfile.js是gulp的配置文件，gulp根据gulpfile.js来执行任务

在项目根目录创建一个gulpfile.js
```javascript
var gulp = require('gulp');
var uglify = require('gulp-uglify');

gulp.task('uglify', function () {
  console.log('start job!')
  gulp.src('js/app.js')
    .pipe(uglify())
    .pipe(gulp.dest('build'))
});
```
上面代码中，gulpfile.js加载gulp和gulp-uglify模块之后，使用gulp模块的task方法指定任务minify。task方法有两个参数，第一个是任务名，第二个是任务函数。在任务函数中，使用gulp模块的src方法，指定所要处理的文件，然后使用pipe方法，将上一步的输出转为当前的输入，进行链式处理。

task方法的回调函数使用了两次pipe方法，也就是说做了两种处理。第一种处理是使用gulp-uglify模块，压缩源码；第二种处理是使用gulp模块的dest方法，将上一步的输出写入本地文件，这里是build.js（代码中省略了后缀名js）。

执行minify任务时，就在项目目录中执行`gulp uglify`

3. `task()`

gulp新建任务的格式
```javascript
gulp.task(name[, deps], fn)
```
`name` 任务名字，类型：字符串；

`deps` 当前任务依赖的任务，这些任务会在你当前任务运行之前完成，类型：Array；例如
```javascript
gulp.task('mytask', ['array', 'of', 'task'], function() {
  // do something
});
```
上面指定的mytask任务由三个指定的任务组成执行mytask任务时会并发执行array，of，task三个任务，所以是`异步调用`

此外
```javascript
gulp.task('default', function() {
  // do  default job
});
```
是执行默认任务，在项目目录中输入`gulp`就会执行

4. `wacth()`

watch方法用于指定需要监视的文件。一旦这些文件发生变动，就运行指定任务。

```js
gulp.task('watch', function () {
   gulp.watch('templates/*.tmpl.html', ['build']);
});
```
上面代码指定，一旦templates目录中的模板文件发生变化，就运行build任务。

```js
watch方法也可以用回调函数，代替指定的任务。
gulp.watch('templates/*.tmpl.html', function (event) {
  console.log('file changed')
});
```

5. `gulp-load-plugins`模块
一般情况下，gulpfile.js中的模块需要一个个加载。

```js
var gulp = require('gulp'),
    jshint = require('gulp-jshint'),
    uglify = require('gulp-uglify'),
    concat = require('gulp-concat');

gulp.task('js', function () {
   return gulp.src('js/*.js')
      .pipe(jshint())
      .pipe(jshint.reporter('default'))
      .pipe(uglify())
      .pipe(concat('app.js'))
      .pipe(gulp.dest('build'));
});
```
上面代码中，除了gulp模块以外，还加载另外三个模块。

这种一一加载的写法，比较麻烦。使用gulp-load-plugins模块，可以加载package.json文件中所有的gulp模块。上面的代码用gulp-load-plugins模块改写，就是下面这样。

```js
var gulp = require('gulp'),
    gulpLoadPlugins = require('gulp-load-plugins'),
    plugins = gulpLoadPlugins();

gulp.task('js', function () {
   return gulp.src('js/*.js')
      .pipe(plugins.jshint())
      .pipe(plugins.jshint.reporter('default'))
      .pipe(plugins.uglify())
      .pipe(plugins.concat('app.js'))
      .pipe(gulp.dest('build'));
});
```
当然，这么做的前提是`node_modules`里要先安装依赖

- [gulp官方网址](http://gulpjs.com)
- [gulp插件地址](http://gulpjs.com/plugins)
- [gulp 官方API](https://github.com/gulpjs/gulp/blob/master/docs/API.md)
- [gulp 中文API](http://www.ydcss.com/archives/424)


