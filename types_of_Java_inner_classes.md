# types of Java inner classes
There are 4 different types of inner classes you can use in Java. The following gives their name and examples.

## Static Nested Classes
```
class Outer {
	static class Inner {
		void go() {
			System.out.println("Inner class reference is: " + this);
		}
	}
}
 
public class Test {
	public static void main(String[] args) {
		Outer.Inner n = new Outer.Inner();
		n.go();
	}
}
```
```
Inner class reference is: Outer$Inner@19e7ce87
```
## Member Inner Class

Member class is instance-specific. It has access to all methods, fields, and the Outer's this reference.
```
public class Outer {
    private int x = 100;
 
    public void makeInner(){
        Inner in = new Inner();
        in.seeOuter();
    }
 
    class Inner{
        public void seeOuter(){
            System.out.println("Outer x is " + x);
            System.out.println("Inner class reference is " + this);
            System.out.println("Outer class reference is " + Outer.this);
        }
    }
 
    public static void main(String [] args){
    	Outer o = new Outer();
        Inner i = o.new Inner();
        i.seeOuter();
    }
}
```
```
Outer x is 100
Inner class reference is Outer$Inner@4dfd9726
Outer class reference is Outer@43ce67ca
```

## Method-Local Inner Classes

```
public class Outer {
	private String x = "outer";
 
	public void doStuff() {
		class MyInner {
			public void seeOuter() {
				System.out.println("x is " + x);
			}
		}
 
		MyInner i = new MyInner();
		i.seeOuter();
	}
 
	public static void main(String[] args) {
		Outer o = new Outer();
		o.doStuff();
	}
}
```
```
x is outer
```
```
public class Outer {
	private static String x = "static outer";
 
	public static void doStuff() {
		class MyInner {
			public void seeOuter() {
				System.out.println("x is " + x);
			}
		}
 
		MyInner i = new MyInner();
		i.seeOuter();
	}
 
	public static void main(String[] args) {
		Outer.doStuff();
	}
}
```
```
x is static outer
```
## Anonymous Inner Classes

This is frequently used when you add an action listener to a widget in a GUI application.
```
button.addActionListener(new ActionListener(){
     public void actionPerformed(ActionEvent e){
         comp.setText("Button has been clicked");
     }
});
```