**_Polymorphism is also explained at et end of the section, with type-casting included._**

# Liskov Substitution Principle

> The Liskov Substitution Principle is one of the SOLID principles of object-oriented programming (Single responsibility, Open-closed, Liskov Substitution, Interface Segregation and Dependency Inversion).

**These five principles combined together are used to make object-oriented code more readable, maintainable and easier to upgrade and modify.**

> Liskov Substitution Principle states the following:

**"in a computer program, if S is a subtype of T, then objects of type T may be replaced with the objects of type S (i.e. objects of type S may substitute objects of type T) without alterting any of the desirable properties of that program (correctness, task performed, etc)".**

> Simply said, any object of some class in an object-oriented program can be replaced by an object of a child class.
>
> In order to understand this principle better, we'll make a small digression to briefly remind ourselves about the concept of inheritance and its properties, as well as subtyping, a form of polymorphism.

### Inheritance, Polymorphism, Subtyping

Inheritance is a concept fairly simple to understand.

> It is when an object or a class are based on another object or class.
>
> When a class is “inherited” from another class, it means that the inherited class (also called subclass, or child class) contains all the characteristics of the superclass (parent class), but can also contain new properties.

This brings us to the next term we should explain, which is called polymorphism:

> objects can behave in one way in a certain situation, and in another way in some other situation.

**In object-oriented programming, this is called context-dependent behavior.**

Subtyping is a concept that is not identical to polymorphism.

> However, the two are so tightly connected and fused together in common languages like C++, Java and C#, that the difference between them is practically non-existent.

Formal definition of subtyping for the sake of completeness :

- “In programming language theory, subtyping (**_also subtype polymorphism or inclusion polymorphism_**) is a form of type polymorphism in which a subtype is a datatype that is related to another datatype (the supertype) by some notion of substitutability, meaning that program elements, typically subroutines or functions, written to operate on elements of the supertype can also operate on elements of the subtype.
- If S is a subtype of T, the subtyping relation is often written S <: T, to mean that any term of type S can be safely used in a context where a term of type T is expected.”

This brings us to the original **theme of the article – the Liskov Substitution Principle**

# Liskov Substitution Principle Examples

Liskov substitution principle (1988) states that functions that reference base classes must be able to use objects of derived (child) classes without knowing it.

Important for a programmer to noitce that, unlike some other Gang of Four principles, whose breaking might result in bad, but working code, **the violation of this principle will most likely lead to buggy or difficult tot maintain code.**

