---
layout: post
title: "Java SOLID Principal"
comments: true
categories: Java
---

# SOLID Principles:
- Single Responsibility
- Open for Extension/Closed for Modification
- Liskov Substitution
- Interface Segregation
- Dependency Inversion

### Single Responsibility

A class should do one and only one job.
Principle violation example (bad):

```
Principle violation example (bad):

public class TechnicalStaff {
    private int id;
    private String fname, lname, title;
    private Date dob, dateOfJoining;
    //Getters & setters
    ...
    void maintainSystems(){}
    void performAppraisal(){}
    void promoteEmployee(){}
}

Principle adherence example (good):

public abstract class Employee {
    private int id;
    private String fname, lname, title;
    private Date dob, dateOfJoining;
    //Getters & setters
    ...
}

public class TechnicalStaff extends Employee {
    void maintainSystems(){} 
}

public class Manager extends Employee {
    void performAppraisalOfDirectReport(TechnicalStaff employee){}
    void promoteDirectReport(TechnicalStaff employee){}
}
```

### Open for Extension/Closed for Modification:
Software entities should be Open for extension, but closed for modification.
```
Principle violation example (bad):

public abstract class Employee {
    private int id;
    private String fname, lname, title;
    private Date dob, dateOfJoining;
    //Getters & setters
    ...
}

public class TechnicalStaff extends Employee {
    void maintainSystems(){}
}

public class Manager extends Employee {
    void performAppraisalOfDirectReport(TechnicalStaff employee){}
    void promoteDirectReport(TechnicalStaff employee){}
}

Now when your company expands and you start employing Non Technical Accounting Staff, you will need to alter existing Manager class as follows:

public abstract class Employee {
    private int id;
    private String fname, lname, title;
    private Date dob, dateOfJoining;
    //Getters & setters
    ...
}

public class TechnicalStaff extends Employee {
    void maintainSystems(){}
}

public class Accountant extends Employee {
    void maintainAccounts(){}
}

public class Manager extends Employee {
    void performAppraisalOfTechnicalStaff(TechnicalStaff employee){}
    void promoteTechnicalStaff(TechnicalStaff employee){}
    void performAppraisalOfAccountant(Accountant employee){}
    void promoteAccountant(Accountant employee){}
}

This is bad since you will need to keep adding new methods to Manager as and when new Employee types are recruited.

Principle adherence example (good):

public abstract class Employee {
    private int id;
    private String fname, lname, title;
    private Date dob, dateOfJoining;
    //Getters & setters
    ...
}
public class TechnicalStaff extends Employee {
    void maintainSystems(){}
}
public class Accountant extends Employee {
    void maintainAccounts(){}
}
public class Manager extends Employee {
    void performAppraisalOfDirectReport(Employee employee){}
    void promoteDirectReport(Employee employee){}
}
```

### Liskov Substitution:
A child class must be able to completely substitute and act-in for it’s base(parent) class.

```
Bad example
public class Bird{
    public void fly(){}
}
public class Duck extends Bird{}
The duck can fly because of it is a bird, But what about this:

public class Ostrich extends Bird{}
Ostrich is a bird, But it can't fly, Ostrich class is a subtype of class Bird, But it can't use the fly method, that means that we are breaking LSP principle.

Good example
public class Bird{
}
public class FlyingBirds extends Bird{
    public void fly(){}
}
public class Duck extends FlyingBirds{}
public class Ostrich extends Bird{} 
```

