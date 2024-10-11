# Functional Programming in Java

### Anonymous Class
Before starting functional programming in java it better to know about anonymous class.
Consider the below class `Car`. Lets say you want to extend this and override the method drive with another class `Benz`.

```java
class Car {
	public void drive() {
		System.out.println("Driving from Car");
	}
}

class Benz extends Car {
	@Override
	public void drive() {
		System.out.println("Driving from Benz");
	}
}

class Main {
	public static void main(String[] args) {
		Car car = new Benz();
		car.drive(); // Driving from Benz
	}
}
```

- So you have overridden and provided another implementation and created an instance.
- Now `car.drive();` will print `Driving from Benz`.
- Here the whole purpose the `Benz` class is just to override the `drive` method from the `Car` class.
- What if you can override this without creating a separate class if you are sure that the overridden method is just for that object (used only once).
- This is where anonymous class comes into picture.

```java
class Car {
	public void drive() {
		System.out.println("Driving from Car");
	}
}

class Main {
	public static void main(String[] args) {
		Car car = new Car(){
			@Override
			public void drive() {
				System.out.println("Driving from Main");
			}
		};
        
        car.drive(); // Driving from Main
    }
}
```

- Here the anonymous implementation starts from the curly braces after `new Car()`
- Now `car.drive();` will print `Driving from Main`.

### Anonymous Class with Abstraction

- Hope you know about the concept of abstraction. Here let me demonstrate how we can use anonymous class to provide implementation to an abstract class.

> [!Note]
> Abstract class cannot be instantiated by default.

- Go through the below code its the same as above anonymous class with abstraction

```java
abstract class Car {
	public abstract void drive();
	
	public abstract int topSpeed();
	
	public void playRadio() {
		System.out.println("Vibe mode on.");
	}
}

class Main {
	public static void main(String[] args) {
		Car car = new Car(){
			@Override
			public void drive() {
				System.out.println("Driving from Main");
			}
			
			@Override
			public int topSpeed() {
				return 180;
			}
		};
		
		car.drive(); // Driving from Main
		System.out.println(car.topSpeed()); // 180
		car.playRadio(); // Vibe mode on.
	}
}
```

Here we have provided implementation to the abstract methods of `Car` with an anonymous class.

### Interface

Interface is somewhat similar to abstract class
- Unlike abstract class we cannot have normal methos in interface. All methods should be abstract and public.
- In an interface all the methods are `public abstract` by default.

```java
interface Car {  
    void drive();  
    int topSpeed();  
    int fuelCapacity();  
}

class Main {  
    public static void main(String[] args) {  
        Car car = new Car() {  
            @Override  
            public void drive() {  
                System.out.println("Driving");  
            }  
			  
            @Override  
            public int topSpeed() {  
                return 200;  
            }  
			  
            @Override  
            public int fuelCapacity() {  
                return 20;  
            }  
        };  
		  
        car.drive(); // Driving
    }  
}
```

Similar to what we have done in abstract class we have given implementation to Car interface anonymously here.

### Functional Interface
Consider the same above scenario with only one method inside the interface.

```java
interface Sum {
	int add(int a, int b);
}

class Main {
	public static void main(String[] args) {
		Sum sum = new Sum() {
			@Override
			public int add(int a, int b) {
				return a + b;
			}
		};
	}
}
```

Java provides an annotation named @FunctionalInterface to annotate an interface.
Through which IDE can provide intelligence to suggest lambda expressions.
Few take aways
- Since we have only one method inside the interface it is for sure that we are going to provide implementation for that method.
- Hence the object creation part `new Sum()` can be omitted.
  Now we have it like

```java
@FunctionalInterface
interface Sum {
	int add(int a, int b);
}

class Main {
	public static void main(String[] args) {
		Sum sum = (int a, int b) -> {
				return a + b;
		};
	}
}
```

- What we are doing here is removing the above mentioned things and creating a lambda expression.
- Additionally we are just adding a `->` between parameters and implementation.
  This can be further optimized to
```java
@FunctionalInterface
interface Sum {
	int add(int a, int b);
}

class Main {
	public static void main(String[] args) {
		Sum sum = (a, b) -> a + b;
	}
}
```

Here we are
- Removing the curly braces for the declaration of the method since we have only one line.
- Removing the return keyword as there is only one line of implementation that is returned.
- Removing the parameters type as they are already mentioned in the interface definition.
  That is the introduction for functional programming in java.