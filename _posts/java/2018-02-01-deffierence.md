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

StringBuffer sf1 = new StringBuffer("rakib");
StringBuffer sf2 = new StringBuffer("rakib");
System.out.println(sf1 == sf2);     // false
System.out.println(s1 == sf2);     // CE: incomparable types: java.lang.String and java.lang.StringBuffer
System.out.println(s1.equals(sf2));     // false

```


1.  .euals() method present in object class also meant for reference comparision only based on our requirement we can override for content comparision.
2. In String class, all wrapper class and all collection classes .equals() method is overriden for content comparision.
3. If r1 == r2 is true then r1.equals(r2) is always true.
4. If two objects are not equal by == operator then we can't conclude anything about .equals method. It may return true or false. 
    ie. if r1 == r2 is false then r1.equals(r2) may return true or false
5. If r1.equals(r2) is true then r1 == r2 may true or false
6. if r1.equals(r2) is false then r1 == r2 is always
7. Either parent to child or Child to parent are same type 
8. r == null && r.equals(null) return false

### Difference between adding WrappedString and String into HashSet

```
public class WrappedString {
private String s;
 public WrappedString(String s) { this.s = s; }
 public static void main(String[] args) {
 HashSet<Object> hs = new HashSet<Object>();
 WrappedString ws1 = new WrappedString("aardvark");
 WrappedString ws2 = new WrappedString("aardvark");
 hs.add(ws1); hs.add(ws2);
 System.out.println(hs.size()); // outputs 2

   }

}
```

And 

```
public class WrappedString {
private String s;
 public WrappedString(String s) { this.s = s; }
 public static void main(String[] args) {
 HashSet<Object> hs = new HashSet<Object>();
 String s1 = new String("aardvark");
 String s2 = new String("aardvark");
 hs.add(s1); hs.add(s2);
 System.out.println(hs.size()); // outputs 1
   }

}
```

The main difference is that String implements equals whereas your WrappedString does not. So from a HashSet perspective, you can add as many new String("aardvark") as you want, they will all be considered the same (because new String("aardvark").equals(new String("aardvark")) is true) and only one will be added.

Whereas two different WrappedString instances will not be equal, even if the strings they contain are equal (because new WrappedString("aardvark").equals(new WrappedString("aardvark")) is false), so the set will not consider them as duplicates.

If you want a behaviour similar to String, you need to implement equals and hashcode in your WrappedString class




