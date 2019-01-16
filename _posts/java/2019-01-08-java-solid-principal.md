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
Principle violation example (bad):

public abstract class Employee {
    private int id;
    private String fname, lname, title;
    private Date dob, dateOfJoining;
    //Getters & setters
    ...
    abstract void sendCommunication();
}
public class TechnicalStaff extends Employee {
    void maintainSystems(){}
    void sendCommunication(){} //this is a problem
}
public class Accountant extends Employee {
    void maintainAccounts(){}
    void sendCommunication(){} //this is a problem
}
public class Manager extends Employee {
    void performAppraisalOfDirectReport(Employee employee){}
    void promoteDirectReport(Employee employee){}
    void sendCommunication(){} //action allowed
}
public class Director extends Employee {
    void performAppraisalOfDirectReport(Employee employee){}
    void promoteDirectReport(Employee employee){}
    void sendCommunication(){} //action allowed
}
Principle adherence example (good):

public abstract class Employee {
    private int id;
    private String fname, lname, title;
    private Date dob, dateOfJoining;
    //Getters & setters
    ...
}

public abstract class ManagementStaff extends Employee {
    void performAppraisalOfDirectReport(Employee employee){}
    void promoteDirectReport(Employee employee){}    
    abstract void sendCommunication();
}

public class TechnicalStaff extends Employee {
    void maintainSystems(){}
}

public class Accountant extends Employee {
    void maintainAccounts(){}
}

public class Manager extends ManagementStaff {
    void sendCommunication(){} //action allowed
}

public class Director extends ManagementStaff {
    void sendCommunication(){} //action allowed
}
```

### Interface Segregation:
A client should never be forced to implement a function that it does not require. Instead of having bloated interfaces, segregate them based on roles.

```
Principle violation example (bad):

public interface Enemy {
    void setDamageStrength();
    void setResilience();
    void inflictDamage();
    void walk();
    void fly();
    void teleport();
}
public class EnemyGuard implements Enemy {
    void walk(){
        //some logic 
}
    
    void inflictDamage(){
        //some logic
    }

    void fly(){} //empty implementation
    void teleport(){} //empty implementation
}
public class EnemyBird implements Enemy {
    void inflictDamage(){
        //damage logic
   
    }
    void fly(){
        //some logic
    }
    void walk(){} // empty implementation
    void teleport(){} // empty implementation
}
public class EnemyWitch implements Enemy {
    void inflictDamage(){
        //damage logic 
   
    }
    void teleport(){
        //lets assume our enemy witch can teleport
    }
    void walk(){} // empty implementation
    void fly(){} // empty implementation
}
You can see that we have 3 concrete classes that do not need certain behaviors to be implemented, were forced to do it anyway. This should never happen and the Interface Segregation principle describes how you can clean this up.

Principle adherence example (good):

public interface Enemy {
    void setDamageStrength();
    void setResilience();
    void inflictDamage();
}
public interface Walkable {
    void walk();
}
public interface Flyable {
    void fly();
}
public interface Teleportable {
    void teleport();
}

public class EnemyGuard implements Enemy, Walkable {
    void walk(){
        //some logic
    }
    
    void inflictDamage(){
        //some logic
    }
}
public class EnemyBird implements Enemy, Flyable {
    void fly(){
        //some logic
    }
    void inflictDamage(){
        //damage logic   
   
    }
}
public class EnemyWitch implements Enemy, Teleportable {
    void teleport(){
        //lets assume our enemy witch can teleport
    }
    void inflictDamage() {
        //damage logic
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



