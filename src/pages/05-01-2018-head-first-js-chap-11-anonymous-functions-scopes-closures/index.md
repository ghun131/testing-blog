---
path: "/head-first-js-chap11-anonymous-functions-scopes-closures"
date: "2018-05-01"
title: "Head first JS Chap 11: Anonymous functions, Closures, Scope and Serious Function"
---

1.
Phần đầu chap này hứa rằng mình sẽ biết một vài 'common coding idioms' và hai khái niệm **anonymous function** và **closure** được nhấn mạnh.
**Anoynymous function** là các hàm không tên, cái này không có gì lạ cả. Sách mất một đoạn giới thiệu loại hàm này. Tiếp đến là khái niệm **hoisting** nghĩa là dùng **function declaration** bất kì đầu trong code thay vì viết **function expression** ở trên đầu.

Mọi thứ có vẻ không có gì thú vị cho đến khi có một câu hỏi. So sánh hai đoạn code sau và giải thích sự khác biệt:

####Specimen #1
```javascript
var secret = '007';

function getSecret() {
    var secret = '008';

    function getValue() {
        return secret;
    }
    return getValue();
  }
var getValueFun = getSecret();
getValueFun;
```
####Specimen #2
```javascript
var secret = '007';

function getSecret() {
    var secret = '008';

    function getValue() {
        return secret;
    }
    return getValue;
  }
var getValueFun = getSecret();
getValueFun();
```
Cả hai đoạn code này đều cho cùng một kết quả, khác nhau chỉ la Speciment #1 không return `getValue()` (chắc tại cái ngoặc tròn làm nó bị vô hiệu hóa) mà chỉ return giá trị của `secret`. Do vậy lúc đặt `var getValueFun = getSecret()`, giá trị của `getValueFun` là giá trị của `secret` (hay là chuỗi `"008"`). `getValueFun` giờ là một string.
Tuy nhiên với Seciment #2 thì `getValue` được return nên việc đặt `var getValueFun = getSecret();` giống như đặt hàm `getValue()` là `getValueFun`. Lúc này `getValueFun` là một hàm chứ ko phải một chuỗi như ở Speciment #1, do đó để gọi `getValueFun` thì phải có ngoặc tròn ở cạnh.

2.
**Closure** là một khái niệm được sách nói là phức tạp nhưng quan trọng. Sách có định nghĩa nó là một hàm đồng nhất với môi trường tham chiếu. Khi đó ta nói hàm đó được *closed* hay đã có một *closure*.

*Dù tự tay viết ra mình vẫn chả hiểu nó là gì, thôi thì chỉ quan tâm xem nó giúp ích được gì và dùng như thế nào*

*Closure* có giá trị để hạn chế sử dụng biến *global*, ví dụ như khi này

```javascript
var count = 0;

function counter() {
    count = count + 1;
    return count;
}
```
Thực ra đoạn code này không có vấn đề gì cả, chỉ là khi làm việc nhóm có thể có nhiều người cùng chọn tên biến là "count". Do vậy nên để biến này là *local*. Sách có hướng dẫn một cách tiếp cận:
```javascript
function makeCounter() {
    var count = 0;

    function counter() {
        count = count + 1;
        return count;
      }
    return counter;
}
```
Và thế là chúng ta có *closure*. Nói ngắn gọn là ta dùng cho tất cả vào hàm `makeCounter` để rồi return lại hàm `counter` sau này dùng.
Cách thứ hai để có *closure* là khi ta dùng một hàm ở trong một hàm khác để xử lý biến tự do (hay biến *local*). Ví dụ như
```javascript
function makeTimer(doneMessage, n) {
    setTimeout(function() {
            alert(doneMessage);
    }, n);
}
```
`doneMessage` là một biến tự do trong khi `function() { alert(doneMessage)}` là một hàm được truyền vào `setTimeout`. Vậy là ta đã có *closure*

Chương này còn nói đến những cái như *Lexical scope* và *free variables*. Đoạn đầu có đề cập đến *nested function*. Chung quy lại với người mới nhập môn như mình những thứ này rất có ích để đọc code đỡ khó chịu và có thể làm quen với syntax của ES6 dễ hơn.