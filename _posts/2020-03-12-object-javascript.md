---
title: Object - javascript
layout: post
---

## 객체의 프로퍼티 설정하기 : Object.defineProperty

{% highlight js %}
// obj는 객체의 참조
// "name"은 프로퍼티 이름
// 프로퍼티 디스크럽터의 참조
// 실행하면 수정한 객체의 참조를 반환함


var obj = {};
Object.defineProperty(obj, "name", {
    value: "Tom",
    writable: true, //false 이면 name프로퍼티 수정못함
    enumerable: false, // 열거 불가능
    configurable: true // 재정의 가능
});
Object.getOwnPropertyDescriptor(obj, "name");


//프로퍼티의 열거 가능 속성을 바꾸는 예제

var person = {
    name="Tom",
    age: 17,
    sayHello: function() {
        console.log(`Hello! ${this.name}`)
    }
};
Object.defineProperty(person, "sayHello", {enumerable: false}); // sayHello를 열거할 수 없도록 설정.
for(var p in person) console.log(p); // sayHello는 안찍힘


// 프로퍼티의 재정의 기능 속성을 바꾸는 예제
var person = {name: "Tom", age: 17, sex: "남"};
Object.defineProperty(person, "age", {configurable: false}); // age를 재정의할 수 없도록 설정
delete person.age; // 재정의를 못하므로 무시됨
console.log(person.age); // 17
Object.defineProperty(person, "age", {enumerable: false}); // error
// age의 enumerable 속성과 configurable 속성을 바꾸려고 하면 에러남


// 객체 상속
var person1 = { name: "Tom", age: 17 };
var person2 = Object.create(person1); // person1의 프로퍼티 상속받음
person2.name = "Sora"; 
for(var p in person2) console.log(p);


// Object.keys ( 열거할수 있는 프로퍼티 이름만 배열로 반환 )
var group = { groupName: "Tennis circle" };
var person = Object.create(group);
person.name = "Tom";
person.age = 18;
person.sayHello = function() {console.log(`Hello  ${this.name}`)};
Object.defineProperty(person, "sayHello", {enumerable: false}); // 열거불가
console.log(Object.keys(person)); //  배열로 반환

//or

var obj = { name: "Tom", age: 17 }
var p = Object.keys(obj); // p = ["name", "age"]
for(var i=0; i<p.length; i++) {
console.log( obj[p[i]] ); // 배열요소를 꺼내서 출력
}

// Object.getOwnPropertyNames ( 열거할 수 없는 프로퍼티까지 반환 )
console.log(Object.getOwnPropertyNames(person));

{% endhighlight js %}