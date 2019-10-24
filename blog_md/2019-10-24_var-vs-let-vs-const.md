# [JavaScript] `var` vs `let` vs `const`

> *What's the different anyway?*

This week I have a great time to learn JavaScript for the first time.

Well, it's not quite correct though. First time I know about JavaScript is because [Daniel Shiffman](https://www.youtube.com/user/shiffman). He's an awesome guy who use p5 to create an awesome project! Go check them out.

Okay, so I stumble upon to this kind of confusion. In Python, there's no such thing as variable declaration in Python! [^1] But it's the only exception though since I think almost all programming languages are have some sort of mechanism to declare a variable. In JavaScript, however, there's some weirdness that I found.

First, before ES6, all programmer use `var` to declare a variable. So, it's should look like `var num = 6`. But after ES6, now we can use `let` and `const`. What's the different anyway?

If you're an Indonesian speaker, probably you'll find [this article](https://medium.com/coderupa/es6-var-let-const-apa-bedanya-1cd4daaee9f0) kinda great to explain all of them. But it's exhaustive list, we just want the gist of it. So here's the table from the the article.

![img](https://miro.medium.com/max/615/1*sUBeBuOB8pAuMPfw9BQmvA.png)

Let's dissect for each terms:

***Redeclare***: you can declare as many as you want with `var`, but it's not the case on the others.

```javascript
// you can do this with no error whatsoever
var myName = 'Markus';
var myName = 'Suwignyo';

// but you can't do this in let
let myName = 'Markus';
let myName = 'Suwignyo'; // error!

// and also in const
const myName = 'Markus';
const myName = 'Suwignyo'; // error!
```

So why should I care? Well technically you shouldn't but think about this way. What's the purpose of redeclaring a variable anyway? 

If you can't find the answer, well welcome to `let` and `const`. 

***Hoisting***: you can use the variable **before** you declare it. In `var` this is possible, but the others, again, it's not.

```javascript
// you can do this with no error whatsoever
console.log(myName);
var myName = 'Suwignyo';

// but you can't do this in let
console.log(myName2); // error!
let myName2 = 'Suwignyo';

// and also in const
console.log(myName3); // error!
const myName3 = 'Suwignyo'; 
```

Again, you ask why should I care? Well, isn't it a bit of weird when you can use something that doesn't exist yet? In JavaScript, here's what's going on when you use `var` variable before you declare it.

```javascript
// each time you code like this
console.log(myName);
var myName = 'Suwignyo';

// the truth is, the interpreter change your code into like this
var myName = undefined;
console.log(myName);
var myName = 'Suwignyo';
```

This kind of feature is seriously confusing if you work on numerous project. Besides, it's not a good practice as suggested by Daniel Brain. [^2] 

***Block scope***: mean your variable is limited for use only on certain block that contains it's declaration. It's true when you use `let` and `const`, but not `var`. Let's see my code:

```javascript
// you can do this in var
for (var i = 0; i < 10; i++) { }
console.log(i); // will output 10

// but you can't do this in let
for (let i = 0; i < 10; i++) { }
console.log(i); // will output 10

// and const
for (const i = 0; i < 10; i++) { }
console.log(i); // will output 10
```

The variable `i` is declared in `for` block. But whenever you use `var` to declare `i`, it's become available inside and outside the block.

How about `let` and `const`? Both actually declared **inside** the block, so whenever you want to use the variable, you have to use it inside the `for` block, not on the outside of it. 

If you have a bull's eyes, you might notice that `let` and `const` have a different error message. `let` is enabling you to reassign the variable more than one, so in this case, `i` will get `0` up to `10`. But still, you can't use it outside the block.

That's quite different with `const`. `const` is a abbreviation from *constant* mean that it's static. Once you declare and initiate it, you can't reassign it anymore. So, in this case, `i` will hold `0` and never beyond that.

***Create global props***: this is a special property only for `var` and I've explained it before that `var` can be redeclare and reassign multiple time, and can be used globally (no matter the scope is).

## Conclusion

So that's it! Which one did you prefer? Should I use `var`, `let`, or `const`? For me personally: I'll never use `var` again. The only reason for this is because you can use `var` globally no matter the scope is. And it's really really bad.

I use Python almost two years, and the way they handle variable is to make it *locally available*. There's no such thing as global variable in Python. So that's why when I use JavaScript for the first time, I have this some sort of leaning towards `let` and `const` because it's more maintainable. 

For now, I use `let` constantly to replace `var`. Special case when I need a constant value that shouldn't change at all, then I'll use `const`. All and all, please avoid `var`!



[^1]: https://www.python-course.eu/variables.php
[^2]: https://medium.com/@bluepnume/theres-no-need-to-define-all-javascript-vars-once-at-the-top-of-a-function-and-there-hasn-t-been-a66b31f21822