---
layout: post
title: "Interview Question"
comments: true
categories: interview
---

## Database
1. get column difference of two table by a single sql?
2. get total table number of a database by a single sql?
3. Different between group by & where? is it write at same query? group by having implement? why needed ths?
4. Store Procedure: insert, update, rollback is on same store procedure. is it possible?
5. JOIN types & implementation?

### Angular
1. difference between Angular vs Angular Js, Angular 1 vs angular 2, angular 2 vs angular 4
2. what is Component in angular 4?
3. rootscope in angular 1?

### Java Collection Framework

1. How work HashMap?
2. Vector vs enum?

### OOP

1. interface vs abstract class
2. must override in which case?


### Spring 

1. what is Response params & its work?
2. is Vector thread safe?
3.    

## Java String


## What are the important features of Java 8 release?
1. Interface changes with default and static methods
2. Functional interfaces and Lambda Expressions
3. Java Stream API for collection classes
4. Java Date Time API

## Extra
ThreadPool
What is the benefit of using Optional in Java 8?
Why are Strings immutable in Java?
SOLID principles
N+1 Select problem in Hibernate



## OOP
###### High Cohesion vs Low Cohesion
High cohesion is when you have a class that does a well defined job. Low cohesion is when a class does a lot of jobs that don't have much in common.

Let's take this example:

You have a class that adds two numbers, but the same class creates a window displaying the result. This is a low cohesive class because the window and the adding operation don't have much in common. The window is the visual part of the program and the adding function is the logic behind it.

To create a high cohesive solution, you would have to create a class Window and a class Sum. The window will call Sum's method to get the result and display it. This way you will develop separately the logic and the GUI of your application.

