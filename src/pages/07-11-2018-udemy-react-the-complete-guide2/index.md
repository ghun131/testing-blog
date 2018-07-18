---
path: "/udemy-react-the-complete-guide2"
date: "2018-07-11"
title: "Udemy React the complete guide second day"
---

This course is amazing and I have always had intention to marathon to Redux, s this time it must be true since I don't have much time left before finishing the product for the Hackathon.

Few things I want to quickly jot down to remind me:
- `()` is used when you want the function to be executed immediately when runtime starts.
- We shouldn't change `state` in many components because it would cause weird behaviors, use `props` instead.
- Methods can be passed as `props` so state only stay in few components.
- If you have to choose between `() => this.switchNameHandler('Maximilian')` and `this.switchNameHandler.bind(this, 'Maximilian')` inside curly braces, you should choose the later. With a bigger scope of the app, the first approach can be inefficient.
- Handle content of the `input` is very complicated. Just a simple update-per-keystroke input field requires decent amount of work for me.
- It has been not until now I know that styling in one component by using its tag name may change the style of the same tag in another component. 