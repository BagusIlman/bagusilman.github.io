---
layout: post
title:  "Using Gulp"
date:   2015-09-22 00:55:37
categories: Article
---

In previous article I blog about some gulp plugins that I use in my project.
Now I want to share what is gulp and how to use it.

Gulp is a streaming build system, what I mean by streaming is it uses file stream for all of it file manipulation.
It will not write file in disk unless you tell it.

The gulp api is ridiculously light and simple. It contain only 4 functions.

1. gulp.task
2. gulp.src
3. gulp.dest
4. gulp.watch

**gulp.task** is for defining your tasks.
{% highlight javascript %}
gulp.task('taskname', function() {
  //do stuff
});

{% endhighlight %}

If your task have dependencies, you can specify it in array and
your task will be executed after all dependencies are done

{% highlight javascript %}
gulp.task('taskName', ['dependencies'], function() {
  //do stuff after all dependencies is done
});
{% endhighlight %}

In console or terminal windows you can type
**gulp taskname**
To execute your task or if your task is named as *default* you just can type **gulp**
to execute the task

**gulp.src** will grab your files and convert it to stream. It uses **.pipe** for chaining it’s output into other gulp plugins.

**gulp.dest** will convert your stream into file and write it to disk.

Below is a sample task that copy+paste files into other directory.

{% highlight javascript %}
gulp.task('copyHtml', function() {
  // copy any html files in source/ to public/
  gulp.src('source/*.html').pipe(gulp.dest('public'));
});
{% endhighlight %}

**gulp.watch** is uses to watch files. when any files are changes, it will perform tasks described


{% highlight javascript %}
gulp.watch('source/javascript/**/*.js', ['jshint']);
{% endhighlight %}

Sample above will watch all .js files in source/javascript and execute jshint
if any of that files are changes.