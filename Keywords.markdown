### Keywords *(as,final,await,static...)*
## 1. Abstract

Use when a class that doesn’t require a **full, concrete implementation of its entire interface.** That is, a class that implements an interface must provide actual code for all the methods declared in the interface.

  Interface here means a blueprint for defining a set of methods or behaviors that a class must implement.

In Dart, an interface is typically an abstract type, meaning it cannot be instantiated on its own.
The functionality of method (called "abstract method") in abstract class should have defined in **implementing class.**

```diff
@@ Abstract class @@
```
```dart
abstract class Vehicle { 
  void moveForward(int meters);
}
```
```diff
@@ its implementing class @@
```
```dart
// Can be implemented
class MockVehicle implements Vehicle { // implements "abstract class"
  @override
  void moveForward(int meters) {
    // definition here...
  }
}
```


Abstract classes cannot be constructed from any library
```dart
// Error: Cannot be constructed
Vehicle myVehicle = Vehicle();
```
### Summary:

Abstract class is like the menu, declares the name & type of methods(called abstract method), and lets other class that implements it define and use these methods. Also, it doesn't appear as an initialized object. The detail definition and functionality will in the implement classes.

## 2. Static

Use when implementing class-wide variables and methods. That is, we can use them without initializing an instance until they’re used.
```diff
@@ static class @@
```

```dart
import 'dart:math';
class Point {
  double x, y;
  Point(this.x, this.y);

  static double distanceBetween(Point a, Point b) {
    var dx = a.x - b.x;
    var dy = a.y - b.y;
    return sqrt(dx * dx + dy * dy);
  }
}

void main() {
  var a = Point(2, 2);
  var b = Point(4, 4);
  var distance = Point.distanceBetween(a, b); 
  //....
}
```

In main, the line `distance= Point.distanceBetween(a, b)`, we didn't initialize a class instance but directly implementing the method.
```diff
@@ How about "no static" @@
we need to call the method "on" an instance.
```
```dart
class Point {
  // ... same here
}

void main() {
  var a = Point(2, 2);
  var b = Point(4, 4);
  var distance = a.distanceBetween(b); // Call on the instance 'a'
}
```

### Summary:
- Static method:
Accessed directly from the class and does not require an instance of the class. Called using the class name
- Non-static method:
Associated with instances of the class and requires an instance to be created before it can be called. Called on the instance


## 3. Extends & Super
   
We use `extends` to create a subclass, and `super` to refer to the superclass.

**Warning: Extend only can inherit one class!!**
```diff
@@ Extends & Super example, override members@@
```

In this example, `Boy` is subclass and inherits `People` (superclass)  
```dart
class People {
    String name;
    int age;
    
    People(this.name, this.age);
    String introduce() => "I'm $name. Nice to meet you.";
}

class Boy extends People { //   `subclass` extend `super class` , only can inherit one class
    Boy(String name, int age): super(name, age);
    // we can call boy.introduce() !!(in main)
}
```

**Warning!! An overriding method declaration must match the method (or methods) that it overrides in several ways:**
- The return must be the same type as (or a subtype of) the overridden method’s.
- Argument types must be the same type as (or a supertype of) the overridden method’s. In the preceding example, the `contrast setter of SmartTelevision` changes the argument type from `int` to a supertype, `num`.
- If the overridden method accepts n positional parameters, then the overriding method must also accept n positional parameters.
- A generic method can’t override a non-generic one, and a non-generic method can’t override a generic one (what is generic? see next).

```dart
class Television {
  // ···
  set contrast(int value) {...}
}

class SmartTelevision extends Television {
  @override //indicate that you are intentionally overriding a member:
  set contrast(num value) {...}
  // ···
}
```

```diff
- What is generic method?
```

A generic method, also known as a parameterized method, is a programming concept. The method is defined with one or more type parameters that allow you to use the same method implementation with different data types, promoting code reusability and flexibility. The idea is similar to generic classes, but instead of applying to a whole class, it applies to a specific method.

By defining a generic method, you can write code that can work with multiple data types. This is particularly useful when you have algorithms or operations that are independent of specific data types, and you want to use them with various data types. Using generic methods can make your code more flexible and reduce the need for duplicate methods with slight variations for different data types.

In Dart, you can define generic methods using `<T>` to represent the type parameters. 

**The type parameters are placeholders for actual types that will be specified when the method is called.**

```dart
T first<T>(List<T> ts) {
  // Do some initial work or error checking, then...
  T tmp = ts[0];
  // Do some additional checking or processing...
  return tmp;
}
```

Here the generic type parameter on first (<T>) allows you to use the type argument T in several places:
- In the function’s return type (T).
- In the type of an argument (List<T>).
- In the type of a local variable (T tmp).

## 4. Show % hide

Using to import only part of the library
```diff
@@ show & hide example @@
```
```dart
// Import only foo.
import 'package:lib1/lib1.dart' show foo;

// Import all names EXCEPT foo.
import 'package:lib2/lib2.dart' hide foo;
```
### Summary:
- import `pkg` show `lib`: To import `lib` only.
- import `pkg` hide `lib`: To except `lib` from importing.

## 5. Assert
Use `assert(<condition>, <optionalMessage>)`. It will disrupt normal execution if a boolean condition is false.
```diff
@@ assert example @@
```
```dart
assert(urlString.startsWith('https'),'URL ($urlString) should start with "https".');
```

(1) `<condition>`: any expression that resolves to a boolean value.

If the expression’s value is true, the assertion succeeds and execution continues. If it’s false, the assertion fails and an exception (an AssertionError) is thrown.

(2) `<optionalMessage>` : error message.

   
## 6.  
