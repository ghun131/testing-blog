---
path: "/head-first-js-chap9-asynchronous"
date: "2018-04-16"
title: "Head first: JavaScript chapter 9: Asynchronous Coding: Handling events"
---

Điều đầu tiên mình quan tâm đến là event handler đôi khi đc gọi là event listener. Tiếp đến là asynchronous. Trong sách có nói asynchronous là loại hàm sẽ được gọi tại bất kì thời điểm nào theo bất kì thứ tự nào.

Một điểm đáng chú ý của chương là NodeList (một tâp hợp các Nodes). Đây là kết quả của việc sử dụng method `getElementsByTagName` và điều thú vị là NodeList này có thể được sử dụng như một array. Tuy nhiên NodeList thực ra có nhiều điểm khác với array.

Phần này tập trung vào giải thích event phần nhiều để dạy mình cách xử lý event (hay cách viết event handler). Hầu hết các even là object của DOM nhưng có một số event không phải là DOM. Trên các thiết bị khác nhau thì các event này cũng khác nhau.