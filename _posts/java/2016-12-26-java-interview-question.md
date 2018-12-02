---
layout: post
title: "un category : Java Interview Questions"
comments: true
categories: Java
---



1. What is difference between Heap and Stack Memory?

Heap memory is used by all the parts of the application whereas stack memory is used only by one thread of execution.
Whenever an object is created, it’s always stored in the Heap space and stack memory contains the reference to it. Stack memory only contains local primitive variables and reference variables to objects in heap space.
Memory management in the stack is done in LIFO manner whereas it’s more complex in Heap memory because it’s used globally.

For a detailed explanation with a sample program, read [Java Heap vs Stack Memory](https://www.journaldev.com/4098/java-heap-space-vs-stack-memory).

2. Java is Pass by Value or Pass by Reference?

Java is Pass by Value and Not Pass by Reference

First of all we should understand what is meant by pass by value or pass by reference.

- Pass by Value: The method parameter values are copied to another variable and then the copied object is passed, that’s why it’s called pass by value.

- Pass by Reference: An alias or reference to the actual parameter is passed to the method, that’s why it’s called pass by reference.

Example: Let’s say we have a class Balloon like below.

```
package com.journaldev.test;

public class Balloon {

	private String color;

	public Balloon(){}
	
	public Balloon(String c){
		this.color=c;
	}
	
	public String getColor() {
		return color;
	}

	public void setColor(String color) {
		this.color = color;
	}
}
```

```
package com.journaldev.test;

public class Test {

	public static void main(String[] args) {

		Balloon red = new Balloon("Red"); //memory reference 50
		Balloon blue = new Balloon("Blue"); //memory reference 100
		
		swap(red, blue);
		System.out.println("red color="+red.getColor());
		System.out.println("blue color="+blue.getColor());
		
		foo(blue);
		System.out.println("blue color="+blue.getColor());
		
	}

	private static void foo(Balloon balloon) { //baloon=100
		balloon.setColor("Red"); //baloon=100
		balloon = new Balloon("Green"); //baloon=200
		balloon.setColor("Blue"); //baloon = 200
	}

	//Generic swap method
	public static void swap(Object o1, Object o2){
		Object temp = o1;
		o1=o2;
		o2=temp;
	}
}
```

Output:

```
red color=Red
blue color=Blue
blue color=Red
```


3. Write a program to print all permutations of String?

This is a tricky question and we need to use recursion to find all the permutations of a String, for example “AAB” permutations will be “AAB”, “ABA” and “BAA”.

We also need to use Set to make sure there are no duplicate values.

4. What is platform independence?
Java code is compiled to class file & this class file can run to all ooperating system.Hence Java is platform independent.

5. Why java is so popular?
- Java is platform independent
- Object Oriented
- Robust
- Secure programming Language

6. Diiferent between C++ & java:
- Pointers: C++ has Pointers But There is no pointers in java
- Structures & Unions: in C++ ==> Class (Structure + methods) & Object in Java
- Memory management vs Garbage Collection in C++ ==> Class & Object in Java
- 


