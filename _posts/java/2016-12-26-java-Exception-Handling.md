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
