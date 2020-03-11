---
title: callback - javascript
layout: post
---

## 콜백함수
> 콜백함수란 특정함수의 인자로 넘겨서 코드내부에서 호출되는 함수,
혹은 어떤 이벤트가 발생했거나 특정 시점에 도달했을때 호출되는함수

{% highlight js %}

//간단한 콜백 예시
function first(callback)
    setTimeout(function(){
        console.log(1); // 1이 찍히고 나서
        callback(); // 파라미터로 넘겨받은 콜백함수 second를 실행함
    }, 1000);
}

function second() {
    console.log(2); 
}

first(function(){
    second();
})

{% endhighlight js %}

