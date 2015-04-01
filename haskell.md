# Haskell

**date 20140715-15:15**

**tags haskell**

This note is taken following Haskell online tutorial: [[http://learnyouahaskell.com/][Learn You a Haskell for Great Good : A Beginner's Guide]].


# Chapter 2 Starting Out

### Open Haskell

Type `ghci` in terminal.

The prompt is `Preclue`, but it can get longer when you load stuff into the session. (?? what does this mean ??)

type `:set prompt "ghci> "` to change prompt sign (it can be anything you would like).


### Simple arithmetic and functions

```
ghci > 5 + 4.0
9.0
```

It works because 5 is skeaky and can act like an integer or a floating-point number. 4.0 can't act like an integer, so 5 is the one that has to adapt.

If the types are not match, Haskell would throw error message.

The `succ` function takes anything that has a defined successor and returns that successor.

`min` reutrns the one that's lesser and `max` returns the one that's greater.

Function application has the **highest** precedence of them all. `()` can be used to escalate the order of process.

```haskell
ghci> succ 9 + max 5 4 + 1
16
ghci > (succ 9) + (max 5 4) + 1
16
```

If a function takes two parameters, we can also call it as an _infix function_ by surrounding it with backticks (**`**).

```haskell
ghci > div 92 10
9
92 `div` 10
9
```

imperative language :: is a programming paradigm that describes computation in terms of statements that change a program state. In much the same way that imperative mood in natural languages expresses commands to take action, imperative programs define sequences of commands for the computer to perform. Opposite to declarative programming, which expresses what the program should accomplish without prescribing how to do it in terms of sequences of cations to be taken. Functional and logic programming are examples of a more declarative approach.

source: [http://en.wikipedia.org/wiki/Imperative_programming](http://en.wikipedia.org/wiki/Imperative_programming)


### Call function

**Space** are used for function application in Haskell, not like C to use parentheses to call function.


### How to load source file?

[http://www.haskell.org/ghc/docs/latest/html/users_guide/loading-source-files.html](http://www.haskell.org/ghc/docs/latest/html/users_guide/loading-source-files.html)

```haskell
Prelude> :cd dir
Prelude> :l filename
[1 of 1] Compiling Main        ( filename.hs, interpreted )
Ok, modules loaded: Main.
```

Then you can call function as normal.


### Write function in Haskell

Functions in Haskell **don't** have to be in any particular order.

`if` statement :

The difference between Haskell's if statement and if statements in imperative language is that the else part is mandatory in Haskell (cannot skip).

If statement in Haskell is an *expression*. 

expression :: is basically a piece of code that returns a value. Because else is mandatory, an if statement will always return something and that's why it's an expression.

*'* **doesn't** have any special meaning in Haskell's syntax. It's a valid character to use in a function name. We usually use ' to denote a strict version of a function or a slightly modified version of a function or a variable.

```haskell
doubleSmallNumber x = if x > 100 then x else x*2
doubleSmallNumber' x = (if x > 100 then x else x*2) + 1

//valid function name
conanO'Brien = "It's a-me, Conan O'Brien!"
```

##### Function 

function name **can't** begin with uppercase letter.

function doesn't take any parameters.

When a function doesn't take any parameters, we say it's a *definition* (or a *name*)

##### List

*list* in Haskell is a **homogenous** data structure. It stores several elements of the _same type_.

use `let` to define a name right in GHCI.

define list

```haskell
ghci> let lostNumbers = [4,8,15,16,23,42]
```

To put two lists together, use `++`. Haskell has to walk through the whole list on the left side of `++`. However, putting something at the beginning of a list using **:** operator is instantaneous. _Think about what operator is most suitable when putting big lists together_.

`[1,2,3]` is actually just syntactic sugar for `1:2:3:[]`. `[]` is an empty list.

`[]`, `[[]]`, `[[],[],[]]` are all different things. They are: a empty list, a list that contains one empty list, and a list that contains three empty lists.

To get an element out of a list by index, use `!!`. The indices start at 0.

The lists within a list can be of different lengths but they can't be of different types.

 - `head` returns first element, throw exception if takes empty list.
 - `tail` returns everything excepts list's first element.
 - `last` returns last element.
 - `init` returns everything excepts list's last element.
 - `length` returns list's length.
 - `null` checks if a list is empty.
 - `reverse` reverse a list.
 - `take` takes number and list and return number of elements out of that list.
 - `drop` drops that number of elements out of a list.
 - `maximum` reutrn biggest element.
 - `minimum` returns smallest element. 
 - `sum` takes a list of numbers and returns their sum.
 - `product` takes a list of number and returns their product.
 - `elem` check if it is an element of the list.
 - `cycle` takes a list and cycles it into an **infinite** list.
 - `repeat` takes an element and produces an infinite list or just that element.


**Texas ranges** 

`[1..20]` contains all natural number from 1 to 20.
`['a'..'z']` contains all lowercase letters.


##### List comprehension

```haskell
S = { 2 * x | x ∈ ℕ, x ≤ 10 }

//represent in Haskell
ghci> [x*2 | x <- [1..10]]  
[2,4,6,8,10,12,14,16,18,20]  
```

`<-` simply means _belong to_.

`stringFunction :: [Char] -> [Char]` means from a string to a string. 
When having multiple parameters, parameters are seperated with `->`.


##### Tuples /t^pl/

like lists, a way to store several values into a single value.

Tuples are used when you know exactly how many values you want to combine and its type depends on how many components it has and the types of the components.

Don't have to be homogenous, a tuple can contain a combination of several types.

Use tuple when you know in advance how many components some piece of data should have. 

More rigid. 

No such a thing as singleton tuple. 

 - `fst` takes a pair and returns its first component.
 - `snd` takes a pair and returns its second component.
 - `zip` takes two lists and then zips them together into one list. The longer list simply gets cut off to match the length of the shorter one.

```haskell
ghci> zip [1,2,3,4,5] [5,5,5,5,5]  
[(1,5),(2,5),(3,5),(4,5),(5,5)]  
```

*** Tuple comprehensions

```haskell
ghci> let triangles = [ (a,b,c) | c <- [1..10], b <- [1..10], a <- [1..10] ]
```

# Chapter 3 Types and Typeclasses

Haskell has a static type system. 

Unlike Java or Pascal, Haskell has type inference. If we write a number, we don't have to tell Haskell it's a number. It can *infer* that on its own. Don't have to explicitly write out the types of our functions and expressions to get things done.


Haskell use `:t` command to print out its type. In results, `::` is read as "has type of". **Explicit types** are always denoted with the first letter in **capital case**.

Functions also have types. When writing our own function, we can choose to give them an explicit type declaration. (good practice)

```haskell
removeNonUppercase :: [Char] -> [Char]  
removeNonUppercase st = [ c | c <- st, c `elem` ['A'..'Z']] 
```

`removeNonUppercase` has a type of `[Char] -> [Char]`, meaning that it maps from a string to a string. That's because it takes one string as a parameter and returns another as a result.

`[Char]` is synonymous with `String`. So it's clearer to write as `removeNonUppercase :: String -> String`.

The parameters are seperated with `->`. To define multiple parameters' type, write as `addThree :: Int -> Int -> Int -> Int`.

##### Types

 - `Int` : integer, 2147483647 to -2147483648
 - `Integer` : also integer, usually for very big number.
 - `Float` : real floating point with single precision.
 - `Double` : real floating point with double the precision.
 - `Bool` : boolean type, two values: `True` or `False`. 
 - `Char` : character, denoted by single quotes.

Tuples are types but they are dependent on their length as well as the types of their components. Empty tuple `()` is also a type which can only have a single value: `()`.


### Type variables

Types are written in capital case.

`a` is a **type variable**. That means that `a` can be of any type. (like generics in other language)

Functions that have type variables are called `polymorphic function`.

```haskell
ghci> :t fst
fst :: (a, b) -> a
```

just because `a` and `b` are different type variables, they don't have to be different types.


### Typeclasses

typeclass :: is a sort of interface that defines some behavior. If a type is a part of a typeclass, that means that it supports and implements the behavior the typeclass describes. 


```haskell
ghci> :t (==)                     // == is a function, called equality operator
(==) :: (Eq a) => a -> a -> Bool  // type declaration
```

Everything before <code>=></code> symbol is called a **class constraint**.

Read as: the equality function takes any two values that are of the same type and returns a Bool

 - `Eq` : is used for types that support equality testing. The function its members implement are <code>==</code> and <code>/=</code>.
 - `Ord` : is for types that have an ordering. `Ord` covers all the stndard comparing functions such as `>`, `<`, `>=`, and `<=`.


**Ordering** is a type that can be `GT`, `LT` or `EQ`, meaning *greater than*, *lesser than*, and *equal*, respectively.


 - `Show` : presented as strings. Most used function that deals with the `Show` typeclass is `show`. 
 - `Read` : opposite typeclass to `Show`. Takes a string and returns a type which is a member of `Read`.


 - `Enum` : members are sequentially ordered types - they can be enumerated. Types in this class: `()`, `Bool`, `Char`, `Ordering`, `Int`, `Integer`, `Float`, and `Double`.
 - `Bounded` : members have an upper anda lower bound. `minBound` and `maxBound` are interesting because they have a type of <code>(Bounded a) => a</code>.
 - `Num` : is a numeric typeclass.
 - `Integral` : is also a numeric typeclass. Includes only integral(whole) numbers. In this typeclass are `Int` and `Integer`.
 - `Floating` : includes only floating point numbers, `Float` and `Double`.

**fromIntegral** function declaration `fromIntegral :: (Num b, Integral a) => a -> b`.


# Chapter 4 Syntax in Functions

### Patterns

specifying patterns to which some data should conform and then checking to see if it does and deconstructing the data according to those patterns.

define seperate function bodies for different patterns.

you can pattern match on any data type -- numbers, characters, lists, tuples, etc.

pattern defines one by one for each line. if line order changed, pattern changes too.

define pattern *recursively*.

`_` means the same thing as it does in list comprehensions, one or more.

Should a pattern match fail, it will just move on to the next element.

`:` is a bind sign.

`x:xs` pattern is used a lot, especially with recursive functions. But patterns that have `:` in them only match against _lists of length 1 or more_. 

**note** 

`x:xs` means x must be the same type as elements in xs.
`_:xs` means to match the head because we don't actually care what it is. 


If you want to bind to several variables (even if one of them is just `_` and doesn't actually bind at all), we have to surround them in `()`.

 - `error` takes in string and generates a runtime error.


syntactic sugar :: is syntax within a programming language that is designed to make things easier to read or to express. It makes the language "sweeter" for human use: things can be expressed more clearly, more concisely, or in an alternative style that some may prefer. 

source: http://en.wikipedia.org/wiki/Syntactic_sugar


### as pattern

put `@` in front of a pattern to bind it to names, so you can retrieve whole list. For example `xs@(x:y:ys)`, call xs instead of repeatly type ``x:y:ys`.

can't use `++` in pattern match.


### Guards

a way of testing whether some property of a value (or several of them) are true or false (similar to *if* statement).

Guards can be written inline.


### Where

put where after guards and then we define several names or functions.

```haskell
bmiTell :: (RealFloat a) => a -> a -> String  
bmiTell weight height  
    | bmi <= skinny = "You're underweight, you emo, you!"  
    | bmi <= normal = "You're supposedly normal. Pffft, I bet you're ugly!"  
    | bmi <= fat    = "You're fat! Lose some weight, fatty!"  
    | otherwise     = "You're a whale, congratulations!"  
    where bmi = weight / height ^ 2  
          skinny = 18.5  
          normal = 25.0  
          fat = 30.0  
```


### Let

*where* bindings are a syntactic construct that let you bind to variables at the end of a function and the whole function can see them, including all the guards. *let* bindings let you bind to variables anywhere and are expressions themselves, but are very local, so they don't span across guards.

<code>let <bindings> in <expression></code>


### Case

taking a variable and then executing blocks of code for specific values of that variable and then maybe including a catch-all block of code.

```c
switch(e) //case in C#
{
	case A:
	  break;
	case B:
	  break;
	default: break;
}
```

```haskell
//case in Haskell
case expression of pattern -> result  
                   pattern -> result  
                   pattern -> result  
                   ...  case expression of pattern -> result
```

`expression` is matched against the patterns.


# Chapter 5 Recursion

### Recursion

Definition in mathematics are often given recursively. 

Having an element or two in a recursion definition defined non-recursively is also called the **edge condition**.

Unlike imperative languages, you do computation in Haskell by declaring what something *is* instead of declaring *how* you get it. That's why there are no while loops or for loops in Haskell and instead we many times have to use recursion to declare what something is.


### Maximum

define `maximum` function recursively

```haskell
maximum' :: (Ord a) => [a] -> a
maximum' [] = error "maximum of empty list"
maximum' [x] = x
maximum' (x:xs)
	| x > maxTail = x
	| otherwise = maxTail
	where maxTail = maximum' xs
``` 

Most imperative language don't have pattern matching so you have to make a lot of if else statements to test for edge condition.

use *where* binding to define `maxTail` as the maximum of the rest of the list.

clearer way

```haskell
maximum' :: (Ord a) => [a] -> a
maximum' [] = error "maximum of empty list"
maximum' [x] = x
maximum' (x:xs) = max x (maximum' xs)
```

### Few more recursive functions

`reverse` funciton

```haskell
reverse' :: [a] -> [a]
reverse' [] = []
reverse' (x:xs) = reverse' xs ++ [x]
```

don't need to write instructions of how reverse happened, you only need to define what reverse is! very different from exisitng imperative language.

Haskell supports infinite lists, our recursion doesn't really have to have an edge condition.

### Thinking recursively

define an edge case and then you define a function that does something between some element and the function applied to the rest.

when trying to think of a recursive way to solve a problem, try to think of when a recursive solution doesn't apply and see if you can use that as an edge case, think about identities and think about whether you'll break apart the parameters of the function and on which part you'll use the recursive call.

# Chapter 6. Higher Order Functions

##### Higher order function

haskell function can take function as parameters and return functions as return values. a function does either of those is called a higher order function.

You want to define computations by defining what stuff *is* instead of defining steps that changes some state and maybe looping them

（定义它是什么而不是定义它如何去实现）


### Curried functions

```haskell
ghci> max 4 5
5
ghci > (max 4) 5 
5
```

putting a space between two things is simply **function application**. The space is like an operator and it has the _highest precedence_.

```haskell
max :: (Ord a) => a -> a -> a
max :: (Ord a) => a -> (a -> a)
```

That's why the return type and the parameters of functions are all simply seperated with arrows.

在这里解答了前几章里的一个遗留问题，为什么 a 和 a 之间要用 `->` 来分开而不是其他。

if we call a function with too few parameters, we get back a **partially applied** function, meaning a function that takes as many parameters as we left out. neet way to create functions on the fly so we can pass them to another function or to seed them with some data.

**!!this is an important concept!!**

```haskell
compareWithHundred :: (Num a, Ord a) => a -> Ordering
compareWithHunred x = compare 100 x

//rewrite to:

compareWithHundred :: (Num a, Ord a) => a -> Ordering
compareWithHundred = compare 100
```

note: `compare 100` is partially applied function, hence return a function.

To section an infix function, simply surround it with parentheses and only supply a parameter on one side. That creates a function that takes one parameter and then applies it to the side that's missing an operand.


### Some higher-orderism is in order