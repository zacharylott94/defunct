# Defunct
## An RFC for a language that's too fixated on functions

I am making this repository as a place to express and discuss a theoretical program language. I currently have no plans to try to implement the language described below, and I also do not possess the technical skill to even consider implementing it.

#### Your use of this repo
You, dear reader, are encouraged to participate in discussion through the use of github's issue system. There will be two main tags you will want to use: `suggestion` and `concern`. 

`suggestion` should be used for any ideas that you think would go well with the current ideas of the language. If there's a language feature that you think would fit well, write up an issue about it and use the `suggestion` tag. 

`concern` should be used for any problem you see, logically or stylistically, with the current set of ideas that make up the proposed language. If there are two presented ideas that just absolutely would not go togother and nobody else has seemed to notice the error, please open an issue describing it and use the tag `concern`.

#### The Organization of this Repo

Currently, all ideas will be here in this readme. As the concept grows (and as I explore better ways to organize things), things will be migrated elsewhere. Maybe we'll use github's wiki system. That's a thing people use, right?

#### Why are you calling it Defunt?

It sounds cool, and I think it describes how broken this language would probably be.


## Proposed Language Features

* First Class Functions
* Treat values as functions that return a value
  * example: `3` is just a function called `3` that takes no parameters and returns `3`. `3 = () -> 3`
* Functions are called without parentheses
  * concern: How would you pass the function itself?
  * concern: Is this going to turn the language into a lisp-like? 
    * `f g x` is this `f(g,x)` or `f(g(x))`?
    * In a lisp-like, everything is bounded by parentheses to remove ambiguity: `(f (g x))`. I don't like the extra parentheses.
* Partial Application/Currying is built in
* All functions technically take one or zero parameters. Partial application means a function like `f(x, y) -> x + y` is actually `f(x) -> g(y) -> x + y`
* Opt-in mutation/impurity at function and variable levels
* Built in function composition
* Strong typing, but optional type annotation with built-in generalization. ex: `f = x y -> x + y` is a function that will work for any values of `x` and `y` for which addition is defined for them.
* Unneeded parameters are ignored.
  * `x = () -> 3`. If you call this function with any parameter, that parameter is ignored. `x(3)` returns `3`.
  * concern: I don't know why I want this, but I'm convinced it could be useful.
* No references. Or, at least, opt-in references.
* Structural equality
* Arrays are functions. So are Dictionaries.
  * How is this `A[1]` any different than `A(1)`? Arrays are just functions that take an index and return a value.
* Logical operators are functions. `or`, `and`, `not`, etc are just functions that take two values.
* In general, if you can find some way to look at a feature and call it a function, it should be a function.
* No Null. The replacement is an empty value. F# calls this "Unit". All types explicitly do not include Unit. You will have to do a type Union. 
* The last line of a function is the return. No `return` keyword. you would have to explicitly return Unit. 
  * I will insist on this so that programmers don't accidentally return Unit when they did not mean to. 
  * This might be unnecessary with good static analysis/type checking.

## Psuedocode Examples
```
f = x y -> x + y
g = x -> x + 2
e = f 
a = f 1 // 1, y -> 1 + y
b = a 2 // 3 <- applied 2 to a; 1 + 2 = 3

//contains a side effect, must use 'impure'
//must explicitly return Unit if no value is returned
impure hello = () -> print "hello"; ()  

```

## Wait, you just want executable Lambda Calculus!
![yes](https://github.com/zacharylott94/defunct/raw/master/Yes.png)