---
layout: post
title:  "Useful Gulp Plugin"
date:   2015-09-20 00:55:37
categories: Article
---

Gulp is a famous task automation tool in node community. Unlike Grunt which depend heavily with configuration and temp file,
Gulp uses stream to perform and chaining a task.

Right now, I'm not writing about how Gulp work but below is some gulp plugin and sample how to use it in your gulpfile.js

<h3>
 Browser-Sync http://www.browsersync.io/
</h3>
<p>
 Seems to be a non stop synchronised browser testing framework. It has a lots of nice of features like simple http server,
 live reload and mirrored multiple browsers so that your action like scroll, click, and refresh are mirrored between multiple
 browsers while you test.
</p>
<pre>
gulp.task('browser-sync', function() {
 browserSync.init({
     server: {
         baseDir: "./"
     },
     port: 8080,
     files: ["*/**/*.*"]
 });
});
</pre>
<h3>Nodemon</h3>
<p>
 Watch and restart node server automatically for you
</p>
<h3>
 wiredep + gulp-inject
</h3>
<p>
 inject your bower file and your custom javascript/css.
</p>
<pre>
var gulp = require('gulp');
var inject = require('gulp-inject');

gulp.task('index', function () {
var target = gulp.src('./src/index.html');
// It's not necessary to read the files (will speed up things), we're only after their paths:
var sources = gulp.src(['./src/**/*.js', './src/**/*.css'], {read: false});

return target.pipe(inject(sources))
 .pipe(gulp.dest('./src'));
});
</pre>
<p>
 dont forget to add below placeholder in your index.html file
</p>
<pre>
&lt;!-- inject:js --&gt;
&lt;!-- endinject --&gt;

&lt;!-- inject:css --&gt;
&lt;!-- endinject --&gt;
         </pre>
<h3>
 JsHint + JsCs
</h3>
<p>
 Style checking and best practise javascript writing
</p>
<pre>
gulp.task('vet', function() {
 log('Analyzing source with JSHint and JSCS');
 var source = ['*/**/*.js',
                 '!node_modules/**/*.*',
                 '!3rdParty/**/*.*'
 ];
 return gulp
     .src(source)
     .pipe($.if(args.verbose, $.print()))
     .pipe($.jscs())
     .pipe($.jshint())
     .pipe($.jshint.reporter('jshint-stylish', {verbose: true}))
     .pipe($.jshint.reporter('fail'));
});

// log function
function log(msg) {
 if (typeof(msg) === 'object') {
     for (var item in msg) {
         if (msg.hasOwnProperty(item)) {
             $.util.log($.util.colors.blue(msg[item]));
         }
     }
 } else {
     $.util.log($.util.colors.blue(msg));
 }
}
         </pre>
<h3>
 List Task
</h3>
<p>
 Sometimes you wrote lots of gulp task and this plugin will show all registered gulp task
</p>
<pre>
gulp.task('help', $.taskListing);
</pre>
<h3>
 Image Minification
</h3>
<p>
 gulp-imagemin
</p>
<pre>
var gulp = require('gulp');
var imagemin = require('gulp-imagemin');
var pngquant = require('imagemin-pngquant');

gulp.task('default', function () {
 return gulp.src('src/images/*')
     .pipe(imagemin({
         progressive: true,
         svgoPlugins: [{removeViewBox: false}],
         use: [pngquant()]
     }))
     .pipe(gulp.dest('dist/images'));
});
         </pre>
<h3>
 Angular TemplateCache
</h3>
<p>
 Warm up your angular template
<p>
<pre>
var templateCache = require('gulp-angular-templatecache');

gulp.task('default', function () {
return gulp.src('templates/**/*.html')
 .pipe(templateCache())
 .pipe(gulp.dest('public'));
});
</pre>
<h3>
 Utilities
</h3>
<ul>
<li>
 Clean Up
</li>
<pre>
var del = require('del');

function clean(path, done) {
log('Cleaning: ' + $.util.colors.blue(path));
del(path, done);
}
</pre>
<li>
 gulp-if
 <p>
     Put some conditional logic in your gulp
 </p>
</li>
<li>
 gulp-util
 <p>
     Can use for logging and print a message into terminal windows
 </p>
</li>
<pre>
// log function
function log(msg) {
if (typeof(msg) === 'object') {
 for (var item in msg) {
     if (msg.hasOwnProperty(item)) {
         $.util.log($.util.colors.blue(msg[item]));
     }
 }
} else {
 $.util.log($.util.colors.blue(msg));
}
}
</pre>
<li>
 gulp-load-plugins
 <p>
    Loads in any gulp plugins and attaches them to the global scope , or an object of your choice.
 </p>
 <pre>
var $ = require('gulp-load-plugins');

// then you can call your plugin with $.pluginName
 var gulpLoadPlugins = require('gulp-load-plugins');
</pre>
</li>
</ul>