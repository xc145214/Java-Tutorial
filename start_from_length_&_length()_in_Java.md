#  Start from length & length() in Java
First of all, can you quickly answer the following question?

>Without code autocompletion of any IDE, how to get the length of an array? And how to get the length of a String?

I asked this question to developers of different levels: entry and intermediate. They can not answer the question correctly or confidently. While IDE provides convenient code autocompletion, it also brings the problem of "surface understanding". In this post, I will explain some key concepts about Java arrays.

The answer:
```
int[] arr = new int[3];
System.out.println(arr.length);//length for array
 
String str = "abc";
System.out.println(str.length());//length() for string
```
The question is why array has the length field but string does not? Or why string has the length() method while array does not?

##  Why arrays have length property?

First of all, an array is a container object that holds a fixed number of values of a single type. After an array is created, its length never changes[1]. The array's length is available as a final instance variable length. Therefore, length can be considered as a defining attribute of an array.

An array can be created by two methods: 1) an array creation expression and 2) an array initializer. When it is created, the size is specified.

An array creation expression is used in the example above. It specifies the element type, the number of levels of nested arrays, and the length of the array for at least one of the levels of nesting.

This declaration is also legal, since it specifies one of the levels of nesting.
```
int[][] arr = new int[3][];
```
An array initializer creates an array and provides initial values for all its components. It is written as a comma-separated list of expressions, enclosed by braces { and }.

For example,
```
int[] arr = {1,2,3};
```
##  Why there is not a class "Array" defined similarly like "String"?
Since an array is an object, the following code is legal.
```
Object obj = new int[10];
```
An array contains all the members inherited from class Object(except clone). Why there is not a class definition of an array? We can not find an Array.java file. A rough explanation is that they're hidden from us. You can think about the question - if there IS a class Array, what would it look like? It would still need an array to hold the array data, right? Therefore, it is not a good idea to define such a class.

Actually we can get the class of an array by using the following code:
```
int[] arr = new int[3];
System.out.println(arr.getClass());
```
Output:
```
class [I
```
"class [I" stands for the run-time type signature for the class object "array with component type int".

##  Why String has length() method?

The backup data structure of a String is a char array. There is no need to define a field that is not necessary for every application. Unlike C, an Array of characters is not a String in Java.