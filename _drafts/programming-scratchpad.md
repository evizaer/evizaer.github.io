# Good code minimizes what can change.
To write good code, limit what can change and name changeable and reuseable things well. In this article, I'll focus on the rationale behind limiting what can change, how to do it, and what programming languages push you towards doing it best.

Here are four objective goals that lead to better code. This article is about why they work and how to achieve them.
* Minimize possible mutation. Use constants and read-only values as much as possible.
* limit scopes of all things to as few operations as possible.
* Use powerful type systems to ensure as few values are valid as possible.
* Favor linear execution flow. Any method of allowing parallel execution is hazardous because it makes the order of execution unclear.

## Rationale
When you're debugging, you're tracing how variables change through sections of code to try to isolate a specific change that's leading to unwanted behavior. Debugging gets more difficult if the changes are happening in more places in the code and, if there's multithreading involved, at unpredictable times.

Every operation your code performs is an opening for a bug. Every bit of state that you could change in a section of code is something that could be changed--now or later--in error.

Debugging code is the intensive practice of reading code. Code is easier to read when less state flows through it. Code is also easier to write when less state flows through it. Types constrain the possible values a variable can hold. When types ensure only meaningful values can occupy a variable, it's harder to introduce bugs. A perfect example of this is the difference between explicit enum types in C# and integer constants used to emulate enums in early C and C++. In C, the type of the enum value is merely `int` or `char`, so most values it could hold would be invalid but the compiler wouldn't bother you about it. You can also do arithmetic to these pseudo-enum integers and get bizarre results.

Code gets more complicated when it lets more of its elements vary. When pieces can vary, you must keep track of how they can vary and what happens with each variation. Each means of variation is a vector for bugs. In a particular case this might not be a big deal--there are millions of numbers you can add to one another without underflow or overflow--or it may be catastrophic--most integers you could use to index into an array will read or write past its bounds.



OO languages fail on the first item: they do not minimize mutation compared to other languages. Objects have data that is implicitly passed into every behavior of that object and may be mutated by the behavior. This is very dangerous--it invisibly bloats the number of items that can vary and gives lots of room for hidden variations that can cause bugs.

Tacit programming may be the ultimate realization of this style. Point-free style gets us most of the way there, but composition's ergonomics are too often poor in programming languages. Also, composition without naming intermediate values can lead to code which programmers will have trouble comprehending because it stretches their working memory capacity. To make sense of a long expression that represents many computational steps will require a programmer remember several intermediate results somehow. Without the aid of names, this can be difficult. Since the composed operations are typically pure functions with simple implementations, a programmer can fluently parse a long point-free function with not too much practice.

The real struggle with point-free style is that the vocabulary of pure functions you need to use to program in that style is different from typical imperative-style programming. Imperative programming relies heavily on assignment, simple math, and method applications that make use of side-effects (most often mutation of the object that hosts the method)

Whenever you use a variable of a specific type, all of that type's operations are viable to be performed as long as that variable lives, which means that the universe of possible code that can be written grows incomprehensibly huge very fast with only a few variables of modest types, like int and double and string.

Regardless of the programming language you are using, you must grapple with the fact that you're representing values in memory in some specific concrete representation, and you must use logic that makes assumptions of that representation in order to use those values in your program. 

Values are only useful because you can act on them. Acting on a value places constraints on what the value can be and what names must be in scope. Those constraints are unavoidable and must be articulated somewhere. The programming language can require the programmer to specify the constraints on what can be done with a value along with that value's type, or the programming language can wait as long as possible to make the determination of constraints by only resolving them exactly when it tries to execute an instruction that uses the value.

Javascript hides the constraints on a type until the latest possible moment--when the specific line of code using that type is actually running. This is programming without knowledge.

Pure functional programming languages are the best according to criteria of minimizing what can change. Purity means that side-effects are impossible or at worst tracked carefully, thus eliminating a common source of uncontrolled or invisible ways values can change.

## Linear execution flow
It's important to know when something will change. Predictable execution flow is important because in order to tell what can change you need to have a concept of when changeable things are open to be changed. The same logic can be applied here as to the concept of limiting scopes.
# Dynamic vs. Static

Dynamic is late, static is early. The benefit of dynamic languages is that bugs affect as little code as they possibly can, and your program can run while having many buggy code paths so long as those paths aren't run. Static languages benefit the programmer because they prevent many classes of buggy code paths from being compiled in the first place.

Tests are types articulated in concretions instead of abstractions. Tests define how method results should vary as parameters vary.

Exhaustive pattern matching and function totality checks ensure that all values of a type can be operated on by a function. Imperative languages rarely allow the programmer these facilities. I'm not sure why, but perhaps it's because the language is so profligate with variable scoping and mutability that totality and exhaustive pattern matching are impractical to an extreme.

Is there a word for functions that produce types with fewer values than their input?

You can think of a program as narrowing the input space to a smaller output space. Types define the bounds of these spaces.
## Keep scopes small
Good code keeps the scopes of all variables as small as possible because bugs arise from unintentional changes or changes with unintentional consequences. To restrict possible consequences, each piece of relevant data should be available to change for as little time as possible. It's easier to review ten lines of code for unintentional changes than it is to review 100, and often the difference between having to do one or the other is a few low-effort code changes.

Each piece of state should be as immutable as possible, and should live for as short a period of time as possible.
# Rust's borrow checker and scopes
Rust uses a C-style syntax for scopes and variable decls which does not suit good use of its borrow checker. Ownership should motivate scoping syntax more.


```
let thing = Thing::new();
let mut thingUser = ThingUser::new(thing);
```

`thing` cannot be used in any way later in this scope unless a function on `thingUser` is called which passes ownership back to this scope. To make scopes more clearly line up with name availability, you could write something like

```
let mut thingUser: ThingUser;
{
    let thing = Thing::new();
    thingUser = ThingUser::new(thing);
}
```

This code more closely reflects the reality that `thing` is out of scope after it is passed into `ThingUser::new`.

How could you make ownership and scopes work together better?

If you transfer ownership out of this scope, you are effectively undeclaring the symbol in this scope.

Rust's ownership system is an implicit per-variable scoping system atop the existing system. Unsafe code lets you break the scoping rules in certain ways.
    
# Explaining generics, layers of abstraction

value level:
Constants
Functions

type level:
Types
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


