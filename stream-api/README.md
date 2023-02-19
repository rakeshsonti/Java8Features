### Java Stream API
* Java don't allow multiple inheritance
* In java 1.8 java thinker need to add new methods in exiting collection interface, So intead of declaring the method they introduced default methods. If they declare the method , it will break the exiting API flow.
* In java 1.8 we have abstract method and we can declare the method of the method but need to add **default** keyword front of that method
* As we know one class can implement multiple interfaces. If both the interface defined the same default method then class need to defined the method
* class method has more priority than method of interface
* class A implement X has show(); X has show() method and B class extends A now if B call show() method . It will be called from A not X
* if A class don't have show then it will call interface method A

-----------------------------------------------------------------------------------------------------------------------

````
package com.stream.api;

/**
 * @author Rakesh Sonti 19-Feb-2023 - 3:21:44 pm
 */
public class CollectionsAPI extends Vehicle {

//help to achieved concurrency
	public static void main(String[] args) {
		CollectionsAPI obj = new CollectionsAPI();
		obj.show();
	}

}

class Vehicle implements Tire {
	public void show() {
		System.out.println("vehicle show..");
	}
}

interface Tire {
	default void show() {
		System.out.println("Tire show..");
	};
}

**Output**:
vehicle show..

````
------------------------------------------------------------------------------------------------------------------------
> We can't override the method in interface which is available in **Object class**
````
interface Tire {
	//showing error
	default boolean equals(Object obj)
		return false;
		
	}
	default void show() {
		System.out.println("Tire show..");
	};
}
````
------------------------------------------------------------------------------------------------------------------------
Java 8 We can defined static methods in Interface

````
interface Tire {

	static void showName() {
		System.out.println("Tire showName..");
	}

}
````
------------------------------------------------------------------------------------------------------------------------



