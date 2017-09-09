### 使用方法

静态多页面实现模块化开发的推荐方案。

demo：[http://liumin.win/new-gulp-swig/](http://liumin.win/new-gulp-swig/)

安装依赖

```
yarn add 或者 npm install

bower install
```

启动项目

```
gulp serve
```

编译打包

```
gulp build
```


测试模板编译任务可用性

```
gulp tempaltes
```

我修改了gulpfile.js的哪里

```
// 新增模板编译任务
var swig = require('gulp-swig');
gulp.task('templates', function() {
  var YOUR_LOCALS = {};
  gulp.src('app/src/*.html')
      .pipe(swig({
        load_json: false,
        defaults: {
          cache: false
        }
      }))
    .pipe(gulp.dest('app'))
});

// 将任务分别加入到gulp各个流程
gulp.task('build', ['templates', 'lint', 'html', 'images', 'fonts', 'extras'], () => {
  return gulp.src('dist/**/*').pipe($.size({title: 'build', gzip: true}));
});
...
  runSequence(['clean', 'wiredep'], ['templates', 'styles', 'scripts', 'fonts'], () => {
...
    gulp.watch('app/src/**/*.html', ['templates']);
...

```
