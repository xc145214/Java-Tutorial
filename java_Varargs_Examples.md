# Java Varargs Examples

## What is Varargs in Java?
Varargs (variable arguments) is a feature introduced in Java 1.5. It allows a method take an arbitrary number of values as arguments.
```
public static void main(String[] args) {
	print("a");
	print("a", "b");
	print("a", "b", "c");
}
 
public static void print(String ... s){
	for(String a: s)
		System.out.println(a);
}
```
## How Varargs Work?

When varargs facility is used, it actually first creates an array whose size is the number of arguments passed at the call site, then puts the argument values into the array, and finally passes the array to the method.

## When to Use Varargs?

As its definition indicates, varargs is useful when a method needs to deal with an arbitrary number of objects. One good example from Java SDK is `String.format(String format, Object... args)`. The string can format any number of parameters, so varargs is used.

String.format("An integer: %d", i);
String.format("An integer: %d and a string: %s", i, s);