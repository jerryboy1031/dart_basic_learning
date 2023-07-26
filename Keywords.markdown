### Keywords *(as,final,await,static...)*
1. Abstract:

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

2. Static:

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
