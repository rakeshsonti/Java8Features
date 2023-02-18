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
--------------------------------------------------------------------------------------------------------------------
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
  
 --------------------------------------------------------------------------------------------------------------------
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
[Official Oracle Site for functional Interface](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html)
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
 -----------------------------------------------Java 7 sort v Java 8 Sort------------------------------------------------------
  Sort with comparator
  ````
  package io.java8.features.typereference;

import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

/**
 * @author Rakesh Sonti 18-Feb-2023 - 2:18:07 pm
 */

public class RunnableExample {
	public static void main(String[] args) {
		List<Person> people=Arrays.asList(
				new Person("Ram","Sonti",12),
				new Person("Ranu","Sharma",34),
				new Person("Kiran","Chain",35),
				new Person("Pinku","Sutar",40),
				new Person("CRani","Stark",56)
				);
			//step - 1 sort list by last name java -7
			Collections.sort(people, new Comparator<Person>() {
				@Override
				public int compare(Person o1, Person o2) {
					return o1.getLastName().compareTo(o2.getLastName());
				}

			});
			//step 2 create a method that print all element of list java -7
			printAll(people);
			//step 3 create a method that print all people that have last name begin with c java -7
			printLastNameBeginWithC(people);
			System.out.println("--------------------------------new cond-------------");
			printLastNameBeginWithCondition(people,new Condition() {

				@Override
				public boolean test(Person p) {
					return p.getLastName().startsWith("C");
				}
				
			});
			System.out.println("--------------------------------new cond-------------");

			printLastNameBeginWithCondition(people,new Condition() {
				
				@Override
				public boolean test(Person p) {
					return p.getFirstName().startsWith("C");
				}
				
			});
		
		
	}
	private static void printLastNameBeginWithCondition(List<Person> people,Condition cd) {
		for(Person p:people) {
			if(cd.test(p))
			System.out.println(p.toString());
		}
	}
	private static void printLastNameBeginWithC(List<Person> people) {
		for(Person p:people) {
			if(p.getLastName().startsWith("C"))
				System.out.println(p.toString());
		}
	}
	private static void printAll(List<Person> people) {
		for(Person p:people) {
			System.out.println(p.toString());
		}
	}
	interface Condition{
		boolean test(Person p);
	}
	@FunctionalInterface 
	interface MyInterface{
		int getAdd(int num1,int num2);
	}
}
class Person{
	private String firstName;
	private String lastName;
	private int age;
	
	@Override
	public String toString() {
		return "Person [" + (firstName != null ? "firstName=" + firstName + ", " : "")
				+ (lastName != null ? "lastName=" + lastName + ", " : "") + "age=" + age + "]";
	}
	public Person() {
		super();
	}
	public Person(String firstName, String lastName, int age) {
		super();
		this.firstName = firstName;
		this.lastName = lastName;
		this.age = age;
	}
	public String getFirstName() {
		return firstName;
	}
	public void setFirstName(String firstName) {
		this.firstName = firstName;
	}
	public String getLastName() {
		return lastName;
	}
	public void setLastName(String lastName) {
		this.lastName = lastName;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	
}

````	
Java 8 solution with lambda expression for above code
````
package io.java8.features.typereference;

import java.util.Arrays;
import java.util.Collections;
import java.util.List;

/**
 * @author Rakesh Sonti 18-Feb-2023 - 2:18:07 pm
 */

public class RunnableExample {
	public static void main(String[] args) {
		List<Person> people=Arrays.asList(
				new Person("Ram","Sonti",12),
				new Person("Ranu","Sharma",34),
				new Person("Kiran","Chain",35),
				new Person("Pinku","Sutar",40),
				new Person("CRani","Stark",56)
				);
			//step - 1 sort list by last name java -8 use lambda class instead of inner anonymous class
			Collections.sort(people, (o1,o2)->o1.getLastName().compareTo(o2.getLastName()));
			//step 2 create a method that print all element of list java -
			printAllConditionaly(people,p->true);
			//step 3 create a method that print all people that have last name begin with c java -7
			System.out.println("--------------------------------new cond-------------");
			printAllConditionaly(people,p->p.getLastName().startsWith("C"));
			System.out.println("--------------------------------new cond-------------");

			printAllConditionaly(people,p->p.getFirstName().startsWith("C"));
		
		
	}
	private static void printAllConditionaly(List<Person> people,Condition cd) {
		for(Person p:people) {
			if(cd.test(p))
			System.out.println(p.toString());
		}
	}


