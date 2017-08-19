---
layout: post
title: Debugging Java Programs With JDB
date: 2017-08-19
---

JDB is a simple command line Java debugger.

---

### Starting a jdb session

```java
import java.util.LinkedList;

public class example
{
  public static void main(String args[])
  {
    LinkedList<Integer> x = new LinkedList<Integer>();
    x.add(10);

    sum();
  }

  public static void sum()
  {
    int a = 2;
    int b = 3;
    System.out.println(a + b);
  }
}
```

```
user@computer$ javac example.java
user@computer$ jdb example
Initializing jdb ...
>
```

---

### Breakpoints
Lines

```
> stop at example:5
```

Methods

```
> stop in example.main
```

Displaying Breakpoints

```
> clear
Breakpoints set:
        breakpoint example:5
        breakpoint example.main
```

Deleting Breakpoints

```
> clear example:5
Removed: breakpoint example:5
```

Continue after hitting a breakpoint

```
> cont
```

Continue one line

```
> next
```

Step into function

```
> step
```

Print source code

```
> list
```

Run class

```
> run example
```

---

### Printing
```
main[1] dump a
com.sun.tools.example.debug.expr.ParseException: Name unknown: a
 a = null
```

Cannot print or dump variables if class is not compiled with -g option.

```
javac -g example.java
```

```
main[1] dump a
a = 2
```

```
main[1] print a
a = 2
```

Both print and dump can print primitive data types. Print can also evaluate expressions.

```
main[1] print 2 + 2
2 + 2 = 4
```

Locals prints all the local variables.

```
main[1] locals
Method arguments:
Local variables:
a = 2
```

Printing objects

Using dump on objects will print information about the object.
```
main[1] dump x
u = {
    size: 1
    first: instance of java.util.LinkedList$Node(id=432)
    last: instance of java.util.LinkedList$Node(id=432)
    serialVersionUID: 876323262645176354
    java.util.AbstractList.modCount: 1
    java.util.AbstractCollection.MAX_ARRAY_SIZE: 2147483639
}
```
Using print on objects will print the contents of the object.
```
main[1] print x
u = "[10]"
```
