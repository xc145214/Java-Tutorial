# What is Instance Initializer in Java?
In this post, I will first use an example to show what are instance variable initializer, instance initializer and static initializer and then illustrate how the instance initializer works in Java.

## Execution Order

Look at the following class, do you know which one gets executed first?
```
public class Foo {
 
	//instance variable initializer
	String s = "abc";
 
	//constructor
	public Foo() {
		System.out.println("constructor called");
	}
 
	//static initializer
	static {
		System.out.println("static initializer called");
	}
 
	//instance initializer
	{
		System.out.println("instance initializer called");
	}
 
	public static void main(String[] args) {
		new Foo();
		new Foo();
	}
}
```
Output:
```
static initializer called
instance initializer called
constructor called
instance initializer called
constructor called
```

## How does Java instance initializer work?

The instance initializer above contains a println statement. To understand how it works, we can treat it as a variable assignment statement, e.g., b = 0. This can make it more obvious to understand.

Instead of
```
int b = 0
```
, you could write
```
int b;
b = 0;
```
Therefore, instance initializers and instance variable initializers are pretty much the same.

## When are instance initializers useful?

The use of instance initializers are rare, but still it can be a useful alternative to instance variable initializers if:

1. initializer code must handle exceptions
2. perform calculations that can't be expressed with an instance variable initializer.

Of course, such code could be written in constructors. But if a class had multiple constructors, you would have to repeat the code in each constructor.

With an instance initializer, you can just write the code once, and it will be executed no matter what constructor is used to create the object. (I guess this is just a concept, and it is not used often.)

Another case in which instance initializers are useful is anonymous inner classes, which can't declare any constructors at all. (Will this be a good place to place a logging function?)

Thanks to Derhein.

>Also note that Anonymous classes that implement interfaces [1] have no constructors. Therefore instance initializers are neede to execute any kinds of expressions at construction time.