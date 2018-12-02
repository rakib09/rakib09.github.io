---
layout: post
title: "Java Garbage Collection"
comments: true
categories: Java
---

## Java Garbage Collection
There are many ways:
- By nulling the reference
```
Employee e=new Employee();  
e=null;  
```
- By assigning a reference to another
```
Employee e1=new Employee();  
Employee e2=new Employee();  
e1=e2;//now the first object referred by e1 is available for garbage collection  
```
- By anonymous object etc.
```
new Employee();  
```

### finalize() method
The finalize() method is invoked each time before the object is garbage collected. This method can be used to perform cleanup processing. This method is defined in Object class as:
```
protected void finalize(){}  
```
Note: The Garbage collector of JVM collects only those objects that are created by new keyword. So if you have created any object without new, you can use finalize method to perform cleanup processing (destroying remaining objects).

### gc() method
The gc() method is used to invoke the garbage collector to perform cleanup processing. The gc() is found in System and Runtime classes.
```
public static void gc(){}
```  
Note: Garbage collection is performed by a daemon thread called Garbage Collector(GC). This thread calls the finalize() method before object is garbage collected.