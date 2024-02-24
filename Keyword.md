
#### Static 
- if we want the class member to be used independently of objects of the class we can use the keyword static to define it 
- It can be used without reference to any instance 
- Instance variables declared as static are like global variables, no copies are made for objects of the class instead they all access the same static variable 
- RESTRICTIONS ON STATIC METHODS :
	- They can only directly call other static methods 
	- they can only directly access static variables of their class 
	- they cant refer to *this* or *super* in anyway 
	- Non static members can be accessed after they have been defined by an instance 
- Anything non static belongs to an instance of a class 
- [[Final]]
