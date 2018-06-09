# Chapter 4: Practicing Horizontal Refactoring

* Recall flocking rules
  1. Select the things in existing code that are most alike
  2. Find the smallest difference between them.
  3. Remove the difference.

## Naming things

Say we have a conditional that produces 2 strings

```
if number==1
  "Take one down and pass it around"
else
  "Take it down and pass it around"
end
```

* When refactoring, we're removing the smallest difference. Here it is `one` vs `it`. 
* Names should be neither too specific nor too general. Here, `it_or_one` would be way too specific. `thing` would be way too general.

### Deriving names from responsibilities

* When you see things like `@instance.some_message(arg).to_s.capitalize.downcase.etc` it means the caller does not trust the receiver to return the correct thing. The receiver is forcing the caller to have a ton of knowledge about it in order to use it. This is bad.
  * Every piece of this knowledge is a dependency.
  * Reduce the number of dependencies imposed on message senders (generalization of Liskov)

* Liskov substitution principle reminder: every subclass should be substitutable for its parent class
  * Prohibits you from doing anything that would force a sender of a message to test the result in order to know how to behave.
  * Senders of messages having knowledge of return types and to treat them differently/convert them is a violation of Liskov.

* You don't have to understand the entire problem to find and express the correct abstractions. You just have to systematically chip away at the differences in similarities. Flocking rules recap: 
  1. Select the things in existing code that are most alike
  2. Select the smallest difference
  3. Remove the difference

* Note that if everyone who works on a codebase follows the flocking rules, their code would come out looking shockingly alike. This is super valuable in terms of team productivity.