# Better Constructors

1. **Static Factory Method** - a static factory method is preferred over a constructor when construction logic is complicated. 
2. **Constructor Chaining** - 

The validations are spread across multiple constructors in the code below, violating the DRY principle.

```java
private double balance;
private double interest;

BankAccount(){}

BankAccount(double balance){
	if(balance < 0){
		throw new IllegalArgumentException("Starting balance can't be less than 0");
	}
	this.balance = balance;
}

BankAccount(double balance, double interest){
	if(balance < 0){
		throw new IllegalArgumentException("Starting balance can't be less than 0");
	}
	if(interest < 0){
		throw new IllegalArgumentException("Interest rate can't be less than 0");
	}
	
	this.balance = balance;
	this.interest = interest;
}
```

To resolve this issue, we can use constructor chaining like this: 

```java
BankAccount(){
	this(0);
}

BankAccount(double balance){
	this(balance, 0.01);
}

BankAccount(double balance, double interest){
	if(balance < 0){
		throw new IllegalArgumentException("Starting balance can't be less than 0");
	}
	if(interest < 0){
		throw new IllegalArgumentException("Interest rate can't be less than 0");
	}
	
	this.balance = balance;
	this.interest = interest;
}

```

In this code above, a constructor calls the next constructor, which then calls the next, and so on like a chain. The validations are confined to only the constructor which gets called at the end of the chain. 

 

3. **Builder pattern -**

 Constructor chaining can become a mess as soon as the length of the chain grows beyond a limit, like in the below code: 

```java
Pizza(int size) { ... }
Pizza(int size, boolean cheese) { ... }
Pizza(int size, boolean cheese, boolean ham) { ... }
Pizza(int size, boolean cheese, boolean ham, boolean mushroom) { ... }
```

For such scenarios, where an object needs to be constructed with a different mix and match of initial values of the fields, we can use the builder pattern as shown below: 

```java
class Pizza {
	private final int size;
	private boolean cheese;
	private boolean ham;
	
	static class Builder {
		// mandatory
		private final int size;
		
		// default is false
		private boolean cheese;
		private boolean ham;
		
		Builder(int size) {
			this.size = size;
		}
		
		Builder cheese(boolean value) {
			cheese = value;
			return this;
		}
		
		Builder ham(boolean value) {
			ham = value;
			return this;
		}
		
		Pizza build() {
			return new Pizza(this);
		}
	}
	
	private Pizza(Builder builder) {
      this.size = builder.size ;
      this.cheese = builder.cheese ;
      this.ham = builder.ham ;
  }
}
```

Using the above builder to construct a Pizza instance:
```java
public class App {
	public static void main(String[] args) {
		Pizza pizza = new Pizza.Builder(12)
							.cheese(true)
							.ham(true)
							.build();
	}
}
```