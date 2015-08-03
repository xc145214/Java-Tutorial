# When to use private constructors in Java?

If a method is private, it means that it can not be accessed from any class other than itself. This is the access control mechanism provided by Java. When it is used appropriately, it can produce security and functionality. Constructors, like regular methods, can also be declared as private. You may wonder why we need a private constructor since it is only accessible from its own class. When a class needs to prevent the caller from creating objects. Private constructors are suitable. Objects can be constructed only internally.

One application is in the singleton design pattern. The policy is that only one object of that class is supposed to exist. So no other class than itself can access the constructor. This ensures the single instance existence of the class. Private constructors have been widely used in JDK, the following code is part of Runtime class.
```
public class Runtime {
	private static Runtime currentRuntime = new Runtime();
 
	public static Runtime getRuntime() {
		return currentRuntime;
	}
 
	// Don't let anyone else instantiate this class
	private Runtime() {
	}
}
```