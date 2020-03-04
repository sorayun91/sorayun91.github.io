---
title: gulp-file-include
layout: post
tags:
- gulp
- gulp-file-include
---

## gulp로 파일 인클루드 하는법


사용법은 [gulp-file-include](https://www.npmjs.com/package/gulp-file-include) 를 참고하였다

* npm install --save-dev gulp-file-include 로 설치
* const fileinclude = require('gulp-file-include');  을 gulpfile에 추가
* 아래 소스처럼 gulpfile에 task 추가 

{% highlight js %}
function html() {
	return gulp.src(paths.html) 	    
		.pipe(fileinclude({
			prefix: '@@', //사용할땐 앞에@@ 를 붙이면됨
		}))
		.pipe(gulp.dest(dist))
		.pipe(connect.reload()); 
}
{% endhighlight %}

* 기본적인 파일인클루드 방법은 예들들면 index.html에 공통헤더와 푸터를 붙이고싶다.
1. header.html, footer.html 을 만들어서 
2. index.html에 원하는 위치에 @@include('./header.html') 이런식으로 붙이면됨

{% highlight html %}
index.html

<body>
    <div class="main">
        @@include('./header.html')
</body>
{% endhighlight %}

* 그리고 각페이지별로 분기처리를 하기위해 페이지 마다 다르게 header에 class를 주고싶다.
* 예를들면 index.html에선 header태그에 main-header클래스를 주고 sub.html에선 header태그에 sub-header클래스를 주고싶다.

1. index.html 에서 name을 넣는다.
2. header.html에서 클래스를 삽입하고싶은곳에 @@name을 넣는다.

{% highlight html %}
index.html

<body>
    <div class="main">
        @@include('./header.html', {
            "name": "main-header"
        })
</body>
{% endhighlight %}

{% highlight html %}
header.html

<body>
    <header class="header @@name">
        공통헤더
    </header>
</body>
{% endhighlight %}

* 웹루트설정(이렇게 해놓으면 나중에 루트가 변경되면 일일이 안바꿔두된다.)
{% highlight html %}
<!DOCTYPE html>
<html>
  <head>
    <link type=stylesheet src=@@webRoot/css/style.css>
  </head>
  <body>
    <h1>Support Contact Info</h1>
    <footer><a href=@@webRoot>Home</a></footer>
  </body>
  </body>
</html>
{% endhighlight %}