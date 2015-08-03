# How to Check if an Array Contains a Value in Java Efficiently?

How to check if an array (unsorted) contains a certain value? This is a very useful and frequently used operation in Java. It is also a top voted question on Stack Overflow. As shown in top voted answers, this can be done in several different ways, but the time complexity could be very different. In the following I will show the time cost of each method.

## Four Different Ways to Check If an Array Contains a Value
1) Using `List`:
```
public static boolean useList(String[] arr,String targetValue){
    return Arrays.asList(arr).contains(targetValue);
}
```
2) Using Set:
```
public static boolean useSet(String[] arr, String targetValue) {
	Set<String> set = new HashSet<String>(Arrays.asList(arr));
	return set.contains(targetValue);
}
```
3) Using a simple loop:
```
public static boolean useLoop(String[] arr, String targetValue) {
	for(String s: arr){
		if(s.equals(targetValue))
			return true;
	}
	return false;
}
```
4) Using Arrays.binarySearch():
* The code below is wrong, it is listed here for completeness. binarySearch() can ONLY be used on sorted arrays. You will see the result is weird when running the code below.

```
public static boolean useArraysBinarySearch(String[] arr, String targetValue) {	
	int a =  Arrays.binarySearch(arr, targetValue);
	if(a > 0)
		return true;
	else
		return false;
}
```

## Time Complexity

The approximate time cost can be measured by using the following code. The basic idea is to search an array of size 5, 1k, 10k. The approach may not be precise, but the idea is clear and simple.
```
public static void main(String[] args) {
	String[] arr = new String[] {  "CD",  "BC", "EF", "DE", "AB"};
 
	//use list
	long startTime = System.nanoTime();
	for (int i = 0; i < 100000; i++) {
		useList(arr, "A");
	}
	long endTime = System.nanoTime();
	long duration = endTime - startTime;
	System.out.println("useList:  " + duration / 1000000);
 
	//use set
	startTime = System.nanoTime();
	for (int i = 0; i < 100000; i++) {
		useSet(arr, "A");
	}
	endTime = System.nanoTime();
	duration = endTime - startTime;
	System.out.println("useSet:  " + duration / 1000000);
 
	//use loop
	startTime = System.nanoTime();
	for (int i = 0; i < 100000; i++) {
		useLoop(arr, "A");
	}
	endTime = System.nanoTime();
	duration = endTime - startTime;
	System.out.println("useLoop:  " + duration / 1000000);
 
	//use Arrays.binarySearch()
	startTime = System.nanoTime();
	for (int i = 0; i < 100000; i++) {
		useArraysBinarySearch(arr, "A");
	}
	endTime = System.nanoTime();
	duration = endTime - startTime;
	System.out.println("useArrayBinary:  " + duration / 1000000);
}
```
Result:
```
useList:  13
useSet:  72
useLoop:  5
useArraysBinarySearch:  9
```
Use a larger array (1k):
```
String[] arr = new String[1000];
 
Random s = new Random();
for(int i=0; i< 1000; i++){
	arr[i] = String.valueOf(s.nextInt());
}
```
Result:
```
useList:  112
useSet:  2055
useLoop:  99
useArrayBinary:  12
```
Use a larger array (10k):
```
String[] arr = new String[10000];
 
Random s = new Random();
for(int i=0; i< 10000; i++){
	arr[i] = String.valueOf(s.nextInt());
}
```
Result:
```
useList:  1590
useSet:  23819
useLoop:  1526
useArrayBinary:  12
```
Clearly, using a simple loop method is more efficient than using any collection. A lot of developers use the first method, but it is inefficient. **Pushing the array to another collection requires spin through all elements to read them in before doing anything with the collection type.**

The array must be sorted, if Arrays.binarySearch() method is used. In this case, the array is not sorted, therefore, it should not be used.

**Actually, if you really need to check if a value is contained in some array/collection efficiently, a sorted list or tree can do it in O(log(n)) or hashset can do it in O(1)**.