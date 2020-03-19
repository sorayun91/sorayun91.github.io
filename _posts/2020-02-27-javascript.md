---
title: javascript 정리
layout: post
---

## es6의 유용한 기능들

* 보간표현식

{% highlight js %}
//기존에는 문자열에 변수 값을 더할때 더하기연산자를 사용했다면
let name = 'sora';
console.log('my name is ' + name);

//보간표현식을 활용하면 좀더 편리하고 알아보기 쉽다.( ` 이렇게 생긴 백틱 안에 플레이스 홀더를 넣음 )
let name = 'sora';
console.log(`my name is ${name}`)

{% endhighlight %}

* 나머지 매개변수
함수의 인자가 들어가는 부분에 ...을 입력하면 그만큼의 인수를 배열로 받을 수 있다.
...로 표현한 인자를 나머지 매게변수라고 한다.

{% highlight js %}

function f(a, b, ...args) { // 1,2 다음의 매개변수를 배열로 받아라
    console.log(a, b, args); // 즉 args는 배열임
}

f(1,2,3,4,5,6); // 1 2 [3, 4, 5, 6]

//or

var sum = (...args) => {
    for(let i=0, s=0; i<args.length; i++) {
        s += args[i];ㅁ
    }
}
sum(1,2,3,4,5);

{% endhighlight %}


---

## 기타

* 객체 delete할때 주의점

{% highlight js %}
//delete를 하면 객체 프로퍼티를 삭제할수 있다. 하지만 메모리에는 남으므로 undefined를 선언해서 치환해야 메모리에서도 삭제됨

const person = {
    firstName: "sora",
    lastName: "yun"
}

delete person.firstName;
person.firstName = undefined;

{% endhighlight %}

---

* in연산자로 프로퍼티가 있는지 확인하기

{% highlight js %}
const person = {
    firstName: "sora",
    lastName: "yun"
}

console.log("age" in person); //false
console.log("lastName" in person); //true
{% endhighlight %}

---


* for/in 문
> 객체안의 프로퍼티를 순회하는 반복문 / 
for (변수 in 객체표현식) 문장 / 
객체표현식이 null 또는 undefined이면 빠져나옴

{% highlight js %}

 let obj = {a:1, b:2, c:3};
 for (let p in obj) {
     console.log(`p = ${p}`);
 }
 
 /*
 p = a
 p = b
 p = c
 
 프로퍼티 값만 가져와서 p에 대입함
 따라서 프로퍼티값을 가져오려면 
 
 obj[p] 로 접근함
 
 */
 
  let obj = {a:1, b:2, c:3};
  for (let p in obj) {
      console.log(`obj.${p} = ${obj[p]}`);
  }
  
   /*
   obj.a = 1
   obj.b = 2
   obj.c = 3
   */
 

{% endhighlight %}

---

* 즉시실행함수

{% highlight js %}

//일반적인 익명함수
let f = function() {...}
f();

//즉시실행함수로 쓰면
(function() {...})();


//or
(function() {...}());

//인수를 넘길땐
(fuction(a,b) {...})(1,2);

//함수표현식 (함수실행결과를 변수에 할당함)
let x = (function() {...})();

//화살표함수의 즉시실행함수
(x => x*x)(3); // 9

{% endhighlight js %}

---

* undefined 체크하는 가장좋은 방법

 {% highlight js %}
 
 typeof x === 'undefined'
 
 {% endhighlight js %}
 
 ---
