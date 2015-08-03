# Java Enum Examples
An enum in Java is just like any other class, with a predefined set of instances. Here are several examples to highlight how to use Java Enum.

## Simple Example
```
public enum Color {
    RED, YELLOW, BLUE; //each is an instance of Color 
}
public class Test {
	public static void main(String[] args) {
		for(Color color: Color.values()){
			System.out.println(color);
		}
	}
}
```
Output:
```
RED
YELLOW
BLUE
```
## With Constructor
```
public enum Color {
    RED(1), YELLOW(2), BLUE(3); //each is an instance of Color 
 
    private int value;
 
    private Color(){}
 
    private Color(int i){
    	this.value = i;
    }
 
    //define instance method
    public void printValue(){
    	System.out.println(this.value);
    }
}
public class Test {
	public static void main(String[] args) {
		for(Color color: Color.values()){
			color.printValue();
		}
	}
}
```
```
1
2
3
```
## When to Use Java Enum?

Recall the definition of Java Enum which is like any other class, with a predefined set of instances.

A good use case is preventing the possibility of an invalid parameter. For example, imagine the following method:
```
public void doSomethingWithColor(int color);
```
This is ambiguous, and other developers have no idea how value to use. If you have an enum Color with BLACK, RED, etc. the signature becomes:
```
public void doSomethingWithColor(Color color);
```
Code calling this method will be far more readable, and can't provide invalid data.
