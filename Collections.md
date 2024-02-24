# Diagram
[[Collections Diagram.canvas]]


![[Pasted image 20231013025522.png]]
# Types 
- Main types of collections include 
1. Lists 
2. Sets 
3. Maps 
# Basic Definitions of Collection Classes
Collections framework is the framework which standardises the way in which groups of objects are handled in your program
It implements Iterator interface, that allows u to iterate through the objects 

### Set 
a collection with no notion of positon, sets must have unique elements 
###  Map 
map is collection of pairs of objects 
1. Value 
2. Key  : object associated 
Map set of keys , each key has value , maps dont allow duplicate keys 

# Iterator Interface 
- Iterators implement iterator interface
- Iterator : 
	- is an object associated with a collction 
	- provides methods for fetching elements of the collection, one at a time in some order 
	- Iterators have method from removing from the collection last item fetched 
- methods : 
	- hasNext( ) : boolean 
	- next( ): E 
	- remove( ): void , optional method not all interators have it , removes element last called by next() from the collection 
# Collections Interface
- Lists and Sets extend collections 
- Collection is an **Interface** that describes operations common to borh 
![[Screenshot 2023-10-13 at 03.13.20.png]]
# AbstractCollections 
- Abstract method 
- Skeletal implementation of collections class, using methods of collections interface
- Working collections class can be made using 
	- iterator( )
	- size( )
	- add( o : Object)
# List 
- extends collection interface and adds operations that are specific to position based index oriented nature of list.
	-  List type collections assign an integer (called an index) to each element stored 
	- Indexing starts at 0 
	- List permits duplicate elements , distinguished by their position in the list 
- 
![[Screenshot 2023-10-13 at 03.22.25.png]]
## Abstract List 
class provides skeletal implementation of a List collection 
- extends AbstractCollection and implements List interface 
- superclass of 
	- ArrayList 
	- Vector
## Array List and Vector 
- Array and Vector are array based lists 
- They use array to store their lists 
- Whenever an array gets full they , a new bigger array is created and the elements are copied to the new array 
-  Vector has higher overhead than array ; vectors are synchronised so that they are safe for multiplet threads
##  AbstractSequentialList and LinkedList
- Array based lists have high overhead
	- For elements being removed or inserted at positions that are not the end of the list
- LinkedList removes the overhead of adding elements or removing them from the middle of the list 
- LinkedList extends AbstractSequentialList which  extends AbstractList 
## Using List classes 
- all three classes of List work similarly but they have different perfomance 
- Because they all implement List interface we can define instantiate of List type and then reference the concrete classes later 
	- Variable type : List , Reference Type : we select later 
```java 
// ArrayList
import java.util.*;
public class Test
{
	public static void main(String [ ] args)
	{
		List<String> nameList = new ArrayList<String> ();
		String [ ] names = {"Ann", "Bob", "Carol"};
		// Add to arrayList
		for (int k = 0; k < names.length; k++)
			nameList.add(names[k]);
		// Display name list
		for (int k = 0; k < nameList.size(); k++)
			System.out.println(nameList.get(k));
		}
}
// LinkedList
import java.util.*;
public class Test
{
	public static void main(String [ ] args)
	{
		List<String> nameList = new LinkedList<String> ();
		String [ ] names = {"Ann", "Bob", "Carol"};
		// Add to arrayList
		for (int k = 0; k < names.length; k++)
			nameList.add(names[k]);
		// Display name list
		for (int k = 0; k < nameList.size(); k++)
			System.out.println(nameList.get(k));
		}
}


```

# Using Iterator
 - to use iterator with collection 
![[Screenshot 2023-10-13 at 03.38.17.png]]
- Remove method 
	- The remove() method removes the element returned by the last call to next(). 
	- The remove() method can be called at most one time for each call to next().
## List Iterator 
Extends Iterator by adding methods fro moving backward through the list,(moving forward is provided by iterator )
- hasPrevious() : boolean
- previous(): E 
![[Screenshot 2023-10-13 at 04.06.43.png]]