	interface Condition{
		boolean test(Person p);
	}
	
}
class Person{
	private String firstName;
	private String lastName;
	private int age;
	
	@Override
	public String toString() {
		return "Person [" + (firstName != null ? "firstName=" + firstName + ", " : "")
				+ (lastName != null ? "lastName=" + lastName + ", " : "") + "age=" + age + "]";
	}
	public Person() {
		super();
	}
	public Person(String firstName, String lastName, int age) {
		super();
		this.firstName = firstName;
		this.lastName = lastName;
		this.age = age;
	}
	public String getFirstName() {
		return firstName;
	}
	public void setFirstName(String firstName) {
		this.firstName = firstName;
	}
	public String getLastName() {
		return lastName;
	}
	public void setLastName(String lastName) {
		this.lastName = lastName;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	
}
````
	Any way we need to declare an interface which contains right method for our need
	 Java.util.function has lots of predifined interfaces
````	
	Instead of COndition we can use Predicate which have test method
	//Predicate is generic interface whose contains test method and generic type
	private static void printAllConditionaly(List<Person> people,Predicate<Person> cd) {
		for(Person p:people) {
			if(cd.test(p))
			System.out.println(p.toString());
		}
	}
	Every time we need a abstract method in functional interface so that the method which we defined using anonymous class, can be used with that interface.
	why we are using test which return boolena?
	ans is pretty much simple printAllConditionaly method second argument is an function which return boolean based on condition so test is fit with all the method passed as an second arguments.We are calling that method later on inside the method.
	
````
	
--------------------------------------------------------------------------------------------
 Println using Consumer Functional interface
````
	package io.java8.features.typereference;

import java.util.Arrays;
import java.util.Collections;
import java.util.List;
import java.util.function.Consumer;
import java.util.function.Predicate;

/**
 * @author Rakesh Sonti 18-Feb-2023 - 2:18:07 pm
 */

public class RunnableExample {
	public static void main(String[] args) {
		List<Person> people = Arrays.asList(new Person("Ram", "Sonti", 12), new Person("Ranu", "Sharma", 34),
				new Person("Kiran", "Chain", 35), new Person("Pinku", "Sutar", 40), new Person("CRani", "Stark", 56));

		// step - 1 sort list by last name use lambda class instead of inner anonymous
		// class
		Collections.sort(people, (o1, o2) -> o1.getLastName().compareTo(o2.getLastName()));

		// step 2 create a method that print all element of list java -
		performAllConditionaly(people, p -> true, p -> System.out.println(p));
		System.out.println("--------------------------------new cond-------------");

		// step 3 create a method that print all people that have last name begin with c
		performAllConditionaly(people, p -> p.getLastName().startsWith("C"), p -> System.out.println(p.getFirstName()));
		System.out.println("--------------------------------new cond-------------");
		performAllConditionaly(people, p -> p.getFirstName().startsWith("C"), p -> System.out.println(p.getLastName()));

	}

	// Consumer is generic interface whose contains accept method whose return
	// nothing just accept the argumant
	private static void performAllConditionaly(List<Person> people, Predicate<Person> pd, Consumer<Person> consumer) {
		for (Person p : people) {
			if (pd.test(p))
				consumer.accept(p);
		}
	}
}

class Person {
	private String firstName;
	private String lastName;
	private int age;

	@Override
	public String toString() {
		return "Person [" + (firstName != null ? "firstName=" + firstName + ", " : "")
				+ (lastName != null ? "lastName=" + lastName + ", " : "") + "age=" + age + "]";
	}

	public Person() {
		super();
	}

	public Person(String firstName, String lastName, int age) {
		super();
		this.firstName = firstName;
		this.lastName = lastName;
		this.age = age;
	}

	public String getFirstName() {
		return firstName;
	}

	public void setFirstName(String firstName) {
		this.firstName = firstName;
	}

	public String getLastName() {
		return lastName;
	}

