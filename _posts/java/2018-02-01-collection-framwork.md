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


#### ArrayList vs LinkList

Performance  :  Performance of ArrayList and LinkedList depends on the type of operation

a. get(int index) or search operation :  ArrayList get(int index) operation runs in constant time i.e O(1)  while LinkedList get(int index) operation run time is O(n) .

b. insert() or add(Object) operation :  Insertions in LinkedList are generally fast as compare to ArrayList.


|  | ArrayList | LinkedList |
| ------ | ------ | ------ |
| Implementation | Resizable Array |	Douby-LinkedList |
| ReverseIterator | No | Yes , descendingIterator() |
| Initial Capacity | 10 |	Constructs empty list |
| get(int) operation |	Fast | 	Slow in comparision |
| add(int) operation |	Slow in comparision	| Fast |
| Memory Overhead	| No | Yes |
