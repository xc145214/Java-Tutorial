# Why String is immutable in Java ?
`String` is an immutable class in Java. An immutable class is simply a class whose instances cannot be modified. All information in an instance is initialized when the instance is created and the information can not be modified. There are many advantages of immutable classes. This article summarizes why String is designed to be immutable. A good answer depends on deep understanding of memory, synchronization, data structures, etc.

##  Requirement of String Pool
String pool (String intern pool) is a special storage area in Method Area. When a string is created and if the string already exists in the pool, the reference of the existing string will be returned, instead of creating a new object and returning its reference.

The following code will create only one string object in the heap.
```
String string1 = "abcd";
String string2 = "abcd";
```
Here is how it looks:
![string-immutable-1](images/java-string-pool.jpeg)

If string is not immutable, changing the string with one reference will lead to the wrong value for the other references.

##  Caching Hashcode
The hashcode of string is frequently used in Java. For example, in a HashMap. Being immutable guarantees that hashcode will always the same, so that it can be cashed without worrying the changes.That means, there is no need to calculate hashcode every time it is used. This is more efficient.

In String class, it has the following code:
```
private int hash;//this is used to cache hash code.
```

##  Facilitating the Use of Other Objects

To make this concrete, consider the following program:
```
HashSet<String> set = new HashSet<String>();
set.add(new String("a"));
set.add(new String("b"));
set.add(new String("c"));
 
for(String a: set)
	a.value = "a";
```
In this example, if `String` is mutable, it's value can be changed which would violate the design of set (set contains unduplicated elements). This example is designed for simplicity sake, in the real `String` class there is no `value` field.
## Security

String is widely used as parameter for many java classes, e.g. network connection, opening files, etc. Were String not immutable, a connection or file would be changed and lead to serious security threat. The method thought it was connecting to one machine, but was not. Mutable strings could cause security problem in Reflection too, as the parameters are strings.

Here is a code example:
```
boolean connect(string s){
    if (!isSecure(s)) { 
throw new SecurityException(); 
}
    //here will cause problem, if s is changed before this by using other references.    
    causeProblem(s);
}
```
## Immutable objects are naturally thread-safe

Because immutable objects can not be changed, they can be shared among multiple threads freely. This eliminate the requirements of doing synchronization.

In summary, String is designed to be immutable for the sake of efficiency and security. This is also the reason why immutable classes are preferred in general.