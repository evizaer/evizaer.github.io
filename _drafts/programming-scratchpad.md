
The lowest level element of programs is data. On the level humans deal with, the atomic unit is a function. Not a function as you think of them typically, though.

`a = 1` is not an assignment statement. It is a function that only causes the side effect of making `a` substitutable for 1 in some scope.

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

# Goodhart's law and simplification
Don't fall into the trap of trying to make something simpler by shuffling around details. Goodhart's law applies to simplification: any individual metric can be circumvented by increasing some other metric!

`var f = function(a, b, c, d, e, f, g) { /* wow, some really complex code. */ }` is actually no worse than `var f = function(o) { a = o.a; b = o.b; c = o.c; /* etc, then the same code */ }` even though the function appears significantly simpler. Passing objects to functions in place of explicit arguments acts to obfuscate the use of the function to the caller/user. Think about the knowledge conveyed to the caller by the function signature: how are they going to find out what to set in `o` to get the desired behavior? 

This is one way in which Javascript fails. No default arguments and no variable-length argument lists in code. You can do these things by hotwiring the function abjects, though, in the function's code, which hides these facts from the caller who needs to know them and probably doesn't.

# Subtyping and taxonomizing

OO is very appealing because it allows nerds to taxonomize. Smart people love classifying and labelling things--it's actually what makes them smart. Being able to classify and label increasingly minute things makes you smarter than others. So OO fits smart people really well. THis is a kind of interdisciplinary smartness that doesn't require specific logical or mathematical skills. Functional languages tend to fit smart people who have a framework for understanding math; a much smaller set of people than smart people who may or may not care for math.

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

