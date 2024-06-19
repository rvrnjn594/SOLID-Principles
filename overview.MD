# Principles of Object Oriented Design

## SOLID Principles of Object Oriented Design

> Object-oriented hierarchy may seem like a simple concept to grasp, since there are so many examples in life to illustrate it. And this is not completely wrong: the basic idea behind object-oriented programming is simple, but the problem is that there are certain details, finesses and tricky situations, that may not be obvious, but demand a careful approach. Due to the apparent simplicity, young and inexperienced programmers often tend to make mistakes such as inheriting too many classes, having too many methods in one class, mixing functionality between classes etc., which may result in non-working code, or code that works, but isn’t very coherent, readable or easily upgraded.

This is why many computer scientists, engineers and “theoretical programmers” have dedicated their time to develop some rules and principles that would lead to good code.

- *S*ingle Responsibility
- *O*pen / Closed
- *L*iskov Substitution
- *I*nterface Segregation
- *D*ependency Inversion

### About SOLID

SOLID is a mnemonic acronym introduced by Michaek Feathers for the "first five principles" named by Robert C. Martin ("Uncle Bob") in the early 2000s.  
Here is excerpt from the author's blog, briefly explaining his reasons and motivation to create these principles:

> Of all the revolutions that have occurred in our industry, two have been so successful that they have permeated our mentality to the extent that we take them for granted.  
> **Structured Programming and Object Oriented Programming.**  
>  All of our mainstream modern languages are strongly influenced by these two disciplines.
>
> > Indeed, it has become difficult to write a program that does not have the external appearance of both structured programming and object oriented programming.  
> > Our mainstream languages do not have goto, and therefore appear to obey the most famous proscription of structured programming.  
> >  Most of our mainstream languages are class based and do not support functions or variables that are not within a class, therefore they appear to obey the most obvious trappings of object oriented programming.
>
> ---
>
> Dependency Management is an issue that most of us have faced. Whenever we bring up on our screens a nasty batch of tangled legacy code, we are experiencing the results of poor dependency management.  
> Poor dependency management leads to code that is hard to change, fragile, and non-reusable.  
> On the other hand, when dependencies are well managed, the code remains flexible, robust, and reusable. So dependency management, and therefore these principles, are at the foundation of the -ilities that software developers desire.

### The Principles

- In short, the single responsibility principle states that a class (or some other module) should only have one responsibility i.e. one reason to change.
- The open/closed states that software entities should be open for extension, but closed for modification.
- According to Liskov substitution principle, objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program.
- The interface segregation principle states that many client- specific interfaces are better than one general-purpose interface.
- The dependency inversion principle could be summed up in the sentence: **_"Depend upon abstractions. Do not depend upon concretions."_**
