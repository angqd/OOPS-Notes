- Interface is a reference type similar to a class that only contains constants, method signatures and nested types.
- There are no method bodies 
- Interfaces cannot be instantiated 
- They can only be ***implemented by class***  and ***extended by an interface***
- All data fields must be public static final in interface 
- You can omit access modifiers in interface definition
- We can create reference variable of interface type
## Where to choose interface vs [[Abstract classes]] : 
- Strong is-a relationship : parent child relationships, should use abstract classes. Ex: Staff member is a person 
- Weak is-a relationships: is-kind-of relationship, should be modelled using interface. Indicates that an object possesses a certain property.
- Multiple Inheritance: A class can both extend an abstract class and implement an interface at the same time to circumvent, multiple inheritance of classes not being allowed in Java

## Nested interface 
```java 
public class A{
	//nested interface 
	public interface NestedInterface{
		boolead isOdd(int n);
	}
}

class B implements A.interface{
	@Override 
	public boolean isOdd(int n){
		return (num & 1 ) == 1;
		}
}
class Main{
	pvsm(){
		B obj = new B();
		System.out.println(obj.isOdd(7));
	}
}

```
