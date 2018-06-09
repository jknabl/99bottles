# Chapter 2: Test Driving Shameless Green

* TDD; red-green-refactor cycle.
* Create the goal of reaching green first above all else (by writing good tests that specify the problem well)
  * Strive for 'Shameless green' discussed previously; prioritize understandability without concern for changeability.
    * This does not mean changeability isn't important; it's just that getting to green quickly is somewhat at odds with writing changeable code.

## 2.2 Writing the first test

* It is tempting to think about the 'right' stuff to test first. But this is a trap. Testing what is 'important' first doesn't matter -- just test anything, and revise your assumptions about the problem if as you go they turn out to be incorrect.

* Wearing 2 hats when doing TDD:
  1. Writer of tests: keeping your eye on the big picture and working forward with the problem in mind.
  2. Writer of code: unconcerned with anything but reaching green.

* Stripping down conditionals to contain _only the things that change_ in a piece of logic.
* Use the testing process to gradually move the code from concrete to general, but only as needed.

* Ref: [The Transformation Priority Premise - Uncle Bob](https://8thlight.com/blog/uncle-bob/2013/05/27/TheTransformationPriorityPremise.html)

> As the tests get more specific, the code gets more generic

* _Transformations_: simple operations that change the behaviour of code. Counterpart to a refactoring.
  * Transformation Priority Premise: the simplest transformation should be prioritized for any given code change when aiming to reach green (e.g. interpolating a variable might be simpler than adding a conditional, and thus it should be chosen)

* At times it may be counterproductive to DRY stuff out prematurely. Say you notice some repetition across 2 conditional branches in a method. A small part of the repetition can be DRYed out maybe by e.g. extracting out a 'pluralization' method. But this makes the code more difficult to understand, and hiding the repetition actually makes it _more difficult to unearth the broader, more fundamental concept_. So in this scenario you should actually _keep_ the duplication until you test some more stuff and unearth the concept you are dealing with.

* When deciding whether or not to DRY, it can be helpful to ask: 
  * Does this change make the code harder to understand on immediately reading?
  * What is the future cost of doing nothing now?
    * If it is not more difficult in the future to make a change when you do nothing, then do nothing!
  * When will the future arrive? When will I get more information?
    * At the beginning of an implementation, as you're writing the initial tests, information comes very quickly as you flesh out the problem domain and solution. So it is fine to tolerate duplication as you clarify the concepts.

* When writing Shameless Green, express the unambiguous abstractions but avoid grasping for the not-quite-visible ones! You can write those when they become clear, as you've worked through the problem.

* `if/elsif` vs `case`
  * `if/elsif` implies that each comparison differs in a meaningful way, that the reader needs to examine each one carefully to understand the conditional logic.
    * If the conditions don't vary in a meaningful way -- e.g. if each just checks that a number is equal to a value -- then you waste a lot of the reader's cognitive energy by having them inspect each case carefully.
  * Conditions in `case` statements are fundamentally the same, and are quicker to read because of that.

* Think of reaching Shameless Green as being on an X/Y plane. You want to move horizontally as fast as possible, just writing stuff that works. Trying to find abstractions causes vertical increase and slows down reaching green -- you want to avoid this. Move along the horizontal path until you've got a fully specced-out Shameless Green solution.

## Exposing responsibilities

> Duplication is useful when it supplies independent, specific examples of a general concept you don't yet understand.

* "Fake it till you make it" with your tests. Doesn't matter if as you write tests, the implementations you come up with to pass them are goofy. The more goofy stuff you write, the more the non-goofy solution exposes itself. Faking it helps to suggest the actual solution over time.

* *Triangulation*: testing pattern introduced by Kent Beck. Aims at helping to uncover abstractions.
  * Write multiple tests at once, write an implementation that will make them _all_ pass.
  * This is exposing a general pattern from multiple, specific examples.
    * Note that this is exactly what Shameless Green is for code rather than tests.

* Knowledge that one object has about another creates a dependency. Dependencies couple objects together and increase the cost of change.
  * e.g. consider asking a caller to call `@bottle.verses(99,0)` vs. `@bottle.song`. 
    * In the former, the caller needs to know about `Bottle`'s implementation of `#verse`. In the latter, the caller just knows it wants the song (better)

* Your goal as a _message sender_ is to _incur as few dependencies as possible_.
* Your goal as a _message provider_ is to require as few dependencies as possible.

> TDD does not claim to be free, merely that its benefits outweigh its costs.

* Tests should confirm _what_ your code does without any knowledge of _how_ the code does it.
  * e.g. when testing a `Bottle#song` method, if it just asserts that `#song` produces the same output as `#verses(a,b)`, you're screwed when `#verses(a,b)` changes, because `#verses(a,b)` is the current implementation of `#song`. In other words, you aren't testing that `#song` returns the song you want in this case... You're testing that the implementation of `#song` matches your current expectations.

> Tests are _not_ the place for abstractions, they are the place for concretions. Abstractions belong in code.

>The Shameless Green solution is neither clever nor extensible. Its value lies in the fact that the code is easy to understand, and cheap to write. If nothing ever changes, this solution is quite certainly good enough.