### Interface Segregation:
A client should never be forced to implement a function that it does not require. 
```
Example (Bad)
public interface Toy {
    void setPrice(double price);
    void setColor(String color);
    void move();
    void fly();
}
public class ToyHouse implements Toy {
    double price;
    String color;
    @Override
    public void setPrice(double price) {
        this.price = price;
    }
    @Override
    public void setColor(String color) {
        this.color=color;
    }
    @Override
    public void move(){}
    @Override
    public void fly(){}    
}
Following the Interface Segregation Principle

public interface Toy {
     void setPrice(double price);
     void setColor(String color);
}
public interface Movable {
    void move();
}
public interface Flyable {
    void fly();
}
package guru.springframework.blog.interfacesegregationprinciple;

public class ToyHouse implements Toy {
    double price;
    String color;

    @Override
    public void setPrice(double price) {

        this.price = price;
    }
    @Override
    public void setColor(String color) {

        this.color=color;
    }
    @Override
    public String toString(){
        return "ToyHouse: Toy house- Price: "+price+" Color: "+color;
    }
}
package guru.springframework.blog.interfacesegregationprinciple;

public class ToyCar implements Toy, Movable {
    double price;
    String color;

    @Override
    public void setPrice(double price) {

        this.price = price;
    }

    @Override
    public void setColor(String color) {
     this.color=color;
    }
    @Override
    public void move(){
        System.out.println("ToyCar: Start moving car.");
    }
    @Override
    public String toString(){
        return "ToyCar: Moveable Toy car- Price: "+price+" Color: "+color;
    }
}
package guru.springframework.blog.interfacesegregationprinciple;

public class ToyPlane implements Toy, Movable, Flyable {
    double price;
    String color;

    @Override
    public void setPrice(double price) {
        this.price = price;
    }

    @Override
    public void setColor(String color) {
        this.color=color;
    }
    @Override
    public void move(){

        System.out.println("ToyPlane: Start moving plane.");
    }
    @Override
    public void fly(){

        System.out.println("ToyPlane: Start flying plane.");
    }
    @Override
    public String toString(){
        return "ToyPlane: Moveable and flyable toy plane- Price: "+price+" Color: "+color;
    }
}
package guru.springframework.blog.interfacesegregationprinciple;

public class ToyBuilder {
    public static ToyHouse buildToyHouse(){
        ToyHouse toyHouse=new ToyHouse();
        toyHouse.setPrice(15.00);
        toyHouse.setColor("green");
        return toyHouse;
        }
    public static ToyCar buildToyCar(){
        ToyCar toyCar=new ToyCar();
        toyCar.setPrice(25.00);
        toyCar.setColor("red");
        toyCar.move();
        return toyCar;
    }
    public static ToyPlane buildToyPlane(){
        ToyPlane toyPlane=new ToyPlane();
        toyPlane.setPrice(125.00);
        toyPlane.setColor("white");
        toyPlane.move();
        toyPlane.fly();
        return toyPlane;
    }
}
```


### Dependency Inversion:

Entities must depend on abstractions instead of concretions. Instead of using direct references from a high-level module to a low-level module, use abstractions.

```
Principle violation example (bad):

public class ApplePhone {
    void acceptCall(){};
    void declineCall(){};
}
public class CarHandsFree {
    ApplePhone phone;
    void pairWithPhone(ApplePhone phone){
        this.phone = phone;
    }

    void attendCall(){
        this.phone.attendCall();    
    }
    void declineCall(){
        this.phone.declineCall();
    }
}
This does not hold good when you want to use a SamsungPhone. So all brands & models of phones that are bluetooth capable needs to confirm to a common abstraction that the hands-free can consume.

Principle adherence example (good):

public interface BluetoothCapabalePhone {
    void acceptCall();
    void declineCall();
}
public class ApplePhone implements BluetoothCapabalePhone {
    void acceptCall(){};
    void declineCall(){};
}
public class SamsungPhone implements BluetoothCapabalePhone {
    void acceptCall(){};
    void declineCall(){};
}
public class HtcPhone implements BluetoothCapabalePhone {
    void acceptCall(){};
    void declineCall(){};
}
public class CarHandsFree {
    BluetoothCapabalePhone phone;
    void pairWithPhone(BluetoothCapabalePhone phone){
        this.phone = phone;
    }
    void attendCall(){
        this.phone.attendCall();
    }
    void declineCall(){
        this.phone.declineCall();
    }
}
```



