---
layout: post
title: "Interview Question"
comments: true
categories: interview
---

## Database
1. get column difference of two table by a single sql?
    ```
    SELECT column_name,ordinal_position,data_type,column_type FROM
    (
        SELECT
            column_name,ordinal_position,
            data_type,column_type,COUNT(column_name) rowcount
        FROM information_schema.columns
        WHERE table_schema='test'
        AND table_name IN ('test','test1')
        GROUP BY
            column_name,
            data_type,column_type
        HAVING COUNT(column_name)=1
    ) A;
    ```
2. get total table number of a database by a single sql?
    ```
    select count(*) from information_schema.tables where table_schema=<db_name>;
    ```

3. What's the advantage of persist() vs save() in Hibernate?
     Sounds like both these methods behaves same when dealing with Transient Entity but differ when dealing with Detached Entity.
    
     For the below example, take EmployeeVehicle as an Entity with PK as vehicleId which is a generated value and vehicleName as one of its properties.
    
     Example 1 : Dealing with Transient Object
    
    ```
    Session session = factory.openSession();
    session.beginTransaction();
    EmployeeVehicle entity = new EmployeeVehicle();
    entity.setVehicleName("Honda");
    session.save(entity);
    // session.persist(entity);
    session.getTransaction().commit();
    session.close();
    ```
    Result:
    ```
    select nextval ('hibernate_sequence') // This is for vehicle Id generated : 36
    insert into Employee_Vehicle ( Vehicle_Name, Vehicle_Id) values ( Honda, 36)
    ```
    Note the result is same when you get an already persisted object and save it
    ```
    EmployeeVehicle entity =  (EmployeeVehicle)session.get(EmployeeVehicle.class, 36);
    entity.setVehicleName("Toyota");
    session.save(entity);    -------> **instead of session.update(entity);**
    // session.persist(entity);
    Repeat the same using persist(entity) and will result the same with new Id ( say 37 , honda ) ;
    ```
    Example 2 : Dealing with Detached Object
    ```// Session 1 
    // Get the previously saved Vehicle Entity 
    Session session = factory.openSession();
    session.beginTransaction();
    EmployeeVehicle entity = (EmployeeVehicle)session.get(EmployeeVehicle.class, 36);
    session.close();
    // Session 2
    // Here in Session 2 , vehicle entity obtained in previous session is a detached object and now we will try to save / persist it 
    // (i) Using Save() to persist a detached object 
    Session session2 = factory.openSession();
    session2.beginTransaction();
    entity.setVehicleName("Toyota");
    session2.save(entity);
    session2.getTransaction().commit();
    session2.close();
    ```
    Result : You might be expecting the Vehicle with id : 36 obtained in previous session is updated with name as "Toyota" . But what happens is that a new entity is saved in the DB with new Id generated for and Name as "Toyota"
    
    ```select nextval ('hibernate_sequence')
    insert into Employee_Vehicle ( Vehicle_Name, Vehicle_Id) values ( Toyota, 39)
    ```
    Using persist to persist detached entity
    
    ```// (ii) Using Persist()  to persist a detached
    // Session 1 
    Session session = factory.openSession();
    session.beginTransaction();
    EmployeeVehicle entity = (EmployeeVehicle)session.get(EmployeeVehicle.class, 36);
    session.close();
    
    // Session 2
    // Here in Session 2 , vehicle entity obtained in previous session is a detached object and now we will try to save / persist it 
    // (i) Using Save() to persist a detached
    Session session2 = factory.openSession();
    session2.beginTransaction();
    entity.setVehicleName("Toyota");
    session2.persist(entity);
    session2.getTransaction().commit();
    session2.close();
    ```
    Result:
    Exception being thrown : detached entity passed to persist
    So, it is always better to use Persist() rather than Save() as save has to be carefully used when dealing with Transient object .
4. What is the difference between update and merge method?
   1)	Update means to edit something.	Merge means to combine something.
   2)	update() should be used if the session doesn't contain an already persistent state with the same id. It means an update should be used inside the session only. After closing the session, it will throw the error.	merge() should be used if you don't know the state of the session, means you want to make the modification at any time.
5. What are the states of the object in hibernate?
   There are 3 states of the object (instance) in hibernate.
   
   Transient: The object is in a transient state if it is just created but has no primary key (identifier) and not associated with a session.
   
   Persistent: The object is in a persistent state if a session is open, and you just saved the instance in the database or retrieved the instance from the database.
   
   Detached: The object is in a detached state if a session is closed. After detached state, the object comes to persistent state if you call lock() or update() method.


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

 * design patterns and system design using SOLID principles
 * Java basic: 
 * **Solid Knowledge with OOP**
 * Java 8 Functional Program, Lamda Expression, java 7 vs java 8
 * Serializable
 * transient, volatile: The transient modifier tells the Java object serialization subsystem to exclude the field when serializing an instance of the class. The volatile modifier tells the JVM that writes to the field should always be synchronously flushed to memory, and that reads of the field should always read from memory. This means that fields marked as volatile can be safely accessed and updated in a multi-thread application without using native or standard library-based synchronization.
 * design patterns and system design using SOLID principles
 * Factory, Singleton, Integration Pattern (EIP)
 * Middle-wire micro service (ESB)
 * Spring Intigration Pattern
 * [Reactive Spring Webflux](https://www.youtube.com/watch?v=M3jNn3HMeWg)
 * REST vs SOAP
 * Authentication - SSO login/jwt/Spring security
 * Elastric search (DB)
 * Mongo DB
 * Spring-> Autowire, how autowire works internally? which types of autowire is using?
 * AOP-> Advantage
 * Testing-> Mockito/Automation(https://www.youtube.com/watch?v=8S8o46avgAw&t=87s)
 * Risk scalable
 * Test Matrix (https://www.youtube.com/watch?v=-2MIOtYG3Iw)
 * Design Component Diagram, 
 * UML diagram (https://www.youtube.com/watch?v=UI6lqHOVHic&list=PL_RvSWIduMYEZd6M7M0e5vSM_e0Jw5hUJ&index=1)
 * Communication- PMP
 * Docker 
 * Load Testing- Gatling/ scala based  (https://www.youtube.com/watch?v=U8nmVUBRmFQ)
 * Performance test
 * Smock test
 * Familiarity with Waterfall/Agile development best practices
 * Experience with build tools such as Maven, Gradle
 * [NGINX vs Apache](https://serverguy.com/comparison/apache-vs-nginx/)
 * [NGINX reverse Proxy](https://www.youtube.com/watch?v=E4MsBstIJMY)
 * [NGINX with Tomcat Load Balancing](https://www.youtube.com/watch?v=9SC1yabcz4k)
 * [NGINX Tomcat Clustering](https://www.youtube.com/watch?v=9gtpyqhd-NI)
 
 

