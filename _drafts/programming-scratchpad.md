# Explaining generics, layers of abstraction

Constants
Functions
Generics (parametric polymorphism)
Higher-kinded Types (not in C#)

The simplest value is a constant.
If a value should be different dependent on other values, then you use a function.
If the type should be different dependent on other types, then you use parametric polymorphism.

In C# generics indicate the types that a class or interface operates on. But you often don't have enough functionality to generically define the operations you desire, so you need to "specialize" by creating a class like `public IntComparer : IComparable<Int> {}`.

values are concrete
functions abstract over values
parametric polymorphisms abstracts over types
higher-kinded types abstract over parametrically polymorphic types

# Becoming idiosyncratic

For general and uninformed use, users need good defaults and no necessary configuration.

You need to become conversant with the system before configuring it makes any sense to you. You can steal some progress towards becoming conversant by borrowing knowledge of typographical matters from other programs where you've had to manage typography. Same with color themes.

You can't know what you want to change until you know how you would improve your use of a product.

# Monads in a few words.

Monads sequence operations on some bit of shared state. You can implement your own definition of "sequencing". For instance, the simplest way of making sure a series of operations execute in sequence with lazy evaluation is to turn them into nested lambdas.

# Translating functional concepts into imperative/OO.
Lifting
A function that takes an `a` and turns it into a `List<a>`. E.g. `List<A> Lift(A item) => new List { item };`

Can this be generalized?
`T<A> Lift(A item) => new T { item }`

But what is T? I think this may be only doable with extension methods in C#.

# Requiring capabilities
Really, to print something there has to be a function defined on it that turns it into a string. But what separates this function from any other function that takes the type and returns a string? It should be dependent on "all" the values. This is tricky for infinite types, of course, but you can still condition it on using all the top-level constructs of the type (e.g. you pattern match on every data constructor and don't toss any of their arguments in the match)

My instinct is to atomize interfaces/typeclasses. 

Interfaces in OO are too loosey-goosey and are basically meaningless, formally, so we don't have a good reason to consider them further. What they share is that they give special meanings to names. If you provide things of the right type and right name in a class, it's assumed it should be sanctified by the interface. The interface transfers an assumption of coherence and special meaning to the group of methods that implement it. Of course in OO this is an illusion, and anything can and does happen. Liberal documentation is required.

Typeclasses are a sanctification of the coherence and intent of a set of functions contained in an instance of it for a specific type. This is different! You consciously bundle functions together into the instance, the compiler doesn't just pick out arbitrary functions that match type signature and name and hoping for the best. But I think the ideal would be to pick out functions with the proper requirements that are available to the program. To print a value, you need a function of `value -> String`. Haskell requires you to sanctify such a function by declaring it an instance of Show for the type `value`. But you could articulate your requirement more precisely: `value -> String` needs to depend on all top-level values of `value`. The problem here is that you can arbitrarily make unlimited such functions by using different labels and delimiters. `T {a :: String, b :: String}` can be represented as a string by "T a = <value>, b = <value>" or "T a = <value>; b = <value>" or "T a is <value>; b is <value>", etc.

Names as our only semantic guideposts. In OO languages this is true, in FP types are very strong indicators of semantics, especially when they're embodied by constraints instead of representations. Int is much less descriptive than (Num a) => a. You really  only want to pull in types that support certain minimally coherent algebras, and you shouldn't be able to use them beyond manipulating them with those algebras. This is non-leaky abstraction at its best.

What about the fact that (+) :: (Num a) => a -> a requires both a to be the same? I don't care if they're the same if I only care about the algebra! But at the value level algebra participation doesn't imply comensurability or compatibility.

# Types as constraints

Types as descriptions of representation vs. types as the intersections of constraints on functionality.

Types as intersection of constraints on: representation vs. functionality.

We can define types in terms of the behavior they must support, or in terms of what they represent.

Constraints on values vs. constraints on what can be done with values.

`(Ord a, Eq a) => a -> a` vs. the type-level implementation of ordering and equality of values.
 
 The ordering of arguments only matters based on what role the arguments play. `a -> a -> a` doesn't convey anything about the roles of the two arguments, though they could be very different (divisor vs. dividend). If they don't play different roles, by have them as separate arguments? Does this also apply to arguments of different types? Must differently-typed arguments necessarily fill different roles?

 If types are roles than argument order doesn't matter.

 Does a in `(+) :: a -> a -> a` fill the same role in both arguments? SHouldn't it be (+) :: (Monoid f) => f a -> a, since order doesn't matter? Can't use a set because uniqueness is irrelevant! So count-sensitivity must be a separate "property" from commutativity.

# Structural reasoning
GHC Haskell has the ability to derive instances of typeclasses for your types based on the structure of the types. You can write such derivations using the generics extension. 

How could you possibly do this? As someone raised an OO programmer I'm used to reams of implementation details going into the implementation of an interface--so many implementation details that it's beyond infeasible for a computer to *just guess them* based on the interface itself. Objects in OO don't seem to have structural properties. Sure, they haven named variables and methods, but what defines the behavior of the object is methods opearting on all that stuff. 

Perhaps the closest you can come is defining interfaces which provide low-level facts about a type's structure, then creating static classes that operate on parameters that have a collection of such interfaces.

```
interface IIdentityValue<T> { T IdentityValue { get; } }
interface IMonoid<T> : IIdentityValue<T> { T Append(T, T); }
abstract class Monoid<T> : IIdentityValue<T>, IMonoid<T> {
    T foldr(T a, IEnumerable<T> b) { /* implementation */ }
}

class SumMonoid : Monoid<int> {
    int IdentityValue { get => 0; }
    int Append(int a, int b) => a + b;
}
```

# Readability
Levels:
* conceptual familiarity - you know about conditional execution (if-statements) but what about monads? free monads? 
* representational familiarity - you're familiar with C# syntax, but what about Haskell's for doing the same thing?
* Idiom familiarity - combinations of concepts and representations produce different commmon patterns of convenient usage--these are like architecture's "desire paths" but in code.
* Domain familiarity
* Design familiarity - Intersection between idioms and domain.

Once we get past familiarity, what are we left with? Expressing complex ideas with as few symbols as possible, and knowing they'll work before we run them. Leaky abstractions work against this.

# Not so SOLID
Taming inheritance? Composition makes more sense.

Inheritance is accretion-made-easy. Composition encourages simple components combined in various different ways. Understanding a bunch of simple components is a lot easier than making sense of the countless accretions of functionality and state change accumulated into the most concrete class in an inheritance hierarchy.

(Definitions from [the wikipedia article](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design)))

Single responsibility principle
    a class should have only a single responsibility (i.e. only one potential change in the software's specification should be able to affect the specification of the class) 

Open/closed principle
    “software entities … should be open for extension, but closed for modification.” 


Liskov substitution principle
    “objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program.” See also design by contract. 

Interface segregation principle
    “many client-specific interfaces are better than one general-purpose interface.”

Dependency inversion principle
    one should “depend upon abstractions, [not] concretions.”

# Perilous Polymorphism in OO


1. Don't let your individual variables hold meaningless values.

Wrong layer of abstraction: Wall, Orc, Door. These just fix certain conditions of terrain tiles that are otherwise variable. Classes that consist of no behavior and only have a bunch of parent class attributes set in their constructors are an abstraction level red flag.

Human conventions are constraints enforced by social means. Programmers may enforce constraints of their own code through a kind of internalized notion of good code--this is a social impulse which interacts with future-you in place of someone else.

Every invalid state of a data structure is a waiting bug, or a convention that needs to be established. The convention is there to avoid the waiting bug.

How many bits of information does a class convey?

Think about how many meaningful constraints a line of code puts on its user.Compare these two methods:

@(1. arguments written out normally.
  2. arguments all wrapped in an object.)


# What you can't change matters.

Letting you change a lot of things at any one time is very dangerous. Bugs come from changes.

In C# `var result = a.Do(b, c)` gives Do the ability to read and write to all state of a, and public state of b and c. This is a lot of state that can potentially be mutated in ways that modify the outcomes of other operations performed on a, b, and c at some later time. 

In Haskell, `let result = f a b c` modifies nothing. It evaluates f using the values of a, b, and c, and will produce the same result given the same values of a, b, and c. The parameters to f could be very complex in themselves, containing megabytes of data in a variety of forms, but that doesn't matter, because the language constrains the programmer in that it doesn't allow the values of the parameters to be modified. Any other places later on in the program where a, b, and c are used know that they have the same value that they had when they were brought into scope. No unexpected or unmarked variation can happen. This means the amount of data flowing into this expression is the same as that for the C# statement, but the data flowing out is *significantly less*. This means that the surface area on which bugs can appear is significantly less.

To make an accurate mental model of a system, we usually take the first step of understanding its parts. Programming languages that allow us to clearly chart the inputs and outputs of a system's parts help us to make clearer mental models faster. Languages with features that make it more difficult to chart out where data can change may let us write code faster in the short-term, but much beyond that the lack of restrictions causes lots of idiomatic knowledge to accumulate. In C#, The programmer has to know what bits of which parameters are modified in order to know if it'll be safe to use a method. 

Idiomatic knowledge about what is done within an abstraction, given that the space of what can be done in that abstraction is way larger than what is ever actually done.

This accrual of idiosyncratic knowledge causes systems to become increasingly difficult to modify and maintain as they get more complex, since the tendrils of each place where each piece of state can change branch out ever further in increasingly idiosyncratic and complex ways.

This is why javascript libraries and tools usually have the very elaborate documentation publicly available, while C# projects typically have less, and many Haskell libraries don't need much documentation at all.

Javascript lets you change the basic constituents and operations of any data structure at any time. C# fixes the constituents of data structures in place, definitionally, but still allows modification in many places. Haskell both forces the programmer to commit to stricter definitions, and limits modification of data to specifically-marked functions.

In Haskell, abuse of mutation and looseness are exceptions, they are not the rule. In Javascript and even C#, reliable and careful code is an exception forced by strong positive cultures and mores, not the rule.

# Basic programming language ergonomics: Take advantage of standard time metaphors in syntax.
Verbs only take certain arguments.
Nouns can be in any of multiple positions

what about using time as a clearer indicator of how syntax should work? We already intuitively have this happen in imperative langauges: typically we write code which sequentially proceeds top to bottom in the file. I think it's easier for people to think this way because it more closely mirrors the intuitive way to give directions to someone on how to do something. 

Within a line, though, this isn't the case. In an assignment statement, the variable whose value we're changing comes first, even though the change happens once the code on the right side has been evaluated.

`d = a.v(b, c)`
`d = v a b c` 
But what about
`a b c v d`

Inputs first, because you already have them, then the action and then outputs last.
It's debatable if the verb or the nouns should go first, because they're both "equally available".
input -> action -> output is pretty clear. 
# Subject-object distinction
https://github.com/dotnet/csharplang/issues/164

From this proposal, it's clear that we want to be able to attach any method to any subject where it makes sense, independent of namespacing and object boundaries.

C# allows extension methods, and there's a proposal to allow extension in basically all ways to any type. This points out that the subject-object distinction is not in fact valuable. You want to define operations on data, and if that operation comes after your data's dot or someone else's dot is irrelevant to the operation. 

Functional programming languages tend to not believe in subject-object distinction at all, and their IDEs pay for it. Functions are module-qualified so we don't have too much namespace pollution, but if you want to see what you can do with a value of type String, it's tricky to do. You could search Hoogle, if you're using haskell, for functions of a type that has String on the left side of an arrow, but you'll get all kinds of stuff that won't make you happy.

# Side-effects
The lowest level element of programs is data. On the level humans deal with, the atomic unit is a function. Not a function as you think of them typically, though.

`a = 1` is not an assignment statement. It is a function that only causes the side effect of making `a` substitutable for 1 in some scope.

Rmemeber that every single piece of internal and public state of an object is implicitly passed to every instance method on that object when it's called.

# The knowledge perspective

Writing a program is creating knowledge that you or someone else is going to have to learn and keep in mind. The objective is to create as little knowledge as possible while solving the problem at hand. This means leveraging consistent behavior, powerful metaphors, and domain-based analogies to their fullest extent so that what knowledge you already have (or can quickly attain) can be used repeatedly, instead of requiring separate bits of knowledge for the same effective solution. From this we get principles of good software engineering: 

* Don't Repeat Yourself (DRY) - Reusing code means less specific knowledge is needed, since you only represent the knowledge of the reusable code's operation once.
* You Ain't Gonna Need It (YAGNI) - Don't add additional features or capabilities to the system beyond what serves the requirements of the system direction. Don't create knowledge which isn't used.
* Keep It Simple, Stupid (KISS) - More complex solutions inherently involve more knowledge to understand. It's built into the word "complex." This is actually a restatement of YAGNI, but in the positive instead of negative.

On the small-scale of writing code, minimizing knowledge means keeping the scope of each bit of state as small as possible. 

There is some wisdom in purist OO design that states that access to state of objects should be as minimal as possible. The programmer has to worry about keeping track of fewer things if he knows that only a few members can be called and set externally.

IDEs help programmers leverage knowledge about the program, automatically derived from the program's code, to inform future code as it is written. Declaring what abstractions are is way more valuable than you at first might imagine. We trade flexibility for hard knowledge. We can't know what an object in javascript will look like unless we run the program. Programmers anywhere can mess with the contents of the any function, and change any data. In contrast, we can glean lots of relevant data from a C# class about what objects of that class will look like when we run the program.

If you can make stuff up on the stop, structural knowledge is unnecessary and unwanted. If the language forces you to know and articulate the meaning of symbols before you use them concretely, you can't just make stuff up and change anything you want to suit your whims at a certain time. This means you have to think about the structure of your code up front--you have to think about particularly difficult questions of how to represent and manipulate information and processes from the real world. You have to do it up front and you have a very strict judge looking over your should during the process who is making sure you're being consistent.

Different languages have different amounts of information you can encode in types so that the compiler can check your work automatically. Object Oriented languages tend to have pretty simple checking. We just want to amke sure you are passing a Thing or at least a kind of Thing to this function. @Insert haskell is next, then idris. And the actual content that makes them more powerful than one another. Blub paradox comes into play?

This is why languages with more sophisticated type-checking tend to turn into proof assistants. Proofs and formal logic are how we state structural knowledge in unambiguous terms.

through defining classes in an OO language or providing type annotations (and your own types) in a functional language

Types are claims about compound data.
Types are necessary, because you've got a bunch of bits that can be read off of disk, RAM, and processor registers, and those bits are only useful in that they represent *something*. Perhaps they represent some number or letter--that's up to programmer's conventions to decide, though. The physical data as it rests on your computer is agnostic. Code gives meaning to bits. Programming languages give you the tools to create that meaning in different ways. We take a cacaphony of bits and use programming languages to turn them into structures--combine these bits interpretted as a number and these other bits interpretted as a string and now you're representing a person's height and name in a something you call a "person" record or struct. A type is a type of data in this way: it's a schema for making sense of a mass of bits.

in dynamic languages you often have to write the code that represents the same knowledge that's encoded in a compiler in a statically-typed language with an expressive type system. If you do not apply these constraints yourself, you are leaving yourself open to bugs. it would be absurd to check that every single value contained in a javascript object is actually what you think it should be everywhere it is used, though, so we skimp and pay the price later with runtime errors that are more usually more difficult to debug than a complie-time error.

Types are a knowledge management tool--and a way of communicating to the compiler the knowledge you want to keep stable, then the compiler takes care of the busywork of maintaining that stability.

# Goodhart's law and simplification
Don't fall into the trap of trying to make something simpler by shuffling around details. Goodhart's law applies to simplification: any individual metric can be circumvented by increasing some other metric!

`var f = function(a, b, c, d, e, f, g) { /* wow, some really complex code. */ }` is actually no worse than `var f = function(o) { a = o.a; b = o.b; c = o.c; /* etc, then the same code */ }` even though the function appears significantly simpler. Passing objects to functions in place of explicit arguments acts to obfuscate the use of the function to the caller/user. Think about the knowledge conveyed to the caller by the function signature: how are they going to find out what to set in `o` to get the desired behavior? 

This is one way in which Javascript fails. No default arguments and no variable-length argument lists in code. You can do these things by hotwiring the function abjects, though, in the function's code, which hides these facts from the caller who needs to know them and probably doesn't.

# Subtyping and taxonomizing

OO is very appealing because it allows nerds to taxonomize. Smart people love classifying and labelling things--it's actually what makes them smart. Being able to classify and label increasingly minute things makes you smarter than others. So OO fits smart people really well. THis is a kind of interdisciplinary smartness that doesn't require specific logical or mathematical skills. Functional languages tend to fit smart people who have a framework for understanding math; a much smaller set of people than smart people who may or may not care for math.

# Subject-object distinction in OO

x.Do(y). This is misleading because it looks like english and makes us want to use natural language metaphors and make all our code look like natural language. But natural language has no automatically-applied systematic knowledge restrictions like programming languages do. Your variables have to be in the right scope at the right time to be used by the methods that need them.

Programming as State Transformation
-----------------------------------

Programming is all about state transformations--taking data and turning it into different data. This indicates that hte most important part of programming is keeping in mind what can change and what it may change to.

You can look at functions through this perspective--parameters tell you what varying conditions influence the outcome, and the return values represent data that has been changed in some way by the operation.

Thinking about functions this way, Object-oriented programming seems to be inferior, because calling a method on an object insinuates all of the state of the object can be changed by the method. Also, any state in the object can vary and change the result of the method. That's a lot more to track, and a lot more that can implicitly vary, than in a language that requires functions to be pure most or all of the time.


What's Affected?
----------------

One of the most important questions to be able to answer when reading code is "what is affected by this function call?" For pure functions you know that the only result is that a value is returned. In C-style languages any piece of memory in the program's purview could have changed. 

Syntax
------

Good syntax specifies important information quickly and unambiguously. It helps the programmer have to remember less, and makes it easier to look up relevant details about how code should be used.

### Types Matter

You can either hide from types or embrace them, but they will always be there even if not as formally an important construct in the language.

### Javascript

In Javascript, code can easily be written which gives the programmer no idea what will work and what will not. Function calls can be mangled by manually manipulating functions as objects from within or without the function; variables can be changed from almost any scope; and objects can be created with arbitrary keys and have their members removed or manipulated by outside parties at will. All of this means thaty ou know nothing about what is actually going to be happening in a program at any point, when you write the program. Any function or object you've created at one point can be messed with extensively before you later use it. It might not even exist any more, and the only indication you'll receive is an error message in your browser's javascript console, accompanied by some odd behavior within your application.

### Named Arguments

When the name can convey a lot of meaning, it's great to be able to name arguments without resorting to packing them into an object that has named properties that must be set.

Higher-order functions generally don't benefit from named arguments, especially if they do not have any repeated types that may be ambiguous in usage. There's also no clear way for the syntax to be written in haskell-like languages.

    map with list = ls, mappingFunc = f

Not much is conveyed there, and the syntax is pretty unwieldy compared to `map f ls`. This is because there are no better names for arguments with such abstract roles.

Compare that to a function meant to merge two dictionaries, one of which has priority--it's values will be used if there's a conflict. The type will be `Dict a b -> Dict a b -> Dict a b` which is highly ambiguous about which of the two input Dicts will take priority. 

Object Orientation and Hiding Side-effects
------------------------------------------

Assume `felix` is a `Cat`-type object. If we properly use the concept of return values and maintain the purity of functions, `Path p = felix.WalkTo(10, 12)` is actually `(Path p, Cat felix) = WalkTo(felix, 10, 12)`.

Calling a method on an object implicitly passes that object into the function, then effectively returns it from the function and assigns that back to your object's identifier in the calling-scope. Object-oriented programming *hides* the behavior of functions from you through being implicitly giving methods access to persistent (between calls of the method) state that is in a different scope that the programmer using the method can't see or even mostly have access to.

Object-orientation is thus fundamentally obfuscatory and the programmer must always behave defensively and with great caution around its primary way of doing abstraction, objects.

On Code vs. Documentation
-------------------------

Documentation will always be needed to provide answers to "why?" questions.

Programming languages can require us to specify enough information such that we don't need to document "what?" questions.

In Javascript, you have to ask yourself "what is this object?" a lot. What properties does it have? What properties can it have? What will code actually use? What kind of data should go in these properties?

Statically typed languages give you all of this information, and its validity is verified when compiling the code. Javascript doesn't care. As long as the pieces are in place at the exact moment they are needed, it won't complain. In fact, even if needed pieces don't exist at all it won't complain much--often it'll let execution continue as if nothing were wrong.

This is a manifestation of the static v. dynamic language divide. When the language doesn't check the validity of most of your logic, you're free to do crazy things that rely on invalid logic in the short term, like mangling the internal state of an object by changing the names and values of its properties and methods so that it performs alternate behavior in addition to or replacing existing behavior specified by its creator.

Should programming be easy?
---------------------------

When something is easy to do in programming, it's usually because the actual complexity of what you're doing is hidden away under levels of abstraction that you will have to become familiar with as you try to do more complex tasks. This complexity is still there. Often this early ease causes long-term pain.

Notice how many examples of programming languages, paradigms, and libraries only show simple examples. Those are examples where the abstractions can pull their weight the easiest.


Static Typing and Thinking about your Program
---------------------------------------------

It's good when features of a programming language make you think about your problem before trying to dash out code to solve it. The more rigor of thought required, the longer the code will take to write the first time but the less likely it will be to need to be changed unless requirements change.

Requiring appropriate rigor in specifying a program raises the thought-floor of code that you write--that means you'll write better code more often because you just can't write lazy and dangerous code as easily.


The types of the variables in your program really matter, whether you specify yourself or not. The bahavior of variable is always mediated by what type they are. This is unavoidable. Even if you don't have to specify types, the types of variables are necessary for your program to do anything--one of many reasons why it's better to explicitly specify types. "What is this?" is a necessary question to answer when reading and writing code--type specification makes that question a lot easier to answer.

Function Declaration Syntax
---------------------------

Consider these three ways of declaring a function's prototype:

ML-style: `function f(a : int) : bool`

C-style: `bool f(int a)`

Haskell-style:

    f :: Int -> Bool
    f a = ...

Haskell is the only style of the three that assumes purity of functions. Even though you may return some value from a function in a C-style language, you also effectively "return" any referenced data structures you've modified on the heap during the process.

Recursion
---------

Recursion can be emulated by making your own stack and adding or removing jobs from that stack as necessary, inserting results gained into the job data structure.

Since recursion uses the stack as an implicit means of primary storage, it's unnecessarily indirect and harms the ability of the programmer to comprehend the space and time requirements of code.

Design Patterns as Abstraction Deficiencies in Languages
--------------------------------------------------------

Design patters appear because the programmer lacks the ability to abstract those patterns in some way where only their changing parts would be modified in subsequent implementations of the pattern.

Lisp has macros. Haskell has Type classes, kinds, and a well-developed type system, as well as auto-currying and functions as first-class objects.

Ideally the biggest "pattern" in the language should merely be a syntactical expression, as opposed to how it is a group of classes with certain behaviors and properties in an OO language.

A simple thought process to analyze this is to consider what is the smallest collection of code you can run to actually get some kind of meaningful result. In OO languages with design patterns it is several classes. In pure functional programming it's one function, or perhaps the implementation of a typeclass, because pure functional programming doesn't rely on the state of other bits of the system within its standard unit of abstraction.

The "Kind of Text" Problem
--------------------------

    type Book = {title : String, author : String}
    
    type Art = Book of Book 
             | ...
    
What kind of text is Book ever? `Book of Book` looks suspicious and confusing.

Ambiguous Syntax
----------------

In TSQL

    CONSTRAINT fk_name
      FOREIGN KEY (child_col1, child_col2, ... child_col_n)
      REFERENCES parent_table (parent_col1, parent_col2, ... parent_col_n)
      ON DELETE CASCADE

On deletion of WHAT?

Function Application as an Operator
-----------------------------------

Haskell syntax requires you to think of function application as an operator. haskell is basically lisp without the parens, with additional infix notation that can cause confusion.

    something 1 + 2

This line is ambiguous to someone not very familiar with Haskell. Does it mean `(something (1 + 2))` or `(something 1) + 2?` In lisp it's totally unambiguous because of the required parens.

It all depends on the precedence level of the function application operator--the space between tokens in an expression.

In C-style syntax, function application is unambiguous because arguments for a function necessarily are enclosed in parens. This makes the differentiation between function names and data names much clearer--such clarity may be in conflict with functions-as-first-class-citizens precepts of Haskell-like languages.

Currying is also "automatic" in Haskell and it's easy to tell, because you don't have to explicitly terminate the end up an argument list as you would in a C-style language.

Core Cognitive Concepts
=======================

Relative location
-----------------

Information relevant to a line of code should be as close to it as possible.

THis actually militates in favor of great naming, since names are a quick way of divining design information about a function or value. The closest that information can be to a function or value is within the name of that function or value. We can derive from this principle that magic values are also bad programming practice, since they are unnamed and thus give us no information about their design and purpose.

Examples and Prior Articles
===========================

http://www.haskellforall.com/2015/09/how-to-make-your-haskell-code-more.html