![Liskov Substitution Principle](https://springframework.guru/wp-content/uploads/2015/04/LiskovSubtitutionPrinciple_Simon.png)

Let's illustrate this in Java:

    class TransportationDevice {
        String name;
        String getName() { ... }
        void setName(String n) { ... }
        double speed;
        double getSpeed() { ... }
        void setSpeed(double d) { ... }

        Engine engine;
        Engine getEngine() { ... }
        void setEngine(Engine e) { ... }
        void startEngine() { ... }
    }

    class Car extends TransportationDevice {
        @Override
        void startEngine() { ... }
    }

> There is no problem here, right?  
> A car is definitely a transportation device, and here we can see that it overrides the _startEngine()_ method of its superclass.

Let's add another transportation device:

    class Bicycle extends TransportationDevice {
        @Override
        void startEngine() /*problem*/
    }

> Everything isn't going as planned now! Yes, a bicycle is a transportation device, however, it does not have an engine and hence, the method _startEngine()_ cannot be implemented.
>
> These are the kinds of problems that the violation of Liskov Substitution Principle leads to, and they can most usually be recognized by a method that does nothing, or even can't be implemented.

The solution to these problems is a correct _inheritance hierarchy_, and in our case we would solve the problem by differentiting classes of transportation devices with and without engines. Even though a bicycle **is a** transportation device, it doesn't have an engine.

> In this example our definition of transportation device is wrong. It should not have an engine.
>
> We can factor our _TransportationDevice_ class as follows:

    class TransportationDevice {
        String name;
        String getName() { ... }
        void setName(String n) { ... }
        double speed;
        double getSpeed() { ... }
        void setSpeed(double d) { ... }
    }

Now we extend _TransportationDevice_ for non-motorized devices:

    class DevicesWithoutEngines extends TransportationDevice {
        void startMoving() { ... }
    }

After extend _TransportationDevice_ for motorized devices. Here is more appropriate to add the _Engine_ object.

    class DevicesWithEngines extends TransportationDevice {
        Engine engine;
        Engine getEngine() { ... }
        void setEngine(Engine e) { ... }
        void startEngine() { ... }
    }

Thus our _Car_ class becomes more specialized, while adhering to the Liskov Substitution Princliple.

    class Car extends DevicesWithEngines {
        @Override
        void startEngine() { ... }
    }

And our _Bicycle_ class is also in compliance with the Liskov Substitution Principle.

    class Bicycle extends DevicesWithoutEngines {
        @Override
        void startMoving() { ... }
    }

### Conclusion

Object Oriented languages such as Java are very powerful and offer you as a developer a tremendous amount of flexibility. You can misuse or abuse any language. In the "Polymorphism" explains the "Is-A" test, discussed below. If you're writing objects which extend classes, but fails the "IS-A" test, you're likely violating the Liskov Substitution Principle.

---

---

# Polymorphism

**"The ability of an object to behave differently in different situations is called Polymorphism."**

> Concept is core to object oriented programmer and key to programming in Java.
>
> There are two types of polymorphism prevalent in Java:
>
> - Static Polymorphism
> - Dynamic Polymorphism
>
> As a Java developer, you will use each type of polymorphism.

### Types of Polymorphism

#### Static Polymorphism

In Java program, it is possible to have two or more methods in the same class having the same name but with different argument lists (**which is signature of a method**).

The argument lists can differ in the number of parameters, data type of parameters and the sequence of data type of parameters.

This is called **static polymorphism.** It is commonly known as **_method overloading._**

The correct method to be called is selected on the basis of the argument list.

**_Note: Return type of the method has no bearing on it's behavior in terms of static polymorphism._**

> Example of Static Polymorphism.
>
>       public class StaticPolymorphism {
>           void test (int a) {
>               System.out.println("Method A - The value of a is: "+ a);
>           }
>           void test (int a, int b) {
>               System.out.println("Method B - The values of a and b are: "+ a +", "+ b);
>           }
>           double test (double a) {
>               System.out.println("Method C - The value of a is: "+ a);
>               return a\*a;
>           }
>       }

In this example, three methods with the name of _test_ have been defined. Each differs in its argument lists.

> The name of all the three methods is same, but their argument lists are different. This is what makes them overloaded methods.

###### Static Polymorphism in Action

We can write a unit test for our example class to observe Static Polymorphism at work. In our test, each method is called with the proper argument list.

    public class StaticPolymorphismTest {
        @Test
        public void testPlymorphism() {
            StaticPolymorphism staticPolymorphism = new StaticPolymorphism();
            staticPolymorphism.test(12);
            staticPolymorphism.test(2, 3);
            double testValue = 1500;
            double result  = staticPolymorphism.test(testValue);
            System.out.println("Test Result is: " + result);
        }
    }

**Just like methods, constructors can also be overloaded.**
-We generally have two types of constructors, **default constructor and parameterized constructor.**

> **_Which among the default constructor or the parameterized constructor will get invoked, depends on the type of constructor which is invoked during the object creation._**

**We can use this() invocation to invoke one constructor from another one.**

> We just need to pass the proper parameters for invoking the appropriate constructor unisg the this() invocation.

Static Polymorphism is often used when you have a list of parameters for a method or constructor call and you wish to default some of the values.

**_You can use Static Polymorphism to provide alternate implementations of methods or constructors which supply default values for the optional parameters._**

#### Dynamic Polymorphism

Dynamic Polymorphism is a key concept in Object Oriented Programming.

> If you wish to become an effective Java programmer, you will need to have a firm
> understading of Dynammic Polymorphism.
> Consider the following class:
>
>       public class Vehicle {
>           protected String manufacturer = "Unknown";
>
>           public void vehicleName() {
>                System.out.println("I'm a vehicle.");
>           }
>       }

This is a simple class for the purposes of our demonstration. In Polymorphism terms we will be referring to this class as a base class.

Its a class you expect to extend with other classes.

> If you expect this class to never be instatiated, or if it should never be instantiated, it is a good programming practice to make the class abstract, so it cannot be used directly.

We implement dynamic polymorphism in Java by extending classes. Consider this example:

    public class Car extends Vehicle {
        private Integer numberOfWheels = 4;

        @Override
        public void vehicleName() {
            System.out.println("I am a car.");
        }
    }

> Here we have a Car object which extends our Vehicle class. We are free to add properties to our extended class as we have done with the numberOfWheels property.
>
> In this example, we are also overriding the vehicleName method of the base class. While you are not required to, in this example, we are using the @Override annotation on the vehicleName method.
>
> This tells the Java compiler you wish to override the method of the base class. If the signature of the method does not match a signature of a method on the base class a compiler error will be thrown.
>
> **This helps prevent you from accidently introducing a new method, rather than overriding the method of the base class.**
>
> It also aids in the readability of your source code for other programmers. Your intention of overriding a method of the base class is clear.
>
> While you are not required to use the @Override annotation, it is considered a best practice.

Through polymorphism, your base class can be extended to handle other use cases.

    public class Motorcycle extends Vehicle {
        private Integer numberOfWheels = 2;

        @Override
        public void vehicleName() {
            System.out.println("I am a motorcycle.");
        }
    }

> In the example above, we've extended our base Vehicle class with a Motorcycle class.
>
> Following the concepts of Object Oriented Programming, using polymorphism, we could have additional classes things such as Boat, Plane, Bicycle, Truck, Armored Tank.
> While each of our use cases are different, each is technically a vehicle.

This gets us to the classic **Object Oriented programming "Is A" test.**

- A Car _is a_ Vehicle.
- A Motorcycle _is a_ Vehicle.
- A Boat _is a_ Vehicle.
- A Armored Tank _is a_ Vehicle.

You are not limited to extending a class just once. Consider this example:

    public class Corvette extends Car{
        protected String manufacturer = "General Motors";
        private Integer numberOfWheels;
        private Boolean hasSupercharger;

        @Override
        public void vehicleName() {
            System.out.println("Zoom, zoom, I'm a Corvette.");
        }
        public void goFast(){
            System.out.println("Zoom.....");
        }
    }

Here we have a Corvette class which extends our Car class, which extends our Vehicle class.

- A Corvetter _is a_ Car.
- A Car _is a_ Vehicle.

It is common when using polymorphism in OOP for your extended classes to become more and more specialized.  
In our Corvette example, you can see how are new class has additioanal properties and methods specific to the Corvette object.

:p Consider how your class would change if it was a Plane or a Boat object.

###### Dynamic Polymorphism in Action

A child class object can be assigned to a parent class reference. The syntax for the same has been given below:

    Vehicle vehicle = new Corvette();

We can write a unit test using JUnit to demonstrate this with our examples so far:

    @Test
    public void testDynamicPolymorphism() {
        List<Vehicle> vehicles = new ArrayList<>();
        vehicles.add(new Vehicle());
        vehicles.add(new Car());
        vehicles.add(new Motorcycle());
        vehicles.add(new Corvette());
        for(Vehicle vehicle : vehicles){
            vehicle.vehicleName();
        }
    }

The output of this test is:

    I'm a vehicle.
    I am a car.
    I am a motorcycle.
    Zoom, zoom, I'm a Corvette.

> In our test, we used Java generics to create a list of Vehicles, then added an instance of each other extended types we have been working with.
>
> Our method call on vehicleName worked because each object in the list is a Vehicle.

**One caveat you need to be aware of is this is not a two way street.**

> Consider:

    1. Vehicle vehicle = new Corvette();
    2. vehicle.goFast();

> It will fail because the "Is a" test. While a Corvette is a Vehicle, a Vehicle is not a Corvette.

Remember that your extended classes will inherit from your base classes.

But if you declare your variable to use the base type, even if you assign the extended type to your variable, **the extended properties and methods will not be available. This is nature of a strongly typed language like Java.**

Naturally, you can use type casting to work around this:

    1. Vehicle vehicle = new Corvette();
    2. Corvette corvette = (Corvette) vehicle;
    3. corvette.goFast();

**But use caution with type casting.**

- In this example, if the vehicle was not an instance of a Corvette object, your program would fail on a runtime error.

### Conclusion

As you see in these examples, polymorphism is a very powerful concept in Object oriented programming. It gives you tremendous flexibility in composing your code. Like any tool in programming, polymorphism is something that can be misused or overused. However, once you master polymorphis, it will bring of elegance to your code. Your code will be easily read by others, and easy to maintain as your code evolves over time.
