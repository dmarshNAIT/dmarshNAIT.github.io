---
layout: page
title: Objects & Classes
permalink: /cpsc1012/objects
parent: CPSC1012
nav_order: 12
---

# Classes & Objects

C# is an object-oriented language, so it is essential we understand what an **object** is.

- Classes define a **type**, objects model a specific **thing**.
- Objects are individual **instances** of a class.

For example, we might define a class called `Dog`. Every dog will share characteristics (age, breed, colour, etc). Each individual dog (my dog, your dog, that dog over there) is an instance of the class `Dog`, and is therefore an **object**.

## Defining a Class
When you define a class, you describe the **characteristics** of its objects, using member variables, also called instance fields.
```csharp
class Dog {
    // instance fields, specific to an instance of this class:
    private int _age;
    private string _name;
} // end of class
```
This means that I could create a `Dog` object that has the `_name` `"Jasmine"`, and another `Dog` object that has the `_name` `"Bowser"`. 

*Note: These instance fields are different from `static` fields which are associated with the class, not a specific object. The value of a `static` field is shared across all instances of that class.*

When you define a class, you can also describe its **behaviour** using methods.
```csharp
class Dog {
    private int _age;
    private string _name;

    public void TakeWalk() {
        // code here
    } // end of method
} // end of class
```

### Access Modifiers

`private` members are only visible to the methods of the class defining the member (e.g. only methods within the `Dog` class have access to `_age` and `_name`).

`public` members can be called from methods in any class (e.g. any class can call `TakeWalk()` on an instance of `Dog`).

## Instantiating Objects

To make an instance (or object) of the Dog class, we must declare the object and allocate memory for it.
```csharp
Dog bowser; // declare bowser to be an instance of Dog
bowser = new Dog(); // allocate memory
```
Usually, we can combine these:
```csharp
Dog bowser = new Dog();
```

## Constructors

When we define a class, we can define a **constructor** method.

> If we don't, the compiler will provide one automatically, but in this default constructor, any member variables that weren't explicitly initialized will be set to default values (`int`s to `0`, `bool` to `false`, `string` to null, etc).

To create a constructor, we create a method with the same name as the class:
```csharp
public class Dog {
    // some instance fields go here

    public Dog (string name, int age){ 
        ...
    } // end constructor

} // end of class
```

## Initializers

If certain member variables are going to have the same value when the object is created, we can initialize them:
```csharp
class Dog {
    private int _age = 0;                    // instance field
        // this is redundant because the default value for an int is already 0
    private static bool _isGoodBoy = true;     // static field

    // other fields and methods go here
} // end of class
```

## Accessors
Accessors are a type of `public` method that lets us **get** (or access) the value of a `private` field. 

For example:
```csharp
public int GetAge() {  
  return _age;  
} // end of method
```

## Mutators
Mutators are a type of `public` method that lets us **set** (or change or mutate) the value of a `private` field.

For example:
```csharp
public void SetAge(int age) {  
    _age = age;  
    // assigns the value passed in as an argument to the _age instance field
} // end of method
```

## Overloading methods
This lets us have flexibility in what arguments can be passed into a method call. Here is an example of overloading our constructor method:
```csharp
public class Dog {
    // some private variables
    // some methods
    public Dog (string name, int age) { ... }
    public Dog (string name) { ... }
} // end class
```

This means that I have 2 options when creating a new `Dog`: I can provide both the `Dog`'s `name` & `age`, or just their `name`.

## Static methods

If we declare a method as `static`, then it does not need an object to be called.

For instance, `Math.Round()` is a `static` method. I don't need to create a `Math` object in order to call it.

## What does this look like altogether?

<script src="https://gist.github.com/dmarshNAIT/35db61dde38abfab9cccb659076043ae.js"></script>