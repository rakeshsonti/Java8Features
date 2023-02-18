### Java 8 provides following features for Java Programming:

  1. Lambda expressions,
  2. Method references,
  3. Functional interfaces,
  4. Stream API,
  5. Default methods,
  6. Base64 Encode Decode,
  7. Static methods in interface,
  8. Optional class,
  9. Collectors class,
  10. ForEach() method,
  11. Nashorn JavaScript Engine,
  12. Parallel Array Sorting,
  13. Type and Repating Annotations,
  14. IO Enhancements,
  15. Concurrency Enhancements,
  16. JDBC Enhancements etc.
  
  ------------------------------------------------------------------------------------------------------------------
 why lambda
enable functional programming
readable and concise code
eliminate boiler plate code
easier to use API and libraies
enable support for parallel processing

OOP
everything is OBject
all code associated with classes and object

//for single lambda expression no need to write the return keywpord
 
---------------------------------------------------------------------------------------------------------
  **Lambda expressions: :raised_eyebrow: **- 
  ````
  package io.java8.features.lambda;

/**
 * @author Rakesh Sonti 18-Feb-2023 - 12:38:14 pm
 */
public class Lambda {

	public static void main(String[] args) {
//		lambda
		//MyInterface hl=()->System.out.println("Hello Greeting!");
		//hl.getHello();
		
		//anonymous class way
		MyInterface hl1=new MyInterface() {
			@Override
			public void getHello() {
				System.out.print("Some hello World!");
			}
		};
		hl1.getHello();
		
	}

}
interface MyInterface{
	void getHello();

}
````
--------------------------------------------------
 ````
 package io.java8.features.typereference;

/**
 * @author Rakesh Sonti 18-Feb-2023 - 2:18:07 pm
 */
public class TypeReference {

	public static void main(String[] args) {
//		StringLengthLambda mylambda=(String s)->s.length();
//		StringLengthLambda mylambda=(s)->s.length();
		StringLengthLambda mylambda=s->s.length();
		System.out.println(mylambda.getLength("Ram"));
	}
	
	interface StringLengthLambda{
		int getLength(String s);
	}

}

 ````
  
 ----------------------------------------------------------------------------------------------
 ````
  package io.java8.features.typereference;

/**
 * @author Rakesh Sonti 18-Feb-2023 - 2:18:07 pm
 */
public class RunnableExample {
	public static void main(String[] args) {
		//anonymous inner class example without lambda
	Thread mythread=new Thread(new Runnable() {
		
		@Override
		public void run() {
			System.out.println("Run method invoked....");
		}
	});
	mythread.run();
	//implement thread using lambda expression || java Old code still work if we are using interface instead of Function type
	//This called functional interfaces
	Thread mythread2=new Thread(()->System.out.println("Run method invoked1...."));
	mythread2.run();
}
}
````
-----------------------------------------------------------------------------------------

Functional Interface
````
  package io.java8.features.typereference;

/**
 * @author Rakesh Sonti 18-Feb-2023 - 2:18:07 pm
 */
public class RunnableExample {
	public static void main(String[] args) {
		// Functional Interface :- there should be at most one abstract method
		// Use @FunctionalInterface to restrict user to create more than one abstract method
		MyInterface obj=(a,b)->a+b;
		System.out.println(obj.getAdd(23, 34));
		
	}
	@FunctionalInterface
	interface MyInterface{
		int getAdd(int num1,int num2);
//		int getLength();
	}
}
````
 -----------------------------------------------------------------------------------------------------
  
  
  
  
