
# Basic 
Polymorphism implies having many forms
- all object types in java are polymorphic 
- **Polymorphic Reference**: 
	- variable that can refer to different types of objects at different times 
	- Method invoked through it can potential change from one invocation to the next
- The ability to redefine methods 
- Every variable has two types 
	1. **Declared Type** : type in declaration 
	2. **Actual Type** : the type of object that the variable references
# Static Polymorphism :
- also called compile time polymorphism 
- Method overloading : same name of method but different return types, parameters
# Dynamic Polymorphism :
- runtime polymorphism :
- Method overriding 
- ## Method Overriding 
- If you have method with same name in subclass, when subclass is called then it will call the version of method from subclass 
- To call the superclass version we can use super.methodName();
- If the names and parameters are not identical then they are overloaded
```java 
@Override // annotation 
	void area(int a, int b){
		// if this method is overriding this annotation remains 
		// if it isnt the annotation will throw an error
	}
```

### Upcasting 
When calling overiden method : 
	- `Parent obj = new Child();`
	- What it can **access** is defined by type of reference: here : *parent*
	- And which one it can access is defined by type of the object
	- The method that will be called depends upon the object type : *Child*
	- A super class reference variable can refer to a subclass also 
- Every class extends the object class in java 
- [[Final ]] keyword can be used to prevent method overriding 
### Overriding static methods 
- If static methods were being inherited then there is no point in overriding them in the child class as the method in the parent class will always run no matter from which object : As it is static 
- Thus they can be inherited but not overiden 
- Overriding depends on objects, but static methods are independent of objects , thus they cannot be overide.
# Wrapper 
class that converts primitive types to objects 
Autoboxing : primitive -> object 
Unboxing : Object -> primitive
- 
