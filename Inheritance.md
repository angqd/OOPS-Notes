- ![[Pasted image 20231013130024.png]]
- Use the extends keyword to create the child class from the parent class 
-  *Important* : constructor of the child class must initialise variables of the parent class
-  Super is a [[Keyword]] that calls the parent class constructor 
```java 
class subclass_name extends superclass_name {
// body 
}
class Parent {
	int x;
	int y;
	Parent(int x, int y){
		this.x = x;
		this.y = y;
	}
}
class Chid extends Parent{
	int z;
	Child(int x, int y, int z){
		super(x,y) // calls the constuctor of the parent class 
		this.z = z;
	}
}
class Main{
	public static void main(String[] args){
		Parent c = new Child(4,5,6);
		// c cannot access z as it is a object of type Parent it doesnt have access to the z variable in subclass child 
	}
}
```
- The class can access all *public* members of the superclass, all members declared *private* cannot be accessed by the child/subclass 
- In general *private* members can only be accessed from within the file itself
- Remember, once you have created a superclass that defines the general aspects of an object, that superclass can be inherited to form specialised classes. Each subclass simply adds its own unique attributes. This is the essence of inheritance.
- *Superclass Variable can Access subclass object*
