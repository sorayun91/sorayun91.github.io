---
title: Mixin - javascript
layout: post
---

>  믹스인이란 특정객체에 다른객체의 프로퍼티를 붙여넣는 기법
obj1 에 obj2를 붙여넣기 한다고 보면된다.

{% highlight js %}
// 얕은복사(객체의 복사본을 만드는데 그객체의 참조만 복사함. 이렇게되면 
원본과 사본이 같은객체를 참조하게된다.)
function mixin(target, source) {
    for(var property in source) {
        if(source.hasOwnProperty(property)) {
            target[property] = source[property];
        }
    }
}

var obj1 = {a:1, b:2};
var obj2 = {b:3, c:4};
var obj = mixin(obj1, obj2);
// obj는 {a:1, b:3, c:4};

// 좀더 완전한 mixin함수
function mixin(target, source) {
    var keys = Object.keys(source); // source의 프로퍼티의 이름을 배열로 만듬
    for(var i=0; i<keys.length; i++) {
        var descriptor = Object.getOwnPropertyDescriptor(source, keys[i]); // 각프로퍼티의 디스크립터를 구함
        Object.defineProperty(target, keys[i], descriptor); // 타깃 객체에 새로운 프로퍼티를 추가함
    }    
    return target;
}

var person1 = {
    _name: "Tom",
    get name() {
        return this._name;
    }
};
var person2 = {};
mixin(person2, person2);
person2.name = "Sora";
console.log(person2.name); // Tom -> 값을 대입해도 바뀌지않았음.
console.log(person2); // Object {_nmae="Tom"}

{% endhighlight js %}

