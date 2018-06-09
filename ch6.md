# Chapter 6: Achieving Openness

* Data clump: when pieces of data appear together in many places, they indicate a concept that can be extracted.
* When a clump gets sent as a collection of different parameters, the receiver often spends a lot of effort on 'clump management'. This is bad in itself. It can also lead to duplication when the clump is passed around to multiple different receivers.
* Remember: instead of injecting an object and supplying it with conditional behaviour, you should arrange such that you can inject the object and simply forward a message to the injected object.
* For removing conditionals operationg on a class, there are _State/Strategy_ and _Replace conditional with polymorphism_ techniques.

* Replace conditional with state/strategy
  * Removes conditional by dispersing branches into new, smaller objects. An object is supplied at runtime to determine what runs.
    * This is composition.
  
* Replace conditional with polymorphism
  * Removes conditional by creating one class to hold the defaults, and adding subclasses for every specialization (branch). An object is selected at runtime for execution.
    * This is inheritance rather than composition.

## Replacing conditionals with polymorphism

* Polymorphism recap: many different kinds of objects can respond to the same message.
  * Senders of a message shouldn't care _which_ receiver they are calling, just that whichever receiver it is responds to the message.
  * Allows senders to remain ignorant of the type and focus on the message.

* Provide a base class that executes the default behaviour. Specialized subclass for each unique case. 

* When several objects play a common role, there needs to be some code that decides which role-playing class to choose.
  * Code like this is said to 'manufacture' instances of the right kinds of objects, so this is called the _Factory pattern_.
* When a factory exists for a role, its sole responsibility is to create objects that play the role.
  * The factory should isolate the names of the concrete subclasses and to hide the logic to choose the correct concrete subclass.
  * Factories don't know what to do, they know the name of who does know what to do in certain cases.

* OOP fundamental: wilful ignorance of type. 

* Beware Liskov violations being created elsewhere when you create a new type.

* OOP (especially in dynamic languages) relies on having _explicit_ trust in the _implicit_ contracts between objects.
  * These contracts consist of the expectations about the messages to which other objects respond, and presumption about the contents of the messages.

* Failures of object trustworthiness == Liskov violations.

> Make the change easy (warning: this may be hard), then make the easy change. -Kent Beck

> When you write conditionals that supply behaviour, and put those conditionals in classes whose names other classes know, your code depends on concretions, and will break with every change.
> ...when you disperse behaviour into polymorphic objects, you can use factories to isolate both the names of the classes and the conditionals that choose them ... This loosens the coupling between objects and makes code open to change.

>Think of your code as a message in a bottle, written in haste for future readers. They'll always know more than you know now. Your job is not to be perfect, but to write a generous and sympathetic story. Tell them a story you can understand, and they'll cherish you forever.