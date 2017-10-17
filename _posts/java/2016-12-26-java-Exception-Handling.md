---
layout: post
title: "Exception Handling"
comments: true
categories: Java
---

## Exception Handling

Hierarchy of Java Exception classes
* Throwable
    - Exception
        - IOException
        - SQLException
        - ClassNotFoundException
        - RuntimeException
            - ArithmeticException
            - NullPointerException
            - NumberFormateException
            - IndexOutOfBoundException
                - ArrayIndexOutOfBoundException
                - StringIndexOutOfBoundException
    - Error
        - StackOverFlowError
        - VirtualMachineError
        - OutOfMemoryError
        

Type of Exception
1. Checked Exception
    -Those type of exception extends Throwable except RuntimeException & are checked at compile time. Example: IOException, SQLException
2. Unchecked Exception
    - Those type of Exception which are not checked at runtime. Example: ArithmeticException, NullPointerException, NumberFormateException 
3. Error
    - Error is irrecoverable e.g. OutOfMemoryError, VirtualMachineError, AssertionError etc.
    

Common scenarios where exceptions may occur

There are given some scenarios where unchecked exceptions can occur. They are as follows:
1) Scenario where ArithmeticException occurs

If we divide any number by zero, there occurs an ArithmeticException.

    int a=50/0;//ArithmeticException  

2) Scenario where NullPointerException occurs

If we have null value in any variable, performing any operation by the variable occurs an NullPointerException.

    String s=null;  
    System.out.println(s.length());//NullPointerException  

3) Scenario where NumberFormatException occurs

The wrong formatting of any value, may occur NumberFormatException. Suppose I have a string variable that have characters, converting this variable into digit will occur NumberFormatException.

    String s="abc";  
    int i=Integer.parseInt(s);//NumberFormatException  

4) Scenario where ArrayIndexOutOfBoundsException occurs

If you are inserting any value in the wrong index, it would result ArrayIndexOutOfBoundsException as shown below:

    int a[]=new int[5];  
    a[10]=50; //ArrayIndexOutOfBoundsException  

### Java Exception Handling Keywords

There are 5 keywords used in java exception handling.

    try
    catch
    finally
    throw
    throws

###### The JVM firstly checks whether the exception is handled or not. If exception is not handled, JVM provides a default exception handler that performs the following tasks:

* Prints out exception description.
* Prints the stack trace (Hierarchy of methods where the exception occurred).
* Causes the program to terminate.

###### But if exception is handled by the application programmer, normal flow of the application is maintained i.e. rest of the code is executed.

#### Java finally block 
* Java finally block is a block that is used to execute important code such as closing connection, stream etc. 
* Java finally block is always executed whether exception is handled or not.
* Java finally block is 

#### For each try block there can be zero or more catch blocks, but only one finally block.

## Java Exception propagation
   An exception is first thrown from the top of the stack and if it is not caught, it drops down the call stack to the previous method,If not caught there, the exception again drops down to the previous method, and so on until they are caught or until they reach the very bottom of the call stack.This is called exception propagation.
   
```
class TestExceptionPropagation1{  
         void m(){  
           int data=50/0;  
         }  
         void n(){  
           m();  
         }  
         void p(){  
          try{  
           n();  
          }catch(Exception e){System.out.println("exception handled");}  
         }  
         public static void main(String args[]){  
          TestExceptionPropagation1 obj=new TestExceptionPropagation1();  
          obj.p();  
          System.out.println("normal flow...");  
         }  
       }  
       
       Output:exception handled
              normal flow... 
```
 
#### By default Unchecked Exceptions are forwarded in calling chain (propagated).
#### By default, Checked Exceptions are not forwarded in calling chain (propagated).

Program which describes that checked exceptions are not propagated

```
    class TestExceptionPropagation2{  
      void m(){  
        throw new java.io.IOException("device error");//checked exception  
      }  
      void n(){  
        m();  
      }  
      void p(){  
       try{  
        n();  
       }catch(Exception e){System.out.println("exception handeled");}  
      }  
      public static void main(String args[]){  
       TestExceptionPropagation2 obj=new TestExceptionPropagation2();  
       obj.p();  
       System.out.println("normal flow");  
      }  
    }  
    
    Output:Compile Time Error
```

ava throws keyword

The Java throws keyword is used to declare an exception. It gives an information to the programmer that there may occur an exception so it is better for the programmer to provide the exception handling code so that normal flow can be maintained.

Exception Handling is mainly used to handle the checked exceptions. If there occurs any unchecked exception such as NullPointerException, it is programmers fault that he is not performing check up before the code being used.
Syntax of java throws

    return_type method_name() throws exception_class_name{  
    //method code  
    }  

Which exception should be declared

Ans) checked exception only, because:

    unchecked Exception: under your control so correct your code.
    error: beyond your control e.g. you are unable to do anything if there occurs VirtualMachineError or StackOverflowError.


### Difference between throw and throws in Java

| No. |	throw|	throws |
| ------ |	------|	------ |
| 1) |	Java throw keyword is used to explicitly throw an exception. |	Java throws keyword is used to declare an exception.|
| 2) |	Checked exception cannot be propagated using throw only. |	Checked exception can be propagated with throws. |
| 3) | Throw is followed by an instance. |	Throws is followed by class. |
| 4) | Throw is used within the method. | Throws is used with the method signature. |
| 5) |	You cannot throw multiple exceptions. |	You can declare multiple exceptions e.g. public void method()throws IOException,SQLException.|



Difference between final, finally and finalize

There are many differences between final, finally and finalize. A list of differences between final, finally and finalize are given below:

| No. |	final	| finally | finalize |
| ------ | ------ |	------ | ------ |
|1)|	Final is used to apply restrictions on class, method and variable.| Final class can't be inherited, final method can't be overridden and final variable value can't be changed.|	Finally is used to place important code, it will be executed whether exception is handled or not.	Finalize is used to perform clean up processing just before object is garbage collected.|
|2)	|Final is a keyword.|	Finally is a block.|	Finalize is a method.|


Java throw example

    void m(){  
    throw new ArithmeticException("sorry");  
    }  

Java throws example

    void m()throws ArithmeticException{  
    //method code  
    }  

Java throw and throws example

    void m()throws ArithmeticException{  
    throw new ArithmeticException("sorry");  
    }  
    
    
        }}  

