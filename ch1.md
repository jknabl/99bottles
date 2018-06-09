# Chapter 1 

* Basic premise of OO design: if you can accept increased complexity in some areas, you will get decreased complexity in others (changeability, flexibility, less dev time)
* DRYing out code involves a tradeoff: invoker of the method no longer knows behaviour, it just knows the message it is going to send. If you can accept that the invoker doesn't know the behaviour, then the benefit is when the behaviour changes the invoker doesn't need to worry about the details. 
* Catch-22: you can't create the right abstraction until you understand the code; but choosing the wrong abstraction may prevent you from ever fully understanding the code.

## 1.1: Simplifying code

* 2 somewhat contradictory goals for code: 
  * Concrete enough to be understood
  * Abstract enough to allow for change
* Extremes of the spectrum:
  * Concrete: large chains of only conditional statements.
  * Abstract: classes everywhere, only indirection

* Consistency in code:
  * e.g. mixing ternary and `if/then` conditionals
  * The function is fine, but there is increased cognitive load when you mix styles. This is a cost people other than you will have to pay. 
* Duplication in code suggests concepts that have not been isolated and *named*. 
  * This also increases cognitive load for others trying to understand the program
  * Also increases chance of subtle bugs being introduced
* When _you_ write code, you know what it does. It is not going to be obvious to _everyone else_ what the code does. So extracting *concepts* into methods with good, descriptive names is extremely important.
* Judging code quality is hard, but some benchmarks: 
  1. How difficult was it to write?
  2. How hard is it to understand?
    * Code is easy to understand _when it clearly reflects the problem it is solving and exposes the problem's domain_.
      * If code does not reflect its domain clearly and obviously, you can infer that it was difficult to write, and it will probably be obvious that it is difficult to understand.
  3. How expensive will it be to change? 

* Overly general code can expose the problem domain reasonably well yet still be difficult to understand. If there are too many levels of indirection or if there are too many concepts than the minimum needed to solve the problem, then the code probably cost more to write than it is worth. It may also cost more to change in the future than was necessary.
  * For example you might end up with a solution wherein a few of the classes you've written contain all the information you need to solve the problem. But you add a bunch of abstraction around them that handle processing like dispatching or listening. These additions can be 'speculative' in that they are not immediately necessary but they 'might' help in the future. But the cost of the additional complexity is probably not worth the slim chance that there is a benefit once the scope of the problem expands in the future. 

* *Reminder*: a good way to check whether or not you're going wrong when writing code is to ask whether or not it obviously exposes characteristics of the problem domain. 
  * e.g. How many Invoice variants are there? How are the variants alike/different? What determines state transitions between variants? 

> DRY makes sense when it reduces the cost of change more than it increases the cost of understanding the code. 

* e.g. of 'bad' concreteness: naming a method after its implementation _right now_. 
  * If we wrap a string 'beer' in a method `def beer`, and there are a bunch of other supporting methods that reference beer (e.g. `print_beer`, `show_beer`) then we are in for a world of hurt when beer needs to change to Kool-Aid.
* To mitigate, _name things after what then MEAN (represent in your problem domain) not what they do_.
  * In the 99 bottles song, 'beer' is 'the beverage that is drunk', not 'the beer'. So methods involving beer should reflect tht they are the beverage, not be concrete and refer explicitly to the beer.
* _Name methods after the concepts they represent, not how they behave_

* "Shameless Green" code -- solves the problem in the simplest way possible, considering future change _only to the extent that change will be likely_. 
  * e.g. in the case of the 99 bottles song, it is highly unlikely that the song will ever change. And we don't need to build a "song printing" application, we just need to print the 99 bottles of beer song. 

## 1.2 Judging code

* SLOC (source lines of code) is not an accurate metric for a number of reasons. One is experienced programmers tend to write more terse code than novices. So there is an incentive to write bad, verbose, overly-concrete code when SLOC is the metric.
* _Cyclomatic Complexity_: an attempt to measure the 'modularity' of code. 
  * Counts # of unique execution paths through code
  * Aims to identify code that is difficult to test/maintain.
  * Can be useful when e.g. comparing 2 different ways of writing the same thing. But is not useful as a catch all 'good code bad code' metric
* _Assignments, Branches, and Conditionals_: Counts:
  * Variable assignments
  * Branches as in _control branches_ (function calls/message sends)
  * Conditionals
  * There is an ABC tool for ruby called FLOG: http://ruby.sadi.st/Flog.html
  * High ABC numbers indicate code that requires a lot of 'mental space'
  * This can be a reliable way of testing complexity of your code!

* *Shameless Green*: the solution that quickly reaches green (tests) while prioritizing _understandability_ over _changeability_. 
  * Uses tests to drive comprehension
  * Accumulates concreteness until sensible abstractions are revealed <-- neat
  * Probably a good place to start for most problems.
