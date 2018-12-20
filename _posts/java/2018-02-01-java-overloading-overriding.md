---
layout: post
title: "Java Overloading Overriding"
comments: true
categories: Java
---

## Overloading in Java
#### Different ways to overload the method
There are two ways to overload the method in java

- By changing number of arguments
```
class Adder{  
static int add(int a,int b){return a+b;}  
static int add(int a,int b,int c){return a+b+c;}  
}  
class TestOverloading1{  
public static void main(String[] args){  
System.out.println(Adder.add(11,11));  
System.out.println(Adder.add(11,11,11));  
}}  

Output:
22
33
```
- By changing the data type
```
class Adder{  
static int add(int a, int b){return a+b;}  
static double add(double a, double b){return a+b;}  
}  
class TestOverloading2{  
public static void main(String[] args){  
System.out.println(Adder.add(11,11));  
System.out.println(Adder.add(12.3,12.6));  
}}  

Output:
22
24.9
```

### Overriding in Java
If subclass (child class) has the same method as declared in the parent class, it is known as method overriding in Java.

##### Rules for Java Method Overriding
- The method must have the same name as in the parent class
- The method must have the same parameter as in the parent class.
- There must be an IS-A relationship (inheritance).

```
class Vehicle{  
  //defining a method  
  void run(){System.out.println("Vehicle is running");}  
}  
//Creating a child class  
class Bike2 extends Vehicle{  
  //defining the same method as in the parent class  
  void run(){System.out.println("Bike is running safely");}  
  
  public static void main(String args[]){  
  Bike2 obj = new Bike2();//creating object  
  obj.run();//calling method  
  }  
}  

Output:
Bike is running safely
```

##### Understanding all java access modifiers

|Access Modifier| within class| within package| outside package by subclass only| outside package|
|------|------|------|------|------|
|Private | Y | N	| N |	N |
|Default|	Y	|Y	|N|	N|
|Protected|	Y|	Y	|Y|	N|
|Public|	Y|	Y|	Y	|Y|

