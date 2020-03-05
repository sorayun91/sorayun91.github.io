---
title: timer-javascript
layout: post
tags:
- 타이머함수
- settTimeout
- setInterval
- clearTimeout
- clearInterval
---

## javascript timer 함수

* setTimeout - 지정된시간이 흐른후 실행함수
{% highlight js %}
setTimeout(function() {
    console.log(new Date());
}, 2000)

//or 첫번째 인수로 문자열로 넘기면 내부적으로 eval()로 평가 후 실행됨
setTimeout("console.log(new Date())", 1000)

{% endhighlight js %}

---

* clearTimeout - setTimeout이 반환하는값을 clearTimeout의 인수로 넘겨서 실행취소
{% highlight js %}
var timer = setTimeout(function() {
    console.log(new Date());
}, 2000)
...
clearTimeout(timer)
{% endhighlight js %}

---

* setInterval - 지정된 시간마다 반복해서 실행
{% highlight js %}
setInterval(function() {
    console.log(new Date());
}, 1000)

//or 첫번째 인수로 문자열로 넘기면 내부적으로 eval()로 평가 후 실행됨
setInterval("console.log(new Date())", 1000)

{% endhighlight js %}

---

* clearInterval - setInterval의 반환값을 clearInterval의 인수로 넘겨서 실행취소
{% highlight js %}
var timer = setInterval(function() {
    console.log(new Date());
}, 1000)
...
clearInterval(timer); 

{% endhighlight js %}