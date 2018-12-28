---
layout: post
title: "Singleton Pattern"
comments: true
categories: Java
---

#### Java Singleton Pattern Implementation
* Private constructor to restrict instantiation of the class from other classes.
* Private static variable of the same class that is the only instance of the class.
* Public static method that returns the instance of the class.
##### Different approaches of Singleton pattern implementation 
1.	Eager initialization
2.	Static block initialization
3.	Lazy Initialization
4.	Thread Safe Singleton
5.	Bill Pugh Singleton Implementation
6.	Using Reflection to destroy Singleton Pattern
7.	Enum Singleton
8.	Serialization and Singleton


#### Eager initialization
In eager initialization, the instance of Singleton Class is created at the time of class loading, 

this is the easiest method to create a singleton class 
but it has a drawback that instance is created even though client application might not be using it.

```
package com.journaldev.singleton;

public class EagerInitializedSingleton {
    
    private static final EagerInitializedSingleton instance = new EagerInitializedSingleton();
    
    //to avoid client applications to use constructor
    private EagerInitializedSingleton(){}

    public static EagerInitializedSingleton getInstance(){
        return instance;
    }
}
```
#### Static block initialization

``` 
package com.journaldev.singleton;

public class StaticBlockSingleton {

    private static StaticBlockSingleton instance;
    
    private StaticBlockSingleton(){}
    
    //static block initialization for exception handling
    static{
        try{
            instance = new StaticBlockSingleton();
        }catch(Exception e){
            throw new RuntimeException("Exception occured in creating singleton instance");
        }
    }
    
    public static StaticBlockSingleton getInstance(){
        return instance;
    }
}
```

#### Lazy Initialization
``` 
package com.journaldev.singleton;

public class LazyInitializedSingleton {

    private static LazyInitializedSingleton instance;
    
    private LazyInitializedSingleton(){}
    
    public static LazyInitializedSingleton getInstance(){
        if(instance == null){
            instance = new LazyInitializedSingleton();
        }
        return instance;
    }
}
```

The above implementation works fine in case of single threaded environment but when it comes to multithreaded systems, it can cause issues if multiple threads are inside the if loop at the same time.
#### Thread Safe Singleton
```
package com.journaldev.singleton;

public class ThreadSafeSingleton {

    private static ThreadSafeSingleton instance;
    
    private ThreadSafeSingleton(){}
    
    public static synchronized ThreadSafeSingleton getInstance(){
        if(instance == null){
            instance = new ThreadSafeSingleton();
        }
        return instance;
    }
    
}
```

Above implementation works fine and provides thread-safety but it reduces the performance because of cost associated with the synchronized method.
Below code snippet provides the double checked locking implementation.
public static ThreadSafeSingleton getInstanceUsingDoubleLocking(){
    if(instance == null){
        synchronized (ThreadSafeSingleton.class) {
            if(instance == null){
                instance = new ThreadSafeSingleton();
            }
        }
    }
    return instance;
}

#### Bill Pugh Singleton Implementation
Prior to Java 5, java memory model had a lot of issues and above approaches used to fail in certain scenarios where too many threads try to get the instance of the Singleton class simultaneously. So Bill Pugh came up with a different approach to create the Singleton class using a inner static helper class.
```
package com.journaldev.singleton;

public class BillPughSingleton {

    private BillPughSingleton(){}
    
    private static class SingletonHelper{
        private static final BillPughSingleton INSTANCE = new BillPughSingleton();
    }
    
    public static BillPughSingleton getInstance(){
        return SingletonHelper.INSTANCE;
    }
}
```
When the singleton class is loaded, SingletonHelper class is not loaded into memory and only when someone calls the getInstance method, this class gets loaded and creates the Singleton class instance.
This is the most widely used approach for Singleton class as it doesn’t require synchronization. I am using this approach in many of my projects and it’s easy to understand and implement also.


#### Advantage of Singleton design pattern
Saves memory because object is not created at each request. Only single instance is reused again and again.
#### Usage of Singleton design pattern
Singleton pattern is mostly used in multi-threaded and database applications. It is used in logging, caching, thread pools, configuration settings etc.


Source: [**JournalDev**](https://www.journaldev.com/1377/java-singleton-design-pattern-best-practices-examples?utm_source=website&utm_medium=sidebar&utm_campaign=DesignPattern-Sidebar-Widget)