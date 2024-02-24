# Data Hierarchy 
- **Character Set** - Java uses unicode characters , = 2 bytes = 8 bits
- **Byte** : can be used to represent byte data
- **Fields** : composed of characters or bytes
- **Records** : related fields 
- **File** : related records
- End of file is always maintained by OS by end of file marker or byte count of file
- Java program receives and indication when it reaches the end of the stream 
- **Text Files** : character - based streams 
- **Binary Files** : read by programs 
# Streams 
*InputStream* is an abstract class that defines java model of streaming byte input 
## Closing the Steam
It implements **Auto-Closeable** and **Closable** interfaces : anything that implements them must be closed after use as it uses the resource for I/O  : they throw IOException
- we can also implement a try( with resources method ) : that automatically closes the stream 
```java
try( FileInputStream f = new FileInputStream("FileInputStream.java")){
	//perform the reading 
}catch(IOException e){
	//print error 
}
```
## FileInputStream
- three stream objects
- **File Streams** will be used for I/O for bytes or characters
	1. Byte Based Streams 
		1. files created by these are called *binary files*
	2. Character Based Streams 
		1. files created : *text files* 
- Opens a file by creating object and associating stream of bytes or character with it 
- Three stream objects when object begins executing 
	- **System.in** : inputs bytes from keyboard
	- System.out : normally outputs character data to screen
	- System.err : outputs character based error messaging  
- To redirect class *system* provides methods 
	- setIn
	- setOut
	- setErr
## FileInputStream
- Java programs perform file processing using classes from package *java.io* 
- **java.io** defines stream classes 
	- FileInputStream(*byte based input from a file*)
	- FileOutputStreamI *(for byte based output to a file)* 
	- FileReader  : character based  input 
	- FileWriter : character based output
- Constructors 
	- FileInputStream(String filePath)
	- FileInputStream(File fileObj) 
	- Both throw *FileNotFoundExcepton* 
## Methods of InputSteam
![[Screenshot 2023-12-18 at 20.05.43.png]]
##  Object I/O
- Java can perform IO of objects or variables of primitive types without converting it to byte format 
- Objects of classes 
	- **ObjectInputStream**
	- **ObjectOutputStream**
- are used along with FileInputSteams and FileOutputStreams 
## Class File 
- Although most of the classes defined by java.io operate on streams, the File class does not. It deals directly with files and the file system. 
- That is, the File class does not specify how information is retrieved from or stored in files; it describes the properties of a file itself.
- A File object is used to obtain or manipulate the information associated with a disk file, such as the permissions, time, date, and directory path, and to navigate subdirectory hierarchies.
- Output stream is abstract class that defines 
- *char* based IO done w 
	- Scanner ( input data from keyboard/ read data from a file)
	- Formatter : enabled formatted data to be outpu to any text based stream 
### Constructors
	- File(String directoryPath)
	- File(String directoryPath, String filename) 
	- File(File dirObj, String filename) 
	- File(URI uriObj)
- *directoryPath* is the path name of the file, 
- *filename* is the name of the file or subdirectory 
- *dirObj* is a file object that specifies directory 
- *URI* is the uri object that describes a file 
- ##### Paths 
	- path information in the file is either *absolute path* contains all directories starting with root directory 
	- *relative path* begins from directory in which application begins executing ; thus relative to the current directiry 
- URL  : UNIFORM RESOURCE LOCATORS locate websites 
- URI : UNIFORM RESOURCE IDENTIFIERS  more general form of the URL
### File Methods 

![[Screenshot 2023-12-18 at 19.41.02.png]]
![[Screenshot 2023-12-18 at 19.41.39.png]]