The substrate of all stored data and programs in computers is a sequence of bits. To make this sequence represent different shapes and kinds of data (like a number, a character, a sequence of instructions, or an employee's payment record) we have to invent conventions that we follow without fail. If we fail to follow the conventions properly, we could get nonsense or, worse, introduce security vulnerabilities by trying to read or write memory that we shouldn't or can't.

We enforce these conventions through types. Alternatively, we enforce these conventions by only allowing someone to read the same type of data that has been written.

The simplest data convention is turning the bit string into a single value. "001" represents the number 1, or the character "A". Based on the length of the bit string we want to interpret as a single number, we articulate a set of possible values. 8-bit integer is a type which can represent the numbers 0 through 254 by interpreting a 8-bit long bit string as a base-2 natural number.

But why 8 bits? Why fix the number of bits? Whenever we see a fixed value, we can imagine a circumstance in which we may want to vary it, i.e. we can abstract it out, leaving a descriptively-named token in its place. 

In order to allow the programmer to configure the number of bits used in the representation of numbers, we could parameterize the type with the number of bits. Since the essence of the type is as a convention of converting a bit string into a number, we could conceive of the type as a function from bit string to number which takes two parameters. The first parameter is the number of bits per number, and the second parameter is the bit string.

`represent_number :: *Int -> BitString -> Int`

Of course, this is bizarre since you must already be able to represent a number in order to write this function. I've prefixed the first "Int" with an asterisk to represent that it's solely conceptual. Let's call it a "conceptual" function. The programming language does this kind of thing for you to allow you convenient shortcuts.

Another convenient shortcut is a character. Characters can be represented by choosing a number of bits, then assigning each variation of those bits to one character. E.g. with four bits, 0001 should represent 'a', 0010 'b', 0011 'c', and so on.

This is the conceptual function `represent_char :: *List *Char -> BitString -> Char`

(Note: For this to continuously read the bit string to decode many values, I should be returning `(ReturnType, BitString)` where the BitString is the remaining unused bits after what we parsed into a representation.)

Decoding a bit string into a number involves establishing a mathematical relation between the bits, while decoding a bit string into a character is a one-to-one mapping operation. These are the two fundamental data representation techniques in computers. You define a mathematical relationship between bits or you code each item your type can represent as a specific bit sequence. 

The third core data type is typically called an "enumeration" in imperative language or, in functional parlance, a discriminated union with only nullary constructors.

You represent enumerations also through a mapping process. The names are only meaningful to the programmer, though, and are defined by the programmer. Character and integer representations are core to programming languages thus are fixed by the language designer or, in many cases, the processor designer as kinds of data the processor for which operations are specificially tailored.

Enumerations are like the general case of mapping types, but programmer-definable. Their representation function looks like this `represent_enum :: *List *Name -> BitString -> Name`

Note that you do not need an integer in this definition. Based on the size of the set you're mapping, an appropriate number of bits can be chosen for the representation. Often in reality some power of two will be used for bit counts. The particular value will be determined by particularities of the processor's architecture instead of what is most convenient for the set we're mapping.

You can generalize the mapping style of representation as the conceptual function `represent_mapping :: *List *a -> BitString -> a`.

## Composing Types
Now we can represent any number or mapping of bit string to arbitrary representee. The real magic of programming comes from how we concatenate and combine these basic representations.

Types can be composed in many ways. Usually these are conceptual groupings of data which tend to travel together in the program. `Struct`s are a common such grouping mechanism, arrays are another.

Structs are a concatenation of representations of fixed numbers of named pieces of data. The names are necessary in the representation because struct literals are useless if they are not named somewhere--you can't access the contents of a struct in code if they aren't somehow named, so you would not make a struct without names.

To represent a struct, you must know the widths of all its members, otherwise you don't know where one member ends and the next begins. Allocating memory for structs can't be done without knowing its size. (I should probably have mentioned this earlier. Maybe I don't want to discuss allocation at all here.)

Structs are the first concept which abstracts over types. You can plug any type into a struct--all you need to know to represent a struct is the types in involved and how many bits they take up. All types defined so far occupy some number of bits, so this data is available about all types.

The process of abstraction:
1. find the minimal set of common properties
1. define a structure which articulates those properties
1. replace concrete values with the structure defined above.

Unique problems arise when you start composing things that themselves consist of compositions. Structs containing structs. Structs which refer to themselves are a tricky problem which we'll save for later.

Let R be the type represented.
`ReprFunc :: BitString -> (*R, BitString)`

You can partially-apply conceptual functions that require bit counts such that they only need a BitString parameter. Through this method you can generate a variety of integral types, like unsigned 8-bit integers, 16-bit integers, longs. Introducing signed integers requires a different representation function.

`represent_struct :: *List (*Name, *ReprFunc) -> Struct`

Arrays are contiguous series of representations of the same type. Representing them is easy.

`represent_array :: *Int -> *ReprFunc -> Array`

Simply run the ReprFunc some number of times and collect the resultant items somehow.

How would you represent an `Option a`?

`represent_option :: *Bool -> *ReprFunc a -> Option a`

## THe real world?
Programmers do not work with representation functions in the real world, even when they're working on very low-level code. The processor has representations for integers, pointers, and floating-point numbers built in, and many operations for these types hardwired to be fast.

It's good to never allow invalid values in a type, but processor peculiarities often prevent this. For instance, if memory is byte-addressed and you have an enum that only has 4 possible values, some bytes you can store cannot be read as values of that enum.

## Representation and Sets
Types are sets. But types are also rules for representation. This might necessarily be the case, since sets are groups of representations. Types are generative, though.


## Meta: OK, but what are generics?
Sometimes you want to provide an abstraction over types.

We've covered representation functions so far that 

Arrays and Structs abstract over types: that can be the entry point to discussing parametric polymorphism.

polymorphism: many forms. Really: it abstracts over those forms. Works without knowing the details of the forms.

# Taking dynamic scoping seriously
Dynamically scoped languages shouldn't allow procedure arguments. In such languages arguments are just a list of variable rebindings which would be better done explicitly.

```
def f:
    x = x + 1
    return g
```

But you need syntax to determine when you're calling a proc vs. referring to it by name.

Dynamic scoping is garbage because it pulls in arbitrary data from other scopes and modifies it. The number of possible changes to state that code has to tolerate balloons ridiculously as code is reused, even if the most sophisticated form of abstract is procedures.

Dynamic scoping only allows the barest possible abstraction because variable scopes cannot be isolated and change cannot be minimized or predicted based on code.

Dynamic scoping proponents fall to the false economy of not knowing.

# Squares and Rectangles, OOD
https://www.gamedev.net/blogs/entry/2265481-oop-is-dead-long-live-oop/

A square is a data constraint on a rectangle. Representing squares and rectangles as different classes with different interfaces is a bizarre suggestion born of the structure of the question more than the quality of the answer.

You need to know the problem you're trying to solve before you can design abstractions to solve the problem. Designing abstractions for their own sake cannot yield intentional good design. It's impossible to tell if a design's good without knowing its application.

What are you trying to do with squares and rectangles? Enforce the constraint through the algorithms that manipulate them as necessary.

# The false economy of not knowing
To solve a problem, your code needs to at least be a function or method call that takes a number of parameters and produces outputs (via the return value, filesystem, network, etc.) that vary based on those parameters. You isolate the exact things that can change going in, then you produce only so many possible outputs as needed to solve those variations on the problem. You can write code that solves exactly one instance of your problem, but then you might as well just provide the output statically. If the solution is more general than the problem, e.g. travelling salesman vs. shortest route between two cities, more configuration is needed. This configuration would be the same every time, while other parts vary, like which two cities you want the shortest route between.

Your code needs to address the problem and turing-complete languages address the same classes of problems. Your choice, then, is between tools that favor different cognitive strategies and proclivities in the programmer and make expressing solutions of certain kinds easier or more difficult.

Choosing your tools implicitly lets you choose when you'll confront the logical errors and other bugs in your program. When you confront bugs implies different distributions of cognitive overhead. Statically typed languages let you confront bugs earlier in proportion to the power of the type system. Java's type system doesn't help much, while Idris' type system helps a bit too much for most programmers--it helps so much that the programming experience qualitatively changes. 

In the most dynamic language, programmers find bugs as late as possible. Only when the execution of the program explores a specific code path will bugs become apparent in that code path.

In the most static language, programmers find bugs as early as possible. The compiler won't run the program until it will terminate with a logically consistent result--of course this result may be wrong because the programmer's logic was wrong, but the program will be internally sound. 

## The boundaries
Types exist even if the programmer doesn't want to acknowledge them and the language doesn't want to make a big deal of them. Programming languages have to store,retrieve, and manipulate bits according to certain rules so that programmers can intuitively do math and manipulate strings. A language must deal with `"s" + 1` in some way. Either types (really, representations) interconvert implicitly--and how this should be done is unclear--or the language has to throw up its hands via a type error and ask the programmer to clarify what she wants. If you're adding an integer to a string, you result can't be a strinteger. Someone has to choose how the output value is represented.

## (Old article)
In OO, we seek to reduce complexity by reducing available knowledge. 

Encapsulation is about hiding some state--not minimizing state the user has to worry about, but hiding it. Encapsulation is about providing a minimal, consistent interface to hidden information. Why do you hide this information?

The naive answer: you hide information so that client code doesn't have to worry about that information. By preventing the user from seeing and manipulating details, you implicitly are telling them that they do not matter. The interface is a subset of the constructs necessary for the implementation, therefore it's simpler to use the interface. The number of possible bugs is thus reduced, since outsiders can tinker with the state of the object only through the interface. 

Encapsulation is a weak promise about mutation. Typically objects feature so much internal mutation that it doesn't matter if we allow or don't allow some other object to also mutate it. We've already hit inflection points past which the number of additional possible states we add to the mix don't matter.

As I've matured as a developer, I have learned that you often have good reason to know at least *some* implementation details of the abstractions you use. Objects, as they get more complex, tend towards requiring more knowledge of implementation details to be used effectively. Consider humble commonly-used data structures like List and Dictionary: to know their interface isn't enough. Documentation pages mention performance characteristics--implementation details. A passable developer will choose a data structure that can get the job done. High-quality developers choose data structures that have performance characteristics appropriate for their use case. As a developer gets better at his job, he knows more about implementation details and can make better decisions because of it.

The best use of knowledge is to prevent bugs in the first place. The first logical step is meaningful types on variables and functions. So much of what you can and can't do with data is specified by its representation. Leaving out basic representation information makes functions brittle or overcomplicated.

This haskell code
```
add :: Int -> Int -> Int
add a b = a + b
```

is functionally equivalent to this pseudo-python:
```
def add(a, b):
    if a is not int: 
        error("a is not int")
    if b is not int: 
        error("b is not int")

    return a + b
```

But this python code is strictly inferior, because you will not know if you've called it incorrectly unless you run your program. You can't know what it expects from its parameters without reading the body of the function.

Not only is there less knowledge available in the python code, it is harder to gain knowledge about it. The haskell code explicitly tells you what it expects of its input and output and will complain at compile-time if you've provided the wrong kind of data.

Limiting knowledge is also a false complexity economy. Preventing someone from knowing something critical to their work is actually worse than letting them know it--to figure out the information they need, they'll have to deduce it from manipulating some other stuff. Ugly.

# Agile, Better
Process should be responsive to the capabilities of the team.

If there are problems where one or two developers on a team quarterback meetings and impose their will on others, intermediate interaction between the quarterbacks and the rest of the team so that all members can have their say

## The story point tangle
If you set a capacity, devs estimate based on percentage of sprint length expected to be spent on a story.
If you set rough hour equivalents, devs use points as a proxy for hours which themselves can be seen as portions of sprint length.
Completed work's percetnage of committed work only approximates the quality of estimates, it doesn't actually show that more work is getting done. To tell if more work is actually getting done than expected, you have to expect specific features be done on a specific timeline.
# Pushing down
The natural boundary for services is exactly modification and access to the data of a single entity.
# The blahness of Method Chaining
Intermediate nouns are necessary to do fake composition using dot-notation.

```cs
ls.Where(o => o.Thing == 1).Select(o => o.Thing2).ToList()
```

vs.

```fs
ls |> where (fun o -> o == 1) |> map (fun o -> o.Thing2)
```

The C# chained version implicitly lazifies the calculation using iterators and does not materialize a result until specific operations are performed (e.g., .ToList()). Implicit lazification confuses many programmers, including experienced ones. 

In F# the operations are performed in sequence with intermediate representations due to strictness. To lazify the process, the programmer must explicitly do something to the operations. F# has a `lazy` keyword.

# The Knowledge Perspective (2nd Draft)
## Conventions and Constraints
In Javascript, all identifiers are suggestions. Anything could be in any identifier at any time.

This is bad enough:
```js
let x = (y, z) => { console.log(y + z); }
x(10); 
> NaN
x(10, 8);
> 18
x(10, "8");
> 108
x("8");
> 8undefined
```

But imagine if the second line was 
```js
setTimeout(() => { x = (y) => y - 18 }, 2000)
```

In Javascript, function declarations suggest how many parameters should be provided. You can pass more or fewer. You can pass any kind of data you want. The code in the function is responsible for verifying the data is in the right format. Reading the code in the function is *the only reliable way* to know what data it can use.

This is one big reason why javascript libraries often have such good documentation. You have no choice but to look to documentation if you want to know anything about a function or object exposed by a library. Reading the code is often a non-starter, because it's unclear where you should start, and once you do start you are liable to fall into many rabbit holes. In modern javascript, you can introduce classes which provide some clues about an object's structure but classes are far from guarantees.

You cannot *know* anything about a chunk of Javascript code aside from bare syntactical facts, like that this line tries to read this value from this object, or write that value to that object.

Making use of a library in Javascript is a matter of understanding the conventions of the library and carefully observing those conventions in the code you're writing. You have no way to know you've observed the conventions properly in a particular line of code until you run your program and it follows a code path that includes that line of code. This is why best practices dictate we should test code--automatically run through as many code paths as possible and verify results match expectations. This is delayed feedback on if you followed all applicable conventions properly.

What if you didn't have to learn the conventions, then manually implement them, then write tests to verify that you manually implemented them correctly?

## Control what varies
At the center of programming is a process where the programmer isolate what can vary that is pertinent to a problem domain and formalizes a series of rules for what should happen when these things vary in different ways with respect to one another. Text editors manage how the text within files can vary; Mapping applications manage how travel can vary; Spreadsheet applications manage how relationships between numerical values can vary. 
The user's input is the source of all this variance.

User interfaces are better when the user is asked for as little as possible to make use of the program. This can be re-framed as there being as few *things that vary* the user must know about and tweak to their specifications before the program can produce the result they desire. A music player only needs one piece of input from the user--a single variable that needs to be set--to play music: a filename. The system may provide other relevant information, like a volume level and sound device. The music player which requires fewer variables to be set is easier to use. The music player which requires fewer variables to be known in order to work is easier to program.

The problem with the javascript code I showed earlier is that *everything can vary*. You can count on nothing being stable. Programmers overcome this instability by producing reams of documentation. The documentation tells the world about all the conventions that this code follows, so that users can have some amount of faith that they will not launch nukes instead printing "hello world!" when they make an innocent function call.

Programming languages typically let you control mutation through a type system and enforcing immutability. Type systems limit the range of values which may be represented by an identifier. Immutability prevents the value referred to by an identifier from changing. Think of immutability as playing the role of a type system at the value level instead of at the identifier level.

Code written in the past constrains the code written in the future that depends on it whether you know about the nature of the constraints or not. This is unavoidable and source of endless frustration. 

For programs to do anything non-trivial, programmers need to represent knowledge about how a problem should be solved. Convention and formalism are substitutable in role of communicating this knowledge.

The compiler or interpretter can do more for you when it has more knowledge.Javascript optimization can be [quite challenging](https://nodesource.com/blog/why-the-new-v8-is-so-damn-fast) because the optimizer has to optimize based on [almost no information](https://github.com/thlorenz/v8-perf/blob/master/data-types.md#fast-in-object-properties) and rely a lot on live caching instead of known, efficient memory layouts and access patterns, as you'd see in a statically-typed language like Rust.

Mutability:
* Value - const vs. let
* Value Type 
* Type

Does minimizing mutability inherently cause low coupling and high cohesion?

Shells tend to tell you even less about functions--all are variadic and the only way to figure out how many params they take is to read all of their code, looking for parameter references.

```
foo() { echo $1 }
```

# Readability (1st Draft)
## An Insurmountable Problem
Each programmer has to learn what good code is themselves.

Usually this understanding is based on a series of simple guidelines, like DRY, YAGNI, keep functions short, and represent the domain with a class structure.

Most programmers, even those articulate enough to write about it and self-confident enough to share it with strangers on the internet, don't seem to show understanding beyond the level of having opinions copied from respected elders tempered by their own personal experience. 

Good code is, unfortunately, far from putting checks next to pithy benedictions from someone you look up to.

Goodhart's law applies to these readability aphorisms. As soon as you tell someone short functions make for good code, they'll shorten all their functions at the expense of readability. Once you tell someone to DRY off, their C code is littered with PhD-level macros in an effort to struggle past the language's minimal abstraction tools. In pursuit of YAGNI, abstractions are stripped from code until there is nothing that *could* be used again, even if it may make sense to try.

<Something about semiotics>

## My Approach to Readability
As a programmer, your goal is to produce working code that humans can maintain and extend. Good code is a robust dual speech act that convinces a computer to produce a desired result while also transparently conveying its intention to future human readers.

The industry uses the term "readability" to capture the human communication element of code. But, really, it should be *understandability*. Reading is a low bar. When people say "did you read X?", they often mean "did you get an understanding out of X comparable to mine?" It's not merely moving your eyes across the page and being able to vocalize the words, it is about ideas and connections. Similarly, what we want a future developer to be able to do is not merely to read our code; we want the reader to come away with a practical understanding of our code with minimal effort.

## Familiarity

Taking *understandability* seriously means taking the reader seriously as a participant in the process. There is no General Understander to whom we can show arbitrary code in any language and get a definitive judgment on its understandability.

Good code is a combination of contributions from the writer *and* the reader.

What we can understand easily is already familiar to us. If we're not familiar with a whole idea, we can see familiarity in its parts and do some mental work to apprehend its entirety by combining its parts. We pursue this process of finding-the-familiar fractally until we reach some point of commonality with the text. Sometimes we don't find such a point--that's when you throw up your hands and say "this is nonsense!". Or you can choose to make stuff up to fill in the areas you don't understand. In good code, we definitely don't want the former, and the latter, though it must happen sometimes, should be minimized.

Here are the levels of familiarity in code:
* conceptual familiarity - you know about conditional execution (if-statements, switch-case) but what about monads? free monads? 
* representational familiarity - you're familiar with C# syntax, but what about Haskell's for doing the same thing? Pattern matching vs. explicit if-statements with separate assignments.
* Idiom familiarity - combinations of concepts and representations produce different commmon patterns of convenient usage--these are like architecture's "desire paths" but in code.
* Domain familiarity - the problem domain itself consists of many abstractions we use to articulate problems and solutions outside of their representation in computers.
* Design familiarity - The intersection between programming idioms and domain. To solve specific problems in code, domain concepts can be represented, partially represented, or entirely left out based on the programmer's approach, while still producing a working solution.

Good code to someone who only has a low level of conceptual familairity will involve tons of comments explaining language constructs in common English. For a seasoned veteran, these comments are obnoxious and distracting.

We have no way of establishing a base level of familiarity that all good code should assume. It's just as unsafe to assume everyone is an expert at your language as it is to assume that readers have minimal domain familiarity. Even within a company among experienced coders, domain and design familiarity with different modules can vary tremendously. In complex modern languages it's not uncommon for several developers to have different idioms for writing code that may take some effort for their peers to understand. The flaw with these idioms--at least through the analytical lens of familiarity--is not inherent to the idioms; it's with the culture behind them and how that culture has not settled into the patterns which would make those idioms a common expectation and a welcome sight.

Most complaints about readability are mostly about familiarity. If you worked with code that looked a certain way for a while, you'd at first chafe at this or that idiosyncrasy, but after a surprisingly short time you'd accept that code as normal. At some point your perception flips: the formerly normal becomes weird.

* I went through this process when I switched from writing predominantly Java to using C# 90% of the time. The two languages have different conventions for casing of identifiers--I used to think pascal-casing method names looked bizarre and was difficult to read, but now I think camel-casing is off-putting. 
* The most common complaints I see about python are about its syntax's whitespace-sensitivity.
* I will never understand how people put up with this formatting of method calls: `doStuff ( int a , int b )`. Spaces around parens just *feel wrong* to me.

## Beyond familiarity
Once we get past familiarity, what are we left with? Expressing complex ideas with as few symbols as possible, and knowing they'll work before we run them. 

Leaky abstractions work against this.

Try to tier the call graph and remove cycles. Functions have dependencies just as classes and modules do, and that complexity accounts for the fine-grained readability of code. Adjacent code should work at a similar level of abstraction, and the calls it makes should be to functions whose code works at a similar level of abstraction.

The number of apparent lines of code of an operation should correspond to its value to the program. It's difficult to follow code when I have to wade through a dozen lines of logging logic in order to get to a function call that does all the work.

# Rust and Reimplementing Memory
Who should own long-term persistent data?
What if we need to represent various kinds of relationships it has to other data?

The graph itself shouldn't own the objects--they need to be used all over the place in various forms. Since the same object can have multiple relationships in the graph, Rc will be necessary with careful use of Weak to prevent the memory being locked up forever in a circular reference.

# The knowledge perspective
## Knowing more or less
You want to have to know as little as possible to use a tool. The best tools use your knowledge efficiently and require you to learn little in addition to a straightforward application of what you already know, and let you leverage new-found and extant knowledge to achieve your goal with minimal effort. 

For physical tools you might need strength and stamina along with some knowledge to make good use of them, but for abstract tools like software, it's all about knowledge.

All of our work as software developers is manipulating abstractions. We create and deploy our knowledge and the knowledge of our users to move bits around and, in the end, help someone get something done. It may seem obvious, but it bears repeating. Often it gets lost in the passion for programming itself, or in the pursuit of ever-harder puzzles to solve.

## From the User's Side
Programs are tools. The peculiarities of physical tools like hammers and screwdrivers usually relate to intuitive physics that you already know. You can often quickly learn additional required relevant intuitive with minimal experimentation. Software tends to be more complex and difficult to learn because it's all abstracted through icons and words, and the metaphors it uses to convey its operation can be misleading or weak or absent altogether. But more complex tools, like software, don't necessarily take more time to learn if the input and output are very clear and simple. It's not hard to learn that pushing a button on a machine makes food appear, even if the mechanism through which the food appears involves quantum tunneling across the known universe by the use of alien technology that manipulates n-dimensional artifacts you are incapable of seeing, let alone visualizing.

When you learn to use a tool you are "reading" knowledge off the tool through experimentation. You integrate it into your model of the tool and the various things the tool is used to modify. The more outputs, and the more complex the output and input patterns are, the longer it'll take you to master the tool. 

Text editors, for instance, can have very simple patterns of input and output: type text in and it gets stored into a file that you name. But within that you have an incredible variance in the complexity of the allowed input patters. Vim and Emacs both take a long time to learn to use well because there are so many ways of giving input. Choosing the right one (or even knowing about the right one) is quite a project. To build muscle memory for such complex tools requires repetition on a daunting scale and a willingness to suffer in the short- and even medium-term in order to gain productivity in the long term. There's a lot to learn. There's a lot of *knowledge* baked into the software that you can extract and use to be more productive with the tool.

## The Programmer's Side
Writing a program is creating knowledge that you or someone else is going to have to learn and keep in mind. The objective is to create as little knowledge as possible while solving the problem at hand. This means leveraging consistent behavior, powerful metaphors, and domain-based analogies to their fullest extent so that what knowledge the user (or other programmers working on the project) already has--or can quickly attain--can be used repeatedly, instead of requiring separate bits of hard-won knowledge to be harnessed in pursuit of the same solution. It's worse when you require more specific and non-generalizable knowledge from your user or collaborator. Learning is expensive! Everyone benefits when you make the best use of every bit of knowledge that you can beg, borrow, or steal from elsewhere. Cognitive ease means happy users and fellow programmers. From this we get some oft-repeated principles of good software engineering: 

* Don't Repeat Yourself (DRY) - Reusing code means less specific knowledge is needed, since you only represent the knowledge of the reusable code's operation once.
* You Ain't Gonna Need It (YAGNI) - Don't add additional features or capabilities to the system beyond what serves the requirements of the system direction. Don't create knowledge which isn't used.
* Keep It Simple, Stupid (KISS) - More complex solutions inherently involve more knowledge to understand. It's built into the word "complex." This is actually a restatement of YAGNI, but in the positive instead of negative.

These are all trying to convince you not to overengineer your code. Overengineering is creating too many abstractions--too much knowledge. This is the knowledge perspective on coding at a high level, but we can get way more concrete than this and create simple and useful guidelines that you can follow with every line of code you write.

On the small-scale of writing code, minimizing knowledge means 
* keeping the scope of each bit of state as small as possible, and
* limiting what can change as much as possible.

Purist OO design is wise to insist that access to state of objects should be as minimal as possible. The programmer has to worry about keeping track of fewer things if he knows that only a few members can be called and set externally. Use `const` or `readonly` everywhere possible. Fewer changeable things means you need to know less in order to safely use an object. Every individual piece of state that can change is a vector for bugs and the creation of more knowledge.

Pure functions and immutable data are the ultimate expression of knowledge-minimal code at the scale of a few lines of code or smaller. Functional programming is typically low-knowledge at its core, but exhibits an interesting property when it comes to abstraction. Because functional programming languages typically have expressive type systems, they provide unrivaled power to express knowledge about abstractions in a pleasingly minimal way, which invites the expression of relatively simple ideas in terms of combinations of existing abstractions. Powerful constructs like monads are clear and minimal abstractions, but of what? High-minded programmers tutorialize them endlessly because monads aren't *really* any*thing*, nor do they represent any *thing*--they're a pattern of knowledge. They're above the level of abstraction at which most programmers ever think; few programmers have a reason to think at this level. Such knowledge of abstractions is hard-won and powerful, but places a unique burden on others. Low-knowledge programming does not necessarily mean that the code will be easy to understand to the untrained. 

## Machines can help if you let them.
IDEs help programmers leverage knowledge about the program, automatically derived from the program's code, to inform future code as it is written. Declaring what abstractions are is way more valuable than you at first might imagine. We trade flexibility for hard knowledge. We can't know what an object in javascript will look like unless we run the program. Programmers anywhere can mess with the contents of any function and change any data. In contrast, we can glean lots of relevant data from a C# class about what objects of that class will look like when we run the program. We can use powerful type systems, like Haskell's, to further confine the universe of possible values that could flow through our program.

You may be tempted to think that "easy" programming is when you can just make stuff up and do what you want and the compiler or interpreter will turn it into some runnable format so that you can see if you did well or messed up. I think this view of ease is misguided and naive. What should be easy is not writing the code, but writing code that you know will come to the desired result as soon as you can possibly know. 

If the programming language forces you to know and articulate the meaning of symbols before you use them concretely, you can't just make stuff up and change anything you want to suit your whims at a certain time. It's less easy to just bash some code out. You have to think about the structure of your code up front--you have to think about particularly difficult questions of how to represent and manipulate information and processes from the real world. You have to do it up front and you have a very strict judge looking over your shoulder during the process who is making sure you're being consistent. This may seem like an onerous burden, but it's actually the burden *you must bear* to write code that works. Either you're doing more thinking up front, or you're doing more debugging later. 

All data that flows through your program will have to have some concrete facts about it that you know and make use of. Regardless of type system, you can't use a map or dictionary the same way you use a list, or tree, or int, and get the same results. Some data structures might be isomorphic to one another (you can implement one by using another) but you actually need to know what you can do with the data structure, and thus, indirectly, you have to know what the data structure *is*, at some level.

## Types are unavoidable, so embrace them
Types are a knowledge management tool--and a way of communicating to the compiler some knowledge that you want to keep stable, then the compiler takes care of the busywork of maintaining that stability.

## Frontiers in Knowledge
Telling your computer all possible knowledge about your program is not the best way of programming, because it costs effort to arrive at and specify unambiguously each piece of knowledge about the program. At some point, the effort you'd need to to understand the exact workings of a tiny super rare edge case far outweigh the benefits. Perhaps I'd draw the line somewhere short of Idris or Coq. 

I am open to expanding my boundaries, and I can feel my boundaries slowly inching forward to cover area I did not think I'd ever reach. I recently went from being highly skeptical of Rust's borrow checker's cost-benefit ratio to actually finding it alluring at best and interesting at worst. Perhaps I'm running into a version of the blub paradox with knowledge. Coq already is a proof assistant that can generate cases for you to fill in--this is a far more interactive way of building up machine knowledge of your program than we're used to. I'm excited to see if advanced type systems can be presented in a way where you don't need to vanish into a cave for a year to be able to make use of most of its power.
## Do Instead of Learn?
It's easier to learn something if you made it yourself--by making it you learned it! All the decisions were, at some point, wired together in your head so you could turn them into working code, so you have a huge head start on remembering how to do things with your code. But there's a powerful illusion at play here. There may be no more knowledge required in the new thing you made than in the thing you would've learned. In fact, you had to learn a lot more in order to make the thing that you made. You could've learned a subset of the features of an existing thing that works way better than the best thing you could write.

Here, you must rely on identifying where assumptions diverge between what code you'd write and what code you'd borrow. If assumptions diverge enough, you can minimize required knowledge by creating a purpose-built thing yourself.

## Low-knowledge Example: The Best API is no API
Wrapping functionality creates new knowledge. Evan Sangaline points out that React's philosophy is to use functionality already in javascript to create UIs instead of defining a bunch of wrapper functionality as angular does. React lets you use built-in functions to iterate through models and create views, whereas angular requires learning wrapper functionality like ng-repeat that serves the same purpose. https://intoli.com/blog/power-assert/

Power Assert adds some powerful difference-detection and friendly message generation infrastructure to javascript's built-in assert procedure. This is "no API", but it's also magic.
## Left-behind Material
Different languages have different amounts of information you can encode in types so that the compiler can check your work automatically. Object Oriented languages tend to have pretty simple checking. We just want to amke sure you are passing a Thing or at least a kind of Thing to this function. @Insert haskell is next, then idris. And the actual content that makes them more powerful than one another. Blub paradox comes into play?

This is why languages with more sophisticated type-checking tend to turn into proof assistants. Proofs and formal logic are how we state structural knowledge in unambiguous terms.

through defining classes in an OO language or providing type annotations (and your own types) in a functional language

Types are claims about compound data.
Types are necessary, because you've got a bunch of bits that can be read off of disk, RAM, and processor registers, and those bits are only useful in that they represent *something*. Perhaps they represent some number or letter--that's up to programmer's conventions to decide, though. The physical data as it rests on your computer is agnostic. Code gives meaning to bits. Programming languages give you the tools to create that meaning in different ways. We take a cacaphony of bits and use programming languages to turn them into structures--combine these bits interpretted as a number and these other bits interpretted as a string and now you're representing a person's height and name in a something you call a "person" record or struct. A type is a type of data in this way: it's a schema for making sense of a mass of bits.

in dynamic languages you often have to write the code that represents the same knowledge that's encoded in a compiler in a statically-typed language with an expressive type system. If you do not apply these constraints yourself, you are leaving yourself open to bugs. it would be absurd to check that every single value contained in a javascript object is actually what you think it should be everywhere it is used, though, so we skimp and pay the price later with runtime errors that are more usually more difficult to debug than a complie-time error.
# Basic programming language ergonomics: Take advantage of standard time metaphors in syntax.
The standard pattern of reading in western languages is left-to-right, top-to-bottom. Time metaphors place the past to the left and the future to the right, the past at the top and the future at the bottom. 

Code is more readable to the extent to which it follows the time metaphors of your native language.

The basic assignment expression in languages with C-style syntax contradicts this pattern. The output is on the left and the input is on the right, when temporally the input precedes the output.

```
output = 1 + input;
```

It would be more ergonomic for the sides to be flipped.

```
1 + input = output
```

Consider this like a sentence: `Store 1 + input in output.`

(We also run into another ergonomics challenge: comparison vs. assignment and alias vs. store.)

Another ergonomics concern mitigates the benefit of this rearrangement: if you're visually scanning, it's easier to locate the definition of a term if all of the terms being defined are visually aligned. That way the eye can scan directly upward or downward and does not need to try to parse out where the output of an assignment is indicated based on the position of special symbols like `=`. 

Verbs only take certain arguments.
Nouns can be in any of multiple positions

what about using time as a clearer indicator of how syntax should work? We already intuitively have this happen in imperative languages: typically we write code which sequentially proceeds top to bottom in the file. I think it's easier for people to think this way because it more closely mirrors the intuitive way to give directions to someone on how to do something. 

Within a line, though, this isn't the case. 

## Composition messes up time metaphors

In some programming languages most code is expressions and composition is the primary mode of combination. Composition establishes a pattern like this, for applying operations a, b, c, and d to value x in order

```
d (c (b (a x)))
```

As opposed to the imperative-style

```
var temp = a x
temp = b temp
temp = c temp
temp = d temp
```

I think F# has a great convention of using an operator to line up composition left-to-right.

```
x |> a |> b |> c |> d
```

This may be the most ergonomic way of composing functions with one starting argument.

# Store vs. Alias vs. Copy
Store - Put a new value in a new memory location and give it a name.
Alias - Give an in-use memory location an additional name.
Copy  - Copy value from one memory location to another and give it a name.

Because data and objects can nest, copies at one level of indirection may create aliases at deeper levels. (Shallow vs. deep copying; Copying the array pointer underlying the collection type instead of allocating new memory and populating it with the same values as the source collection.)

## Rust
Rust's ownership model implies these differences. Rc objects are alias managers.
Copying is implicit based on if Copy trait is on the struct.

Ted Kaminski's article [on objects and data](https://www.tedinski.com/2018/01/23/data-objects-and-being-railroaded-into-misdesign.html).
# Basic Ergonomics: Irregular Verbs
In human languages, when a verb is very commonly used it is more likely to have exceptional grammatical rules associated with it, like irregular conjugation. Ex. The verb "to go" is irregular in most languages.

A part of the compromise between a command and programming language that makes shell design so hellish is that commonly-used commands *should be short* and easy to type, yet they often mean something relatively complex. `mv a.txt b.txt` renames `a.txt` to `b.txt`, but stands for "move". 

Programmers have been taught that naming is critically important. You would never name a function or method "mv"--what the heck does that even mean?

But if a function is called a lot, perhaps it makes sense to give it a shorter name, even when you have the help of an IDE.

## Assignment
In an assignment statement, the variable whose value we're changing comes first, even though the change happens once the code on the right side has been evaluated.

`d = a.v(b, c)`
`d = v a b c` 
But what about
`a b c v d`

Inputs first, because you already have them, then the action and then outputs last.

It's debatable if the verb or the nouns should go first, because they're both "equally available".
input -> action -> output is pretty clear. 

A trivial pattern-matching `let` in Rust: `let Some(node) = head`

This is bad. What is Some(node) coming from? You have to look forward to determine it. It is a parallel construction to typical assignment operator usage, but the deconstruction aspect makes it unclear.

# Subject-object distinction
https://github.com/dotnet/csharplang/issues/164

From this proposal, it's clear that we want to be able to attach any method to any subject where it makes sense, independent of namespacing and object boundaries.

C# allows extension methods, and there's a proposal to allow extension in basically all ways to any type. This points out that the subject-object distinction is not in fact valuable. You want to define operations on data, and if that operation comes after your data's dot or someone else's dot is irrelevant to the operation. 

Functional programming languages tend to not believe in subject-object distinction at all, and their IDEs pay for it. Functions are module-qualified so we don't have too much namespace pollution, but if you want to see what you can do with a value of type String, it's tricky to do. You could search Hoogle, if you're using haskell, for functions of a type that has String on the left side of an arrow, but you'll get all kinds of stuff that won't make you happy.

# Side-effects
The lowest level element of programs is data. On the level humans deal with, the atomic unit is a function. Not a function as you think of them typically, though.

`a = 1` is not an assignment statement. It is a function that only causes the side effect of making `a` substitutable for 1 in some scope.

Rmemeber that every single piece of internal and public state of an object is implicitly passed to every instance method on that object when it's called.
# An if statement by any other name...
The correct use of inheritance is as a way of copying shared code among classes. This is isomorphic to composition + if-statements.

Inheritance and dynamic dispatch are fancy, obscured if-statements.

Isomorphic code: base class with an enum and switch-cases covering all enum values in its virtual functions.

The isomorphic code is more flexible, because you can have "derived class" chunks call one another or arbitrarily share code without compromising the structure of the code in an ugly way, such as referring to one child in another child.

Things get somewhat more complex when children need to store different data.

It's good to stack interfaces and use composition instead of inheritance.

# Abstractions
If statements whose conditions are all of the form `a == const b` can be expressed as a dictionary lookup in a dictionary from `b`s to behavior.

# Technical Debt
On a software project, everything you do generates technical debt.

Having requirements generates technical debt. You have to implement them and design them precisely. You're committing to future time expenditures of uncertain duration.

Every line of code you write cements into place a design which will have flaws and lead to rework for business reasons at some point in the future. Each line of code can imperfectly implement design decisions you didn't even know you were making. You only discover problems by stumbling into them, so the decisions you made before you stumbled into a problem represent a misunderstanding of the problem or solution which will inevitably manifest itself into technical debt.

# Simple and lost
## The Parable of Perfect Software
You've created a great product. It consists of simple, neatly-defined components with clear interfaces. They're all well-tested and performant. Their distributed deployment is tidy and uses the absolute best technology to accomplish its goals. All but one of your nodes could fail and it would not even bring your top-class service down for a second.

Six thousand years later archeologists dig up your infrastructure and wonder how any of it ever worked. They see a database, and a bunch of servers with filesystems packed with obscure software they have never heard of. Which bits of software are actually the world-renowned system you produced? Are these "permission denied" errors locking off anything they should know if they want to reconstruct your masterpiece? They search the museums for documentation, but can find only scraps, many of them point to software components that no longer exist, or hardware that cannot be found.

You were really good at your job--a 100x engineer--but during the civilizational collapse of 2040, it became a lot less important to document your software. You found it hard to just keep things running well enough that you weren't swarmed by hungry members of the underclass and torn apart. You had to fight tooth-and-nail to not be purged in the latest round of the semi-feudal government cleaning out the old elites and installing their own.

## The Wrong Abstraction Forever
When you lose most of your system, the wrong abstraction remains wrong forever. You can not trace where the abstraction trail leads. You cannot re-inline overcomplicated logic.

Testing deficits multiply issues many-fold. If you're re-inlining logic, you're changing code in several places across potentially a few modules. Tracing the effects of these changes and allocating testing resources can become a battle you'll never win.
# Too few tokens
point-free programming style leads to too few tokens. It's hard to think about point-free code because there are so many unlabelled potentially meaningful intermediate states. 

Breaking code into meaningful chunks helps the reader remember what the chunks do. The reader can hold a lot more ideas in their head when some smaller ideas are grouped into bigger ideas and labelled. Since you can store 5-9 chunks in short-term memory at once

# Sick with variations
Consider a humble function `getName :: Employee -> String`.

The `Employee` is actually a container for some fields. Let's say that employee is simple: `{ givenName :: String, familyName :: String, age :: int, country :: String }`. `getName`'s procedure is to select givenName and familyName and, depending on country, produce a single string representing the person's name as it would appear in that country's records.

There are multiple layers of selection going on here from within the structure of `Employee`. `age` is never used. 

When conceptualizing the complexity of this function, you should imagine it instead as a function `getName :: (String, String, Int, String) -> String`.

There are many possible things this function could do to create a string. Strings themselves are effectively lists of values, and thus can be used in an astounding variety of ways. So the function is more like `getName :: ([Char], [Char], Int, [Char]) -> [Char]`. Tons of complexity is possible from this--any element of each of those [Char] parameters can be combined with the others or with the Int to produce any individual element in the list of Chars that results from the function.

Now imagine if mutation was allowed. Brutal. Any of those items could change in any way. In my experience OO programmers are blithely unaware of just how much is assumed (by convention or laziness) about the contents of methods. They could change so many things, but they don't. You're very lucky that they don't, and when they do it can cause big, confusing, and hard to understand problems in inverse proportion to you knowledge of the codebase and problem domain.

Some languages, like C#, prevent you from mutating primitives passed directly into methods, but do not prevent you from mutating primitives which are in an object which is passed to a method, or in `this`. This just adds another layer of complexity to the picture--now you've got to know what is primitive and what is not, as well as dealing with the explosion of possible actions the method could perform because of possible selection and mutation of its inputs.

The name of the method puts some convention-driven common-sense constraints on what the method should do. But in a complex evolving system these constraints are subject to revision on a regular basis. Someone can come up with a reason to implement a new feature that requires the behavior of `fullName` to change, and now more data must be included. Maybe `fullName` populates a field on an object instead of just returning the `fullName` now.

In Rust code, it's useful to split various bundles of coherent state apart into separate structs so that they can be individually borrowed or moved. This minimizes the contention for resources and makes the borrow checker less of an enemy while writing code. This is called "state splitting." It's a very useful concept, because giving access to less state reduces possible variation in the callee.

Mutation control through unidirectional event flow in React/Elm. You mutate the state by submitting events that are reduced with the old state into a new state at each frame boundary.

Putting events on a queue instead of mutating the state directly means there's way less room for state to vary which means there are fewer places where invariants need to be enforced.

# Values as functions
```
y = 0
x = y + 5
y := 7
// change y
print(x)
```

What if `=` creates a function, where all free variables are parameters which are bound to the values they hold in the enclosing scope?

This turns the above program into
```
y = () => 0;
x = (y0) => y0() + 5;
y = () => 7;
print(x(y))
```

After all, what is the difference between y and y()? Both are nullary functions. This formulation makes all scopes explicit.

# Horses, carts, and short functions
I think that for the small function body idea to work, the programmer already has to be good enough to have arrived at a roughly readability-optimal function body length for the problems he's solving.

Worse programmers attempting "short function body" in solving a complex problem will push more state into the class-scope and make the code more side-effect laden, which is necessarily a decrease in code quality.

This is because the data dependencies between chunks of code are too complex to just put everything into arguments to functions--at least not without refactoring skills beyond those of the programmer in question.

There's also the problem of needless abstractions making certain state variable when it should actually be held constant over a certain period (which would be between two function calls that use that bit of state as an argument, for instance).

I think the short function body thing is a rule derived from looking at high-skilled programmers' code and using the mental model "if I tell people what this code looks like and they make code meet these metrics, it will be good code."

But really there are common underlying causes shared between good code and code with short function bodies.

The metric doesn't get you to the actual cause.

# Sets and Representations

What do types express? Sets only articulated by their disjunction with other sets? Contraints? Low-level metaphors for low-level storage?

How much semantics should types convey?

I imagine programming with types in a way where I'd rarely need to name parameters, because the function name and parameter type names carry all the meaning I need. Ex.  `createThing :: ThingSize -> Thing` as opposed to `int -> Thing`.

This brings up an interesting problem that OO creates: where do I put methods? They all have to be on some kind of object, but sometimes a method acts equally on two things. Since there are no implicit side-effect restrictions, role confusion results.

Order of arguments conveys information, so do names and types. But do we need to get all three right if arguments can be disambiguated by just one of them? The `Subject.Verb(DirectObject)` paradigm is very easy to grok, but what about more complex sentences? One with multiple Subjects? One with multiple objects, direct and indirect? 

# The crappy story of simplicity
https://lemire.me/blog/2017/12/06/simplistic-programming-is-underrated/

Only using simple constructs and ideas is not a sign of being smart. It doesn't make you an effective programmer. Simplicity is a matter of drawing clear distinctions and boundaries around abstractions and maintaining them in the face of a variety of needs without requiring contortions.

Refusing to abstract code because it is simpler otherwise is like refusing to use a big word where a paragraph will do. Do you want to read a book that uses only words well within your grasp, but takes pages to describe concepts where a polysyllabic word or apt metaphor will do?

C is simple, but in using it to solve complex problems its problems bite you very hard. Simple tools can combine well or poorly with one another. Combining the simple can often lead to way more cmoplexity than if you started off with some more abstract or somewhat more complex ideas. (Memory management, for instance.)

# Clean code? Cheap conventions.
https://www.youtube.com/watch?v=Fevz-Kb4bxc

Just use meaningful identifiers and balance creating new abstractions with keeping token count low.




# Abstraction in Action
I have a string like "2013.10153002" and I want to turn it into "2013.1015.3002" in one pass regardless of where the dots appear in the original string. Simple task, but provides a good simple problem that we can take from the most concrete to the most abstract implementation, illustrating the steps as we go.

Here is the "easiest" and most direct implementation. The very dumbest thing to do is to not even loop. Loops introduce an abstraction, and so do variables. But to program this without a loop would mean to fix the length of the input string that we handle.
```
string result = "";
int charCount = 0;
foreach (char c in desc)
{
    if (c != '.')
    {
        result += c;
        if (++charCount == 4 || charCount == 8) result += '.';
    }
}
```

# Static typing misses
(Inspired by https://blog.merovius.de/2017/09/12/diminishing-returns-of-static-typing.html)

The difference between static and dynamically-typed code is that static typing catches bugs before the code is run and dynamically-typed code catches them as the code runs. The bugs we're talking about are programmer mistakes like allowing null pointer access, or using a value of the wrong type in the wrong place.

All bugs are not created equal.

Since dynamically- and statically-typed languages both involve writing code that has expectations of its terms' capabilities and bit layout, they are both solving the same problem. It's not that dynamically-typed languages are avoiding the difficulties that static type-checking forces the programmer to grapple with. Dynamically-typed languages just delay the pain. Sometimes, this is non-problematic, because often the pain is so minute and rarely-encountered that spending time fixing it before you run the code is more expensive than fixing the bug after users or testers stumble upon it. For instance, if a certain feature is only used once a month, it's partially redundant with other features, and the bug causes some UI element to show a meaningless value in place of some usually-unimportant information in a label, you are unlikely to justify spending much if any time to fix that. Sometimes, getting the right value for that label is difficult given the other constraints on the system, and the bug exists because you tried to do it an easy way, but actually you can't do it that easy way. It might take you an hour to fix this, but even after years of usage by your customers they may never notice it.

The cost of resolving such issues increases superlinearly as you add more rigid constraints to the type system, like dependent typing and other proof requirements that require manual intervention (as opposed to the automated proof solving implicit in type-checking in an expressive static type system like vanilla Haskell's).

# The wisdom of the dot

IDEs have a much easier time completing code when you can give them some context, but they always do it in the order you type stuff. In functional languages you start with the name of a function--that gives the IDE nothing to work with.

Nim's option to put the first parameter to a function before the function is wonderful for this reason. It's also super low friction and quite readable in most situations.

```
let ls = [1, 2, 3]
assert ls.len == len(ls) # len's type is proc(array): int here.
```

parens are higher friction than typing a dot, so this is a huge gain. You also have no `this` pollution in functions, because you always explicitly specify all parameters to the function in the declaration--the dot notation is an optional convenience, it doesn't indicate any deep truth about scoping rules. This gains the advantages of the OO dot-notation without incurring the costs. The only big cost is that if you omit the parens from a one-param function (because you moved the only param to the leading position), it becomes unclear if the identifier represents a (cheap-to-access) field or a (relatively-expensive-to-call) one-argument function.

# Friction

## Naming Conventions
I love it when I can deduce useful semantic information from identifiers' names. It makes code way easier to read and understand. But some conventions require you to too-frequently press keys that are out of the way.

Pony code I read had initial underscores on many identifiers. Underscore is an annoying character to type. Don't make me hit it all the time to program. When I see underscores used to separate words in an identifier, I understand how that code can be easier to read since it more closely resembles words with spaces between them than camel-casing does. But don't require me to put an out-of-the-way character *before* most variable names instead of a way easier option like, say, lower-casing that variable name. All those little bits of friction pile up when I'm using a higher-friction convention in almost every line of code I write.

## Text Editors: Chords vs. Modes and Sequences

The beauty of vim is that the modal editing model means keybinds are very concise and low-friction through the use of a small amount of context. The one global bit of implicit context is the "mode" you are in: insert, normal, visual, etc.. In only one of those modes, most keys insert their corresponding characters into the buffer--insert mode. The other ones leave the whole keyboard open to binding. And instead of pressing keys simultaneously, as you do in typical application keybinds that rely on the control and alt and meta keys, in vim you're often pressing keys in sequence, and none of those keys are particularly out of the way. You're not pressing, say, ctrl+x and then some other key combination to do most things--you're just typing in the main area of the keyboard, your fingers straying little more than a row up or down from the home row. This is a lot less friction than, say, emacs or Microsoft Word during document navigation and editing, which is the primary activity of a text editor.

## Pattern matching vs. Declarations and if statements.
Pattern matching is super low friction compared to if statements and variable bindings for the same use case.

Haskell's
```
data Animal 
    = Dog 
    | Cat

speak :: Animal -> String -> String
speak Dog s = "Woof " ++ s
speak Cat s = "Meow " ++ s
```

vs C#'s
```
public enum Animal { Dog, Cat }

public static string Speak(Animal a, string s) 
{
    switch (a) 
    {
        case Animal.Dog: return "Woof " + s;
        case Animal.Cat: return "Meow " + s;
    }
}
```

There are several kinds of savings here:
* token savings: Haskell has 21 tokens (fewer if you omit the type signature and rely on inference), C# has 39 tokens. (I'm only counting literals as one token, though "Animal.Dog" is three.) 
* line savings: Haskell has 3, C# has 8. C# has 6 if you move the opening braces up a line, but that's non-standard C# formatting.
* locality: This is harder to measure, but the distance between introduction of symbols and their use is on average much smaller in haskell than in C#. `s` is introduced several lines above where it is used in C#, whereas in Haskell it's on the very same line.

## Now multiply
Don't think about these small additions of friction in terms of the absolute scale of one instance. Don't think about them as "well, they do the same thing in the end, so they're interchangeable." Think about it in terms of small numbers multiplied by large numbers. You're pressing thousands of keyboard shortcuts a day in emacs or vim. Most of the time you spend writing out code is typing out identifier names. If-statements and local variable declarations are endemic to even simple code. If you have to do less efficient things super often in a language, that's friction you'd be better off without. All of these design decisions must be taken in a broader context which could justify the added friction through other trade-offs, but it's easy to make a thousand sacrifices thinking all are insignificant, just to realize that in the end you've done way more damage than you had ever imagined.


# Types for representation, Constraints for safety

We can group functions into discrete algebras which can make use of one another. This maps to the concept of interfaces and interface inheritance in OO.

The types of terms should be in the form of constraints--what algebras they must satisfy minimally to work. "Int" or "Bool" are not this, they are representation strategies. Standard practice so far considers representation and valid algebras over that representation to be inseperable at a basic level. 

Names aren't enough, you need names and membership in some coherent whole. This membership is represented by grouping functions into interfaces or typeclasses. The grouping of the functions is important! You can't assume any function with the same name and signature-shape (not sure what a signature means in a constrained system) has the same meaning!

What you actually care about when you program is that values can be manipulated using algebras that have consistent results and follow certain laws.

Representations do sometimes get in the way, as in adding a float to a double.

OO tells us that internal representation should be encapsulated.

It's likely impractical to provide proofs that algebras are filling laws, but if we can pick out representations that the algebra can apply to, we can do property-based testing ala quickcheck.

Optimizing time and space in such a system becomes really tricky, because representations can change and this can have significant space and performance costs or benefits.


# Taking composition seriously

Haskell is hard because it takes composition seriously and we're not used to that as programmers. You can compose expressions without them leaking hidden state into other expressions that changes the result.

# Data abstraction, knowledge

In programming nexcom, I'm noticing that it's best to leave everything public. Restricting knowledge is not a particularly valuable thing to do when there's already a lot that can mutate. You have to make a bunch of methods that only expose specific mutations. But you don't know what mutations you'll actually need--what's in-bounds and out-of-bounds for an object. Responsibilities are unclear and are probably better left unclear. Uncoupling is expensive in complexity and lines of code and leads to a treacherous, circuitous logical flow.

https://medium.com/@chrisdaviesgeek/why-you-should-check-out-clojurescript-f31f64ac7d0e

Everything is a map or a list or a tree. Is this a good world? I'd say it's a semantically bare one. Just data is not enough. 

Javascript has multiple layers at which you can mutate objects.
1. the value within the object.
1. the member (you can remove any property or method from an object, like removing a key-value pair from a map)
1. the prototype. Though this doesn't mutate children that have already had the property set concretely on them, it can cause a lot of trouble if prototypal inheritance is harnessed to save time constructing objects with common properties and methods.

You can modify anything at any time and fundamentally break everything for more than just your own little corner of the world. 

Clojure solves this problem by being "data-oriented"--you use immutable maps and lists everywhere. You'll have to bring your own functions (or library functions) to the party. You can can change the structure of the map you get (by making a new map with some changes in it), but it will only effect code in the function creating the new map that actually uses the new map, and code outside the function will only be affected if it uses that function.

The data dependence is different here than in an OO language. The data dependence is articulated in function calls and using return values. The data is hanging out "above" the flow of code being changed by each chunk of code. The data-passing model is more transparent and clear. You can just run a function and know what will come out given what goes in. 

Purity is critical for this model to pay off. But clojure doesn't enforce purity or let you know when code is impure. You can hide mutation in functions and unwittingly sabotage a caller's data if necessary conventions aren't fully adopted. It's certainly easier to achieve purity than in javascript, but the necessary inclusion of Java interop leads to a thousand avenues back to side-effectful code.

Haskell uses types to control impurity. Though you can use global storage to work around Haskell's enforced purity, like writing data to files and mutating those files, that's a lot of extra work. The language makes it hard to do this, and if you're relying on data from files, you'll still have `IO a` types peppering your functions to tell you and everyone else that you're at risk of death by side-effect.

## But what about data-oriented programming?

Knowing the structure of data is important, especially if you want to verify that an operation is sensible without gathering a heap of test data first. For you to write code that uses data that's just a map, you have to know what keys might be around and what they mean. Types can help you with both of these problems. A record Type instead of a map can provide you with just what keys could possibly appear, and the types of the values of those keys can alert you to the actual meaning of the key: you can use hoogle to look up functions that operate on the type and get a good survey of what can be done with that type.

More knowledge is better. It takes time to formalize this knowledge into code, but once you formalize it you can rely upon it. It acts as a contract. A map is no contract--it's a loose conglamoration of conventions that you didn't agree to and have no definitive source of truth about which can change at any time without notice until a runtime crash occurs.



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


# Not so SOLID
Taming inheritance? Composing verbs makes more sense.

Inheritance is accretion-made-easy. Composition encourages simple components combined in various different ways. Understanding a bunch of simple components is a lot easier than making sense of the countless accretions of functionality and state change accumulated into the most concrete class in an inheritance hierarchy.

I don't see SOLID principles as being practical. Personal experience gives me the impression that top-down design principles that don't talk about the process of solving problems are missing something important and aren't valuable. The best you can do is keep it simple and hide knowledge.

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

One of the most important questions to be able to answer when reading code is "what is affected by this function call?" For pure functions you know that the only result is that a value is returned. In C-style mutation-centric languages any piece of memory in the program's purview could have changed. 

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
# --- Published ---
# Idiosyncrasies Always Accumulate
Visual Studio is a big piece of software. Millions of lines of code. It supports dozens of languages and hundreds of project types. It supports a project templating system which lets you create new project types yourself. It has a rich extension ecosystem which implies it also has a rich API for developing extensions. It has hundreds of keybinds to unique actions, so there is a lot you can possibly do.

Visual Studio is bulky and kind of slow.

It's easy to get frustrated with the bulk and heft of Visual Studio when you're using it all the time. "Why?" piles on "Why?" and soon the mountain of undesirable quirks and unnecessary-seeming slowness weighs heavily on your mind. The water, as David Foster Wallace would call it, disappears and all you see are the various impurities and contaminants that float in it all around you. Hours where the software was invisible and you were able to gleefully do your development work dissolve into nothingness the instant you are confronted by a spinner for no apparent reason, or intellisense mysteriously stops working, or source control just won't connect.

"If I did this myself, I could do so much better. Microsoft is a huge corporation and its incentives and culture are all messed up. They can't manage this thing, but I know I could."

There are several forces that push all software to be like Visual Studio as it grows. In this article, I will outline some of the big ones I've been able to notice.

At the core is the tension between well-factored code and shifting assumptions.

## Pressure From all Sides
Well-factored (read: structurally good, minimal) code typically has a module, class, or function/method dependency structure that resembles (or, ideally, *is*) a tree where more specific, idiosyncratic behavior is limited to the leaf nodes and the more shared behavior is pushed up towards the root of the tree. The dependency structure inevitably involves cycles at some point, making it formally more of a graph, but cycles are generally a bad sign for code quality at some level.
 
Idiosyncrasies are assumptions or decisions made during development that are inconsistent with other decisions made in similar circumstances. Idiosyncratic behavior surprises and frustrates and is the source of many bugs. Idiosyncrasies pile up as features are added or changed or deleted. They come in many varieties: UI quirks, exceptions in regions of code or architecture, using two different library calls to do the same thing, using two different UI metaphors to do the same thing, all kinds of terminological and technological inconsistencies specific to a module or submodule, etc.

Some small minority of idiosyncrasies are captured in documentation. But most idiosyncrasies age into invisibility quickly. The people that built them and the reasons for their construction pass into the void because of staff turnover and further technical changes. There's always more stuff to do, learn, and remember. Idiosyncrasies get snowed under by the weight of all the decisions various stakeholders and implementors must make in order to ship features. Underlying assumptions are constantly shifting in small increments when they aren't making noticeable big leaps.

You can imagine your code as a blob of dough which rests on a plate. Looking at the dough, you may not notice that the surface on which it rests has changed from a square into an octagon, and now some of the dough is lazily flopping over the sides. Assumptions shift beneath the code we write as more features are added on and it can be hard to notice if you're spending your time looking at the code and narrowly analyzing the features you have to implement now or in the near future.

When you're writing code, you may not have an available baseline against which to look for the kinds of inconsistencies that comprise idiosyncrasies. Even in medium-sized projects with a single developer, the developer can only hold so much in her head at once. Baselines shift or are lost as the code grows and the developer learns about the details of the problem domain. Refactoring to take new baselines into account seldom happens on more than a piecemeal basis since this kind of refactoring often modifies foundational abstractions which many submodules share. In larger codebases where many developers do or have done work, working without a grasp of the baseline can become the norm unless the organization spends significant effort on documentation and cultural upkeep.

The underlying inevitability: As you increase the number of features in a piece of software, the idiosyncrasy count increases. You must make more and more assumptions as you implement more features. Most of these assumptions are never acknowledged, let alone tracked.

Perfectly-factored code makes use of all possible simplifying assumptions so that it may limit scope and minimize LOC. When you add features, you are breaking some of these assumptions. New features change the shape of the ideal perfectly-factored code, sometimes in radical ways. When adding features, you increase the minimum complexity of the solution represented by your code. Even if you try to write code to be "easily changed", the surface of possible change is unstable. Users or product owners will not take long to come up with urgently necessary features that will either shed light on previously unknown assumptions by requiring you to break them, or ask you to break the very assumptions you had to make so you could factor the code for easy extension.

You will inevitably run into plenty of requirements issues which will lead to distortion of assumptions. Users and product owners will ask for features which they will not use as specified, because they do not understand the problem their feature suggestion solves well enough to come up with a good feature suggestion. You will then make a bunch of assumptions in implementing a largely useless feature. This feature then constrains all future development, introduces bugs in other components because of underlying library changes (in proportion to how close to perfect factoring you are), but serves no actual purpose. The feature will not be removed. It will become an eternal part of the useless scenery. Another inexplicable idiosyncrasy.

Eventually idiosyncrasies will accumulate to the extent that new and old team members alike will grow frustrated with portions of shared code and rewrite special isolated versions of them to achieve local ends in new features they are implementing. This pushes partial reimplementations of shared code into leaf nodes of the dependency tree and reduces the reliability of relevant up-tree abstractions. Once enough shared functionality has been rewritten into leaf nodes, developers can't trust that the invariants of the higher-level shared code will hold. Underlying shared state could have been changed by idiosyncratic re-implementations of core functionality which do not adhere to (and, likely, directly contravene for uncertain reasons) the invariants that the shared code once enforced.

Even necessary idiosyncrasies in well-implemented past features will constrain the implementation of future features. This often leads to bizarre results that frustrate users. Because component X relies on information from component Y that is particular to some other use case but not X's use case, the user has to enter more information that is seemingly irrelevant to the task at hand, or the user is constrained by missing pieces that will clearly not be used in the particular goal they're trying to achieve by using the software. Ex. Why do I need an Adobe Acrobat license to convert PDFs? All I want to do is use your media conversion software to convert a PNG to a TIFF.

## And I should do what?
Numerous natural and unavoidable forces in software development lead to the gradual accumulation of idiosyncrasies even if you're doing everything right. These idiosyncrasies will not disappear if we simply try to rewrite the world ourselves when confronted with bloated software that does more than we need. Most of the time we will retrace the steps of our forebears in our reimplementation, because we easily lose track of all the complexity that lurks under the surface in even simple software. 

Rewriting the world is attractive, though, because the idiosyncrasies we create in big rewrites are idiosyncrasies that we understand--we might not see them as idiosyncrasies at all--Not until we come back to the code months or years later and wonder why this project is so bloated and strange!