	public void setLastName(String lastName) {
		this.lastName = lastName;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

}

````
	
----------------------------------------------------------------------------------------------------------------------	
  Exception handling in Lambda Exression
````
	package io.java8.features.exception;

import java.util.function.BiConsumer;

/**
 * @author Rakesh Sonti 18-Feb-2023 - 8:05:20 pm
 */
public class ExceptionHandling {

	/**
	 *
	 */
	public static void main(String[] args) {
		int arr[] = { 1, 2, 3, 4, 5, 6 };
		int key = 0;
		process(arr, key, wrapperLambda((val, keyy) -> System.out.println(val / keyy)));

		// process(arr, key, (val, keyy) ->System.out.println(val / keyy));
		/*
		 * process(arr, key, (val, keyy) -> { try { System.out.println(val / keyy); }
		 * catch (Exception ex) { System.out.println(ex.getMessage()); } });
		 */
	}

	private static BiConsumer<Integer, Integer> wrapperLambda(BiConsumer<Integer, Integer> consumer) {
		return (val1, key1) -> {
			try {
				consumer.accept(val1, key1);
			} catch (Exception ex) {
				System.out.println(ex.getLocalizedMessage());
			}
		};
	}

	private static void process(int[] arr, int key, BiConsumer<Integer, Integer> consumer) {
		for (int i : arr) {
//			try {
			consumer.accept(i, key);

			/*
			 * }catch(Exception ex) { //handle exception
			 * System.out.println(ex.getMessage()); }
			 */
		}
	}

}


````
--------------------------------------------------------------------------------------------------------------------------
  Closure
````
package io.java8.features.closure;

/**
 * @author Rakesh Sonti 18-Feb-2023 - 8:31:54 pm
 */
public class ClosureExample {
	public static void main(String[] args) {
		int a=10,b=20;
		//closure exists here
		doProcess(a,i->System.out.println(i+b));
		//we are using here but this method executing in doProcess but it still remember the value of b, this is called closure in functional programming
		/*
		doProcess(a,new Process() {

			@Override
			public void process(int i) {
				System.out.println(i+b);
			}
			
		});
		*/
	}
	public static void doProcess(int i,Process p) {
		p.process(i);
	}
}

interface Process {
	void process(int i);
}

````
---------------------------------------------------------------------------------------------------------------------------
	
This
````
	package io.java8.features.closure;

/**
 * @author Rakesh Sonti 18-Feb-2023 - 8:31:54 pm
 */
public class ThisReferenceExample {
	//In case of anonymous inner class this value changed but in case of lambda doesn't
	public void exdcuteMethod() {
		doProcess(10, i->{
			System.out.println("Value of i is: "+i);
			System.out.println(this);//this will work and pointing to the ThisReferenceExample class
		}) ;
	}
	public static void main(String[] args) {
		ThisReferenceExample thisRef=new ThisReferenceExample();
		thisRef.exdcuteMethod();
		thisRef.doProcess(10, i->{
			System.out.println("Value of i is: "+i);
//			System.out.println(this);//showing error || Lambda does not touch this refrence
		}) ;
		/*
		thisRef.doProcess(10, new Process() {

			@Override
			public void process(int i) {
				System.out.println("Value of i is: "+i);
				System.out.println(this);
				//this belong to the inner anonymous class
			}
			public String toString() {
				return "This is my to string methos";
			}
			
		});
		*/
		
	}
	public void doProcess(int i,Process p) {
		p.process(i);
	}
	public String toString() {
		return "This is my to string method for outer";
	}
}


  interface Process { void process(int i); }
 


````	
---------------------------------------------------------------------------------------------------------------------	
Method References
``
	package io.java8.features.MethodRefences;

/**
 * @author Rakesh Sonti 18-Feb-2023 - 10:59:53 pm
 */
public class MethodRefrence {

	public static void main(String[] args) {
//		Thread th=new Thread(()->printMessage()); //lambda way
		Thread th=new Thread(MethodRefrence::printMessage);
		th.start();
	}
	public static void printMessage() {
		System.out.println("Hello");
		
	}

}


``	
---------------------------------------------------------------------------------------------------------------------	
	// step 2 create a method that print all element of list java - Method refrence
		performAllConditionaly(people, p -> true, System.out::println);
---------------------------------------------------------------------------------------------------------------------	

	
	
	
