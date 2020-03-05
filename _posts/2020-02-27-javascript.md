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

