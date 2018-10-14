---
path: "/udemy-react-the-complete-guide9"
date: "2018-07-26"
title: "Udemy React the complete guide ninth day"
---

Well just to not confuse my future me, this is precisely not ninth day due to the fact that this course has taken me quite a long time since the first day of Facebook Community Challenge Hackathon until now. However, this is the ninth day that I update my notes.
1. The teacher - Max is such an awesome guy. He explains every step that he takes to overcome even the most simple task. And I am absolutely in awe to see his understanding of the runtime of this app.
2. So in video 165 from chapter 10, Max created a `higher order component` and somehow wrap it around another component. How can he do that? And in which situations that I can do the same? Why does he do it anyway? What are the alternatives?
3. I may want to work on the `request` object of `axios` because it seems that I don't get the reason why he needs to use it here.
4. There is a fascinating problem that Max proposes in lecture 167 of this chapter. So we use 2 `interceptors` for one particular `axios` instance in a *higher order component* named `withErrorHandler`. But things will get out of hand when we later add `Router` and reuse `withErrorHandler` because these interceptors will be called multiple times and stay there. The best scenario is that they eat up memory and in the worst, they create some complicated bugs.