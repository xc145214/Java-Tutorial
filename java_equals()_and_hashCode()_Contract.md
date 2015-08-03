# Java equals() and hashCode() Contract
![hashcode-1](images/java-hashcode-650x369.jpeg)

The Java super class java.lang.Object has two very important methods defined:
```
public boolean equals(Object obj)
public int hashCode()
```
They have been proved to be extremely important to understand, especially when user-defined objects are added to Maps. However, even advanced-level developers sometimes can't figure out how they should be used properly. In this post, I will first show an example of a common mistake, and then explain how equals() and hashCode contract works.

## A common mistake

Common mistake is shown in the example below.
```
import java.util.HashMap;
 
public class Apple {
	private String color;
 
	public Apple(String color) {
		this.color = color;
	}
 
	public boolean equals(Object obj) {
		if (!(obj instanceof Apple))
			return false;	
		if (obj == this)
			return true;
		return this.color.equals(((Apple) obj).color);
	}
 
	public static void main(String[] args) {
		Apple a1 = new Apple("green");
		Apple a2 = new Apple("red");
 
		//hashMap stores apple type and its quantity
		HashMap<Apple, Integer> m = new HashMap<Apple, Integer>();
		m.put(a1, 10);
		m.put(a2, 20);
		System.out.println(m.get(new Apple("green")));
	}
}
```
In this example, a green apple object is stored successfully in a hashMap, but when the map is asked to retrieve this object, the apple object is not found. The program above prints null. However, we can be sure that the object is stored in the hashMap by inspecting in the debugger:

![hashcode-2](images/hashCode-and-equals-contract-600x268.png)

## Problem caused by hashCode()

The problem is caused by the un-overridden method "hashCode()". The contract between equals() and hasCode() is that:
1. If two objects are equal, then they must have the same hash code.
2. If two objects have the same hashcode, they may or may not be equal.

The idea behind a Map is to be able to find an object faster than a linear search. Using hashed keys to locate objects is a two-step process. Internally the Map stores objects as an array of arrays. The index for the first array is the hashcode() value of the key. This locates the second array which is searched linearly by using equals() to determine if the object is found.

The default implementation of hashCode() in Object class returns distinct integers for different objects. Therefore, in the example above, different objects(even with same type) have different hashCode.

Hash Code is like a sequence of garages for storage, different stuff can be stored in different garages. It is more efficient if you organize stuff to different place instead of the same garage. So it's a good practice to equally distribute the hashCode value. (Not the main point here though)

The solution is to add hashCode method to the class. Here I just use the color string's length for demonstration.
```
public int hashCode(){
	return this.color.length();	
}
```