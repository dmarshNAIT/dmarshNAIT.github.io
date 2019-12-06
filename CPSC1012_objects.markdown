---
layout: page
title: Objects & Classes
permalink: /cpsc1012/objects
---

# Classes & Objects

Classes define a type, objects model a thing.

Objects are individual instances of a class.

For example, we might define a class called `Dog`. Every dog will share characteristics (age, breed, colour, etc). Each individual dog (my dog, your dog) is an instance of the class `Dog`, and is therefore an object.

## Defining a Class
When you define a class, you describe the **characteristics** of its objects, using member variables or fields.
```csharp
class Dog {
    // instance fields, specific to an instance of this class:
    private int Age;
    private string Name;
} // end of class
```

When you define a class, you describe its **behaviour** using methods.
```csharp
class Dog {
    private int Age;
    private string Name;

    public void TakeWalk() {
        // code here
    } // end of method
} // end of class
```

### Access Modifiers

`private` members are only visible to the methods of the class defining the member (only methods of the `Dog` class have access to `Age` and `Name`).

`public` members can be called from methods in any class (so any class of object can call `TakeWalk()` on an instance of `Dog`).

## Instantiating Objects

To make an instance (or object) of the Dog class, we must declare the object and allocate memory for it.
```csharp
Dog bowser; // declare bowser to be an instance of Dog
bowser = new Dog(); // allocate memory
```
Alternatively, we can combine these:
```csharp
Dog bowser = new Dog();
```

## Constructors

When we define a class, we can define a constructor.

If we don't, the compiler will provide one automatically. Any member variables that weren't explicitly initialized will be set to default values (`int`s to `0`, `bool` to `false`, `string` to null, etc).

To create a constructor, we create a method with the same name as the class:
```csharp
public class Dog {
    // some instance fields go here

    public Dog (string theName, int theAge){ 
        ...
    } // end constructor

} // end of class
```

## Initializers

If certain member variables are going to have the same value when the object is created, we can initialize them:
```csharp
class Dog {
    private int Age = 0;
    // other fields and methods go here
} // end of class
```

## Accessors
Accessors are a type of `public` method that lets us **get** (or access) the value of a private field. 

For example:
```csharp
public int GetBalance() {  
  return Balance;  
} // end of method
```

## Mutators
Mutators are a type of `public` method that lets us **set** (or change or mutate) the value of a private field.

For example:
```csharp
public void SetAge(int Age) {  
    this.Age = Age;  
        // assign the value passed in as an argument to the Age instance field
} // end of method
```

## Overloading methods
This lets us have flexibility in what arguments can be passed into a method call.
```csharp
public class Dog {
    // some private variables
    // some methods
    public Dog (string theName, int theAge) { ... }
    public Dog (string theName) { ... }
} // end class
```