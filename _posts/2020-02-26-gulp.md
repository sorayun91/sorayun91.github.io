---
title: Gulp4 setting
layout: post
tags:
- gulp
- gulp4
- gulp setting
---

# Gulp4로 세팅하기

### SPA가 아닌 일반 레거시 프론트개발 환경에서는 걸프가 좀더 쉽고 편리한것같다
#### 사전조건은 nodejs가 설치되어있어야함 https://nodejs.org/ko/ 에서 다운로드 가능하며 안정적인버전으로 다운로드함.

##### 1. 우선 터미널을 열어서 폴더하나를 만들자. 나는 gulp-test라고 만들었다.
> mkdir gulp-test

##### 2. 해당폴더로 가서 package.json을 생성한다 (package.json은 npm에 의한 프로젝트 의존성 모듈설정파일이다.)
> npm init

* name, version은 필수항목인데 나중에도 수정가능하므로 엔터엔터 쳐서 넘어간다.
* script는 run 실행 명령어를 정의하는거고
* dependencies는 npm 으로 모듈을 설치하면 자동으로 추가가된다.
* dependencies가 있고 devDependencies가 있는데 어떤 라이브러리가 프로젝트의 컴파일(빌드) 타임에 필요하면 devDependencies에 넣고, 
런타임에도 계속 쓰이는 것이면 dependencies에 넣어야 한다고함. 왠만한건 다 개발에 쓰이는것이므로 dev에 추가하면될것같음.


##### 3. 걸프 전역에 설치
> npm install -g gulp


##### 4. 걸프 로컬디렉토리에 설치 
( --save-dev옵션을 주면 devDependencies에 추가됨 줄여쓰면 -D)
> npm install --save-dev gulp 

![npm](/images/posts/npm.jpg)
###### npm 설치하다보면 위처럼 경고가 뜨는경우가 있는데 무시해도됨

##### 5. 필요한 패키지 설치

> npm install --save-dev gulp-concat gulp-uglify gulp-watch gulp-minify-css gulp-connect gulp-sass gulp-sourcemaps del @babel/register @babel/core @babel/preset-env gulp-babel

* @babel/register @babel/core @babel/preset-env gulp-babel : es6를 es5로 컴파일해줌
* gulp-concat: 파일 하나로 합침
* gulp-uglify: js파일 난독화, 압축 
* gulp-watch: 실시간 감지
* gulp-minify-css: css 압축
* gulp-connect: 웹서버띄우고, 파일 새로고침기능
* gulp-sass: scss를 css로 컴파일
* gulp-sourcemaps: 소스맵(ex 에러났을때 컴파일되기전 어떤파일에서 에러났는지 알수있음)
* del: 빌드할때 기존 빌드파일삭제해줌

##### 6. 프로젝트 최상단에 .babelrc 파일생성해서 아래 소스 넣어줌

>{
   "presets": ["@babel/preset-env"]
 }

##### 7. 프로젝트 최상단에 gulpfile.babel.js 파일생성
{% highlight js %}
const gulp = require('gulp');
const connect = require('gulp-connect');
const del = require('del');
const minificss = require('gulp-minify-css');
const concat = require('gulp-concat');
const sass = require('gulp-sass');
const sourcemaps = require('gulp-sourcemaps');
const babel = require('gulp-babel');
const uglify = require('gulp-uglify');

const src = 'publish';
const dist = 'dist';

const paths = {
    js: src + '/**/*.js',
    css: src + '/css/**',
    scss: src + '/scss/*.scss',
    html : src + '/**/*.html',
    img : src + '/img/**',
    font : src + '/font/**'
};

export const clean = () => del([ 'dist' ]);

function gulpJs() {
    return gulp.src(paths.js) //개발코드 위치
        .pipe(babel()) // es6 -> es5로 컴파일
        .pipe(uglify()) // js난독화
        .pipe(concat('/front-1.0.0-min.js')) //파일 하나로합침
        .pipe(gulp.dest(dist + '/js')) // dist에 복사
        .pipe(connect.reload()); //변경되면 실시간 새로고침
}

function scss() {
    return gulp.src(paths.scss) //개발코드 위치
        .pipe(sourcemaps.init()) // 소스맵 초기화
        .pipe(sass()) // 사스로 컴파일
        .pipe(minificss()) //코드 압축하고
        .pipe(concat('/front-1.0.0-min.css'))  //파일 하나로합침
        .pipe(sourcemaps.write('.',{includeContent: true})) // 소스맵생성
        .pipe(gulp.dest(dist + '/css')) // dist에 복사
        .pipe(connect.reload()); //변경되면 실시간 새로고침
}

function html() {
    return gulp.src(paths.html) //개발코드 위치
        .pipe(gulp.dest(dist)) // dist에 복사
        .pipe(connect.reload()); //변경되면 실시간 새로고침
}


function font() {
    return gulp.src(paths.font) //개발코드 위치
        .pipe(gulp.dest(dist + '/font')) // dist에 복사
        .pipe(connect.reload()); //변경되면 실시간 새로고침
}

function image() {
    return gulp.src(paths.img) //개발용 이미지 위치
        .pipe(gulp.dest(dist + '/img')) // dist에 복사
        .pipe(connect.reload()); //변경되면 실시간 새로고침
}

function server() {
    connect.server({
        root : './',
        livereload : true,
        port : 9000
    });
}

function watcher() {
    gulp.watch(paths.js, gulp.series(gulpJs));
    gulp.watch(paths.scss, gulp.series(scss));
    gulp.watch(paths.html, gulp.series(html));
    gulp.watch(paths.img, gulp.series(image));
}

const build = gulp.series(clean, gulp.parallel(gulpJs, html, scss, font, image, watcher, server));

exports.default = build;
{% endhighlight %}

##### 8. gulpfile.babel.js  gulp task돌림

gulpfile.babel.js 오른쪽마우스 클릭후 show gulp tast클릭하면 아래와같이 tast가 나옴

![gulp](/images/posts/gulp.jpg)

##### 9. gulp run 

그러면 dist폴더에 빌드가 완료된 파일들이 나오게된다.

![dist](/images/posts/dist.jpg)