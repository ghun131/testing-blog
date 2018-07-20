---
path: "/udemy-react-the-complete-guide7"
date: "2018-07-18"
title: "Udemy React the complete guide seventh day"
---

So for the past three days, I have dived into the HTTP request in chapter 9 of this course mostly because it is the biggest question I've had in mind for some time:"How to handle HTTP request?". And now I have the answer.
Anyway I tried to work with some simple APIs that don't require token or authorization (By the way these things would be my future goals) and it turned out pretty well and exciting.
So today I get back on track with the normal flow of the course. It is chapter 8 - a real project that build a burger.
1. One thing that I should notice here is this code
```javascript
import React from 'react';

const layout = (props) => (
    <div>Toolbar, SideDrawer, Backdrop</div>
    <main>
        {props.children}
    </main>
);
```
It makes an error message because we have an JSON-JSX element. There are three solutions for this situation. 
- Firstly, we can return an array and give each items a key by replacing the `()` with `[]`. Quite ridiculous but true.
- The second solution is to wrap the content with a **Auxilliary higher order component**. It will immediately output the content. Basically it goes like this:
```javascript
import React from 'react';

import Aux from '../../hoc/Aux;

const layout = (props) => (
    <Aux>
        <div>Toolbar, SideDrawer, Backdrop</div>
        <main>
            {props.children}
        </main>
    </Aux>
);
```
It has worked so far but I'm not sure why my lecturer avoid using the third option.
- We use `<div></div>` tag to wrap the content instead of `<Aux></Aux>`.