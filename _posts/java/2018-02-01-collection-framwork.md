---
layout: post
title: "Collection Framework"
comments: true
categories: Java
---

## Collection Framework

#### List vs ArrayList
List is in interface while ArrayList is a class.

##### Why store ArrayList object on List variable?
You might have seen something like this:

```
List<Movie> listOfMovies = new ArrayList<Movie>()
```

here we are using a List as a type of variable to store an object of ArrayList class, created using new() operator.
 
The answer is to take advantage of Polymorphism. If you use interface than in future if the new implementation is shipped then you are not required to change your program. For example, any program written using List will work as expected whether you pass a LinkedList, Vector or ArrayList, because they all implements List interface, they obey the contract exposed by List interface.

The only difference comes in performance, which is actually on of the driver for change. In short, if you program using interface, tomorrow if a better implementation of your interface is available then you can switch to that without making nay further change on the client side (part of the program which uses that interface).