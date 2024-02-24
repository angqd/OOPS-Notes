# Component
- Setters 
	- setSize(intx, in h)
	- setLocation( int,int )
	- setBounds(int , int , int , int ) this moves and resizes components 
	- setEnabled 
	- setVisible
	- setFocusable
	- setName
- Getters 
	- **getHeight()** Returns the height of this component as an int.
		**getWidth()** Returns the width of this component as an int.
		
		**getX()** Returns the x coordinate of this component as an int.
		
		**getY()** Returns the y coordinate of this component as an int.
		
		**getName()** Returns the name of this component as a String.
# Frame 
- extends window , which extends container which extends Component 
- setTitle(string) : title to input string 
- setResizeable(True) : user can resize the frame 
- setDefaultCloseOperation(action) : sets default close action 
- ![[Screenshot 2023-10-13 at 10.17.54.png]]
```java 


// class that defines frame
class FutureValueFrame extends JFrame{
	// frame constructor 
	public FutureValueFrame(){
		setTitle("Future value Calc");
		setBounds(267,200,267,200);
		setResizeable(false);
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); // set exit action 
		centerWindow(this); // center frame 
		// add panels
		Jpanel panel = new Panel();
		this.add(panel);
	}
	//method that centers the frame 
	private void centerWindow(Window w){
		Toolkit t = new Toolkit.getDefaultToolkit();
		Dimension d = tk.getScreenSize();
		setLocation((d.wifth-w.getWidth())/2,(d.height-w.getHeight)/2);
	}
}
// class that defines a panel 
class Panel extends JPanel implements ActionListener{
	private Jbutton calcBtn;
	private Jbutton exitBtn;
	public panel(){
		calcBtn = new Jbutton("calc"); // define the new button 
		clacBtn.addActionListener(this); // adds the action listener 
		this.add(calcBtn); // add it to the panel 
		exitBtn = new Jbutton("Exit");
		exitBtn.addActionListener(this);
		this.add(exitBtn);
	}
	// coding action to be perfomed on the button click 
	public void actionPerformed(ActionEvent e){
		Object source = e.getSource();
		if(source == exitBtn)
			System.exit(0);
		else if(source == calcBtn)
			calcBtn.setText("CLICKED");
	}
}
// class that displays it 
import javax.swing.*;
public class app{
	psvm(String[] args){
		JFrame frame = new FutureValueFrame();
		frame.setVisible(true);
	}
}
```
- add(Component ) : Adds component to the frame content pane 
# ToolKit Class 
- java.awt package
- Tool kit class helps set the layout of the swing frame 
- getDefaultToolkit():  returns toolkit 
- getScreenSize(): screen resolution returned as dimensions object 
	- Dimension Class : 
		-  Has two fields , height and width 
- Number of pixels can be taken from dimension and toolkit to center ur frame or components 
# Panels 
- Frames contain panels that contain the swing components 
- to add components we first add them to the frame 
- Method fro building swing gui is first building a panels with their various components and then adding that to a frame 
# Button 
- Common constructors : 
	- JButton( ) : Creates button w no text 
	- JButton(String) : Button with string label 
- Methods : 
	- setText(String)
	- getText()
# Handling Action Event 
- Class containing button should implement actionListener interface 
- add an action listener object to the button by addActionListener method 
- **override the actionPerformed(ActionEvent e ){}**
# Layouts 
### FlowLayout 
- Alignement fields are : CENTER LEFT RIGHT 
	- setLayout( layout manager )
	- FlowLayout : centered 
	- FlowLayout( Alignment )
- Inside ur panel constructor we define 
	- this.setLayout( new FlowLayout(FlowLayout.Center));
### Border Layout : 
North west center east south 
```java 
class BorderLayoutPanel extends JPanel
{
	public BorderLayoutPanel(){
		this.setLayout(new BorderLayout());
		JPanel btnPanel = new JPanel();
		btnPanel.setLayout(new FlowLayout(FlowLayout.RIGHT));
		JButton calculateButton = new JButton("Calculate");
		JButton exitButton = new JButton("Exit");
		btnPanel.add(calculateButton);
		btnPanel.add(exitButton);
		this.add(btnPanel, BorderLayout.SOUTH);
		
		
	}
}
```
# Labels 
- Label is used to display text on the screen 
- assign it to a variable or create label and add to panel in single statement 
- get and set methods for the tex t
	-  `this.add(new JLabel("Hi");`
# TextField 
- JTextField(String title, int cols) : textfield with number of cols with , starts with texts specified in the string 
- set and get Text methods 
- set Columns method 
- setEditable
- setFocusable 
# Future Value Calculator 

- ![[Screenshot 2023-10-13 at 11.08.27.png]]
# Further Components  
![[Screenshot 2023-10-13 at 11.34.02.png]]
![[Screenshot 2023-10-13 at 11.36.31.png]]
## TextArea 
- JTextArea(String , intRows, intCols) 
- getText()
- setText()
- setLineWrap(Boolean) :  wrapping of text if it doesnt fir in the text area 
```java 
Private JTextArea = commentTextArea;
commentTextArea = new JTextArea(7,20);
commentTextArea.setLineWrap(true);
JScrollPane commentScroll = new JScrollPane(CommentTextArea);
add(commentScroll);
add(commentTextArea);
// code that creates the scroll panel 
JscrollPane commentScroll = new JScrollPane(commentTextArea,ScrollPaneConstants.VERTICAL_SCROLLBAR_ALWAYS,
ScrollPaneConstants.HORIZONTAL_SCROLLBAR_NEVER); 

```
## ScrollPane 
- JScrollPane(Component, vertical , horizontal ) : scroll panel that displays the specified component and uses the specified vertical and horizontal policies 
- ![[Screenshot 2023-10-13 at 11.42.37.png]]
- 