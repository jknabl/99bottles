# Chapter 3: Unearthing Concepts

* Refactoring for the sake of refactoring is not a good use of time. Refactoring because it 'might' make code easier to change 'in the future' is not a good use of time if there is no concrete change to be made.
* Make changes only when driven by requirements

* Code that needs to be changed frequently imposes higher standards for the code. Code that is never/rarely changed does not need to be changeable. 

> Conditionals are the bane of OO

## Open/Closed principle

* Start with this.
* Classes should be open to extensibility but closed to change. 
  * If you have a new requirement and the code is not currently open to the requirement, make the code open to the requirement. Then make the change.
    * If you don't know how to make the code open to the requirement, then start by identifying code smells. Then iterately remove the simplest ones.

* SOLID refresher
  * *S*ingle Responsibility: methods in a class should be cohesive around a single purpose.
  * *O*pen/closed: code/classes should be open to extension but closed to change.
  * *L*iskov Substitution Principle: a subclass must be substitutable for its parent class.
  * *I*nterface Segregation: classes should not be forced to depend on methods they do not use.
  * *D*ependency Inversion: depend on abstractions, not concretions.

* Open/closed principle
  * Don't conflate moving code around (refactoring) with the act of adding new features. The two acts are separate. When you have a new requirement, refactor so that the code is open to the requirement. Then implement the requirement.

* Reference: _Refactoring_ - Martin Fowler. 
* Reference: _Refactoring: Ruby Edition_ - Jay Fields

* While refactoring based on removing code smells, it may not be immediately obvious that the removal of the smell is related to solving the problem of adding your requirement. This is fine, and kind of the point. You are chipping away at the problem until the requirement can be implemented sensibly.

## Flocking rules

* Useful for finding a larger abstraction when it isn't readily apparent

1. Select the things in existing code that are most alike.
2. Find the smallest difference between them.
3. Remove the difference.

* Removing the difference will provide a smaller abstraction within the larger one.

### Focusing on difference

* In general it is more intuitive to start focusing on the sameness between things. It is more natural to start looking for the abstraction that links the concrete examples. But this is wrong-headed. 
* If two concrete examples represent the same abstraction and they contain a difference, that difference must represent a smaller abstraction within the larger.
  * If you can name the difference, you've identified the abstraction.

* General rule: the name of a thing should be one level of abstraction higher than the thing itself.
  * Names that are many levels of abstraction higher than the thing they name are problematic. They are overgeneral and lead to Speculatively General code, which is harder to understand and change than necessary.
    * If you can insert a level of abstraction between a thing and its name, you should demote the name of the thing to the lower level of abstraction.

* Reference: _Refactoring to Patterns_ by Joshua Kreievsky
  * Gradual Cutover Refactoring
    * Switch small pieces at a time rather than everything at once. This is less disruptive to ongoing projects and allows you to make changes without dedicating huge chunks of time to refactoring.
    * e.g. If you add a parameter to a method and the method has many 100s of callers, a strategy might be to provide the method with a default argument so that you can gradually update the callers.

