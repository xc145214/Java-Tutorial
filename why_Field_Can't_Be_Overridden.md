# Why Field Can’t Be Overridden?

## Can Field Be Overridden in Java?

Let's first take a look at the following example which creates two Sub objects. One is assigned to a Sub reference, the other is assigned to a Super reference.
```
package oo;
 
class Super {
	String s = "Super";
}
 
class Sub extends Super {
	String s = "Sub";
}
 
public class FieldOverriding {
	public static void main(String[] args) {
		Sub c1 = new Sub();
		System.out.println(c1.s);
 
		Super c2 = new Sub();
		System.out.println(c2.s);
	}
}
```
What is the output?
```
Sub
Super
```
We did create two Sub objects, but why the second one prints out "Super"?

## Hiding Fields Instead Of Overriding Them

In [1], there is a clear definition of Hiding Fields:

>Within a class, a field that has the same name as a field in the superclass hides the superclass's field, even if their types are different. Within the subclass, the field in the superclass cannot be referenced by its simple name. Instead, the field must be accessed through super. Generally speaking, we don't recommend hiding fields as it makes code difficult to read.

From this definition, member fields can not be overridden like methods. When a subclass defines a field with the same name, the subclass just declares a new field. The field in the superclass is hidden. It is NOT overridden, so it can not be accessed polymorphically.

## Ways to Access Hidden Fields

1. By using parenting reference type, the hidden parent fields can be access, like the example above.
2. By casting you can access the hidden member in the superclass.
```
System.out.println(((Super)c1).s);
```