### Seperators 
- File.seperator to get ur systems correct seperator  `\ is used in windows 
- /  is used in linkux / UNIX 
## Output Stream 
- FileOutputStream creates an OutputStream that you can use to write bytes to a file. It implements the AutoCloseable, Closeable, and Flushable interfaces. Four of its constructors are shown here:
	- FileOutputStream(String filePath)
	- FileOutputStream(File fileObj) 
	- FileOutputStream(String filePath, boolean append)
	- FileOutputStream(File fileObj, boolean append)
- Throws FNF exception 
- Creation of a FIleOutputStream is not dependent on the file already existing 
#### Methods of Output Stream
- ![[Screenshot 2023-12-18 at 20.29.39.png]]
- 
# Sequential Access Text Files
- store records in order by the record key field 
- always recommeded to use all scanner formatter inside try catch to find their specific exceptions 
### Formatter
- Formatter works by converting the binary form of data used by a program into formatted text.
- Formatter method format works like the system.out.printf for formatting the strings
- Formatter outputs formatted strings 
- Formatter close not called explicitly
- OS closes it on program execution termination 
- Scanner  *.hasNext()* is used to check whether the end of *end-of-file* key combination has been entered 
- 
```java 
output = new Formatter("clinet.txt"); 
// string input is assumed to be path 
// if file DNE , this creates file in diretory 
try{
	output.format("%d %s\n", record.getAccount(),record.getFirstName());
	}catch( FormatterClosedException formatterClosedException){
}

```
- **SecurityException** : user doesn't have permission to write data to the file 
- **FileNotFoundException**  
### Updating Sequential-Access Files
- data in many sequential fies cnnot be modified 
- if a name needs to be changed it cannot be simply edited as the new name required more space in some cases 
- Thus the entire file is rewritten
## Object Serialisation 
- to read an object from/ write an object from a file 
- A serialized object is represented as a sequence of bytes that includes the object’s data and its type information.
-  After a serialized object has been written into a file, it can be read from the file and deserialize to recreate the object in memory.
- If object is of wrong type it wont throw compilationError it will show in the runtime 
- **ObjectInputStream and ObjectOutputStream** implement ObjectInput and ObjectOutput interfaces and enable entire objects to be read/written wrt stream
- To use serialisation w files 
	- initialize ObjectInputStream and with FileInputStream and same for Output 
 ObjectOutput interface method writeObject takes
an Object as an argument and writes its information to an
OutputStream.
### De-serialisation 
- during deserialisation, when the output stream is written into an object , the constructor of that object if it is serialised will not be called. But if it has a parent class that is not serialised then , the parent constructor will be called
- Follow slides for rest 
- Serialisation is a tagging interface :  has no method to be overridden  [[Interfaces]] 
```java
//Object 
package filess;  
import java.io.Serializable;  
public class Student implements Serializable {  
    public int rollno;  
    public String sName;  
}

//Serialisation 
public class SerialisationDemo {  
    public static void main(String[] args) {  
        Student s1 = new Student();  
        s1.rollno = 20;  
        s1.sName = "angas";  
        String fileName = "ob.txt";  
        try{  
            FileOutputStream fileOutputStream = new FileOutputStream(fileName);  
            ObjectOutputStream objectOutputStream = new ObjectOutputStream(fileOutputStream);  
            objectOutputStream.writeObject(s1);  
            objectOutputStream.close();  
            fileOutputStream.close();  
            System.out.println("Object saved to file");  
        }catch (FileNotFoundException e){  
            e.printStackTrace();  
        }catch (IOException e){  
            e.printStackTrace();  
        }  
    }  
}
//Deserialistion
public class Desrialisation {  
    public static void main(String[] args) {  
        String fileName = "ob.txt";  
        try{  
            FileInputStream fis = new FileInputStream(fileName);  
            ObjectInputStream ois = new ObjectInputStream(fis);  
            Student obj = (Student)ois.readObject();  
            System.out.println(obj.rollno);  
            System.out.println(obj.sName);  
            ois.close();  
            fis.close();  
        }catch (FileNotFoundException e){  
            e.printStackTrace();  
        }catch (IOException e){  
            e.printStackTrace();  
        }catch (ClassNotFoundException e){  
            e.printStackTrace();  
        }  
    }  
}

```
## J File Chooser 
```java
import javax.swing.JFileChooser;
import javax.swing.JFrame;
 import javax.swing.JOptionPane;
 import javax.swing.IScrollPane;
 import javax.swing.JTextArea;
 import javax.swing.JTextField;
 
private File getfileOrDirectory(){
	JFileChooser fileChooser = new JFileChooser();
	fileChooser.setFileSelectionMode(JFileChooser.FILES_AND_DIRECTORIES);
	int result = fileChooser.showOpenDialog(this);
	if(result == JFileChooser.CANCEL_OPTION)
		System.exit(1);
	File fileName = fileChooser.getSelectedFile() // get the file 
	// handle error 
	if( // error ){
	}
	return fileName;
}

```