---
layout: post
title: "Difference"
comments: true
categories: Java
---

## Difference
### equals vs '=='

In General We use == operator for reference or memory location comparision 
whereas .equals() method for content comparision.

Example: 
```
String s1 = new String("rakib");
String s2 = new String("rakib");
System.out.println(s1==s2);         // false
System.out.println(s1.equals(s2));  // true
```


1.  .euals() method present in object class also meant for reference comparision only based on our requirement we can override for content comparision.
2. In String class, all wrapper class and all collection classes .equals() method is overriden for content comparision.

