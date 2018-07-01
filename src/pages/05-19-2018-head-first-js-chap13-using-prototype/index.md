---
path: "/head-first-js-chap13-using-prototype"
date: "2018-05-08"
title: "Head first JS Chapter 13: Using Prototype"
---

*Phần này nói về prototype-based object - một loại object khác với class-based của Java hay C++ (mấy thứ mà mình không biết đó)*

Tưởng tượng ta có một object constructor Dog khiểu như thế này

```javascript
function Dog(name, breed, weight) {
    this.name = name;
    this.breed = breed;
    this.weight = weight;
    this.bark = function() {
        if(this.weight > 25) {
            alert(this.name + " says Woof!");
        } else {
             alert (this.name + " say Yip!");
        }
    };
}
```

Nó có 3 properties (name, breed và weight) và một thuộc tính (bark). Giờ tạo ra 3 object như sau:

```javascript
var fido = new Dog('Fido', 'Mixed', 38);
var fluffy = new Dog('Fluffy', 'Poodle', 30);
var spot = new Dog('Spot', 'Chihuahua', 10);
```

Với mỗi một object, ta có một method bark. Giả sử có tầm 1,000 object thì cũng có nghĩa là cần dùng 1,000 method bark (mỗi chó một cách sủa).
Vì thế mà giờ, ta sẽ gộp tất cả các cách sủa lại làm 1 và để ở phần *prototype*, lần sau mỗi lần ta bảo "fido" sủa, browser sẽ chỉ đến prototype tìm method bark (sủa) thay vì tìm method này ở object fido.
Giờ sách bảo làm thế này:

```javascript
function Dog(name, breed, weight) {
    this.name = name;
    this.breed = breed;
    this.weight = weight;
}

Dog.prototype.species = 'Canine';
Dog.prototype.bark = function() {
    if(this.weight > 25) {
        console.log(this.name + ' says Woof!');
    } else {
        console.log(this.name + ' says Yip!');
    }
};
Dog.prototype.run = function() {
    console.log('Run');
};
Dog.prototype.wag = function() {
    console.log('Wag!');
};
```

Okay vậy prototype rất tốt cho việc chỉnh sửa một lượng lớn object là ví dụ (instances) của một constructor nào đó. Thế nếu như chỉ chỉnh sửa một nhóm trong toàn bộ ví dụ đó thì sao. Giả sử như với "Dog" là toàn loài chó thì có những giống chó hoặc một dạng chó phục vụ một mục đích nhất định cứ cho là chó diễn xiếc như sách chọn gọi là "ShowDog"
Đầu tiên là khai báo các properties giống như của `Dog()`.

```javascript
function ShowDog(name, breed, weight, handler) {
    this.name = name;
    this.breed = breed;
    this.weight = weight;
}
```
Tiếp đó là thêm property `handler` mà chỉ có `ShowDog()` có:

```javascript
    this.handler = handler;
```

Bước cuối để tạo constructor `ShowDog()` là khai báo tương tự như tạo object từ constructor:

```javascript
    ShowDog.prototype = new Dog();
```

Tuy nhiên theo DRY (don't repeat yourself) thì `ShowDog()` có lặp lại các bước tương tự như `Dog()`. Do đó ta dùng `call` method thay thế cho 3 dòng đầu khai báo properties. Viết lại như sau:

```javascript
function ShowDog(name, breed, weight, handler) {
    Dog.call(this, name, breed, weight);
    this.handler = handler;
}
```

Một người bạn bảo tôi rằng mọi thứ trong JavaScript đều là object. Có thể điều này không hoàn toàn đúng nhưng có một đoạn trong sách khiến tôi nghĩ rằng nó có lý. Cụ thể là với string ta có thể sử dụng các method build-in để thay đổi string đó. Hơn thế ta còn có thể điều chỉnh object `String` để tạo ra các method tùy ý. Ví dụ như đoạn code sau:

```javascript
String.prototype.cliche = function() {
    var cliche = ['lock and load', 'touch base', 'open the kimono'];

    for (var i = 0; i < cliche.length; i++) {
        var index = this.indexOf(cliche[i]);
        if (index >= 0) {
            return true;
        }
    }
    return false;
};
```
Khi này method `cliche` đã được thêm vào object `String`. Tuy nhiên ta lại không thể làm điều này với object `Array`