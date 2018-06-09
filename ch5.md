# Chapter 5: Separating Responsibilities

* Refactoring recipes don't promise to find you a solution (though they are more likely to than just blindly adding stuff). But refactoring is very easy to revert. So it is a safe way of productively exploring the problem domain.

* When things become very subtle and there are no obvious further refactorings to be made, time to identify code smells. Some questions to ask if none are obvious: 

1. Do any methods have the same shape?
2. Do any methods take an argument of the same name?
3. Do arguments of the same name always mean the same thing?
4. If you were to add the private keyword to this class, where would it go?
5. If you were going to break this class into two pieces, where is the dividing line?

* Technique: Squint Test
  * Put code you want to judge on your screen
  * Lean back and squint such that you can still see the code but can't read it
  * Look for changes in 
    * Shape
    * Color

> Superfluous difference raises the cost of reading code, and increases the difficulty of future refactorings
  * e.g. using multiple types of conditional form, ternary and if/then

> As an OO practitioner, when you see a conditional, the hairs on your neck should stand up. Its very presence ought to offend your sensibilities. You should feel _entitled_ to send messages to objects, and to look for a way to write code that allows you to do so.

* There is a big difference between a conditional that _selects an appropriate object_ and a conditional that _supplies behaviour_. The former is good and the latter bad.
* Code is "striving for ignorance", and preserving ignorance means minimizing dependencies.

* The 'name things at one higher level of abstraction' principle applies more to methods than classes. With classis, it's often best to stay close to the level of abstraction of the thing, to avoid being too speculative.

## Appreciating immutability

* It is perfectly possible to construct large, useful programs using only immutable falues (see functional programming)
* Immutable objects are very easy to reason about because they will never secretly change state. You are confident that what got created is what exists for the lifetime of the object.
  * By extension immutable objects are easy to test.
* Immutable objects are inherently threadsafe. No bugs re: separate threads mutating state of a shared object.
* The benefits of immutability are so great that _if it were free_ we'd choose it all the time.
  * Main downside is mostly in the creation of new objects.

> ...only two hard things in computer science: cache invalidation and naming things.
  * The 'cache invalidation' part is related to our immutability discussion.

* Costs of caching and mutation are related. If the thing you cache never changes, you never need to invalidate the cache. If you cache mutable stuff, you need complex logic that updates the cached copy whenever changed.

* Humans are bad at predicting in advance whether or not code will be fast/slow.
  * Writing code to solve performance problems before actual data proving the performance problems is not reasonable.

* Optimize for ease of understanding while maintaining acceptable performance. Optimize for performance only where absolutely necessary (and proven)

