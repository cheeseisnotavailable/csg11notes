# CS Notes G11

September 3, 2024
## Intro to Recursion
Recursion - when a function calls itself and everything gets horribly confusing
Iteration -> like a for loop (which is why the variable for for loops is “i”)

The “stop condition” is called the base case, which is where the recursion stops. This base case cannot have recursion, otherwise it will go forever. Naturally, the recursive step has to get closer and closer to the base case. 

September 4, 2024
## Intro to OOP

Improving the structure of your programs can bring several advantages, such as making the code clearer, easier to maintain, easier to debug, simpler to scale, etc. 

OOP - further change to program structure. 

Humans think of the world by categorizing things into objects so that they know things about things that they’ve never seen before as long as they’ve seen the same type of thing before. So if you’ve seen a couple of cups, you’ll know what a cup is and what you can do with it. 

Objects in CS have:
Data/states (variables or data structures)
Actions/behaviors (functions, methods, procedures)

Example:
Cat Object
States:
Name - Monkey
Age - 7
Hungry - true
Colors - brown, white
Weight - ~5kg
Behavior:
Speak - tells you if the cat is hungry?
Eat - increases weight?
Claw at furniture
Fight roommates


public class Cat{
	String name;
int age;
boolean hungry;

public boolean isHungry(){
	return hungry;
}
}

OOP benefits:
Easier to debug
More modular
Easier to add more functionality

September 5, 2024
## Classes & Objects

What’s the difference between a class and an object?
A class is like a mold for an object.
You can make infinitely many objects from a class. In CS, you can’t really make classes from an object.
Though, a class does not have to have objects for us to use methods from it. For instance, we never have to make IBIO objects to use IBIO.output().
This is because the methods are static!
Main is also static!
Static - a non-access modifier denoting things that belong to the class itself rather than specific instances of the class
But if we’re doing actual objects, we can’t use static, because we’re looking for the properties specific to actual objects and not to the class. 
One example of an acceptable time to use these is when defining the number of sides of a rectangle, since all rectangles have 4 sides. 

Class - an extensible program-code-template for creating objects, providing initial values for states and implementations of behaviors

Object - a particular instance of a class, where the object can be a combination of variables or data structures and functions, procedures or methods.

Steps in object creation:
Declaration - variable name & object type
Instantiation - “new” -  used to create new objects
Initialization: the “new” keyword is followed by a call to the constructor, creating a new object.

Circle c = new Circle();

Reference variable (object) vs. primitive
If we declare an object named A, then write Object B = A, if you change A, B’s values will also change. This is because B is just a reference to A and not its own object.


You can add parameters into constructors!
As in: Rectangle r = new Rectangle(4, 3);
Why?
We can force the user (other programmers) to provide defaults
Programmers do not have to understand the innermost details of the object. You don’t necessarily want people touching, for example, the width of the rectangle all of the time. You can keep them secret.

//Constructor!
Rectangle(int width, int height){
	this.width = width;
	this.height = height;
}

September 6, 2024
## Encapsulation

Private or public - what does that mean in CS? Directly changing the state information of an object from a different class is like borrowing someone’s stuff behind their backs. 
Encapsulation - keeping all state variables private, which means they cannot be directly accessed or changed from an outside class. 
Or, to use the fancy IB definition: 
Encapsulation refers to the practice of hiding the structure and representation of data within a class and making it accessible outside the class via accessor functions.
So how would you change it?
Make a public method that allows you to access it! Such as:
public void setWidth(int w){}
Conventionally called getters and setters

Private - only accessible in its own class
Protected - you and your children can use it, even if your children are in a different package (and also non-subclasses within the same package(!))
Default -  (package access)
Public - accessible across all classes, even outside the package

Advantages:
Data hiding/data integrity
Control access — allows validation or extra logic,  protecting against unintended changes. 
Increased flexibility
Modularity and reusability
Bundles stuff into related classes; Code is easier to understand
Modify internal implementation without affecting other stuff as long as the public interfaces don’t change
Testing a little bit of code at a time is easy (unit testing)

September 9, 2024
## OOP, Continued

The class with a main method is called the driver class in a project.
You can use packages to organize your code within a project, even though Mr. Gunn doesn’t do it in class. 

When you have encapsulation, instead of directly using r.width, you can create methods in your class called getters and setters that allow more directed access to these variables. For example, you could make the function to report different things depending on who’s asking it. Or, you could make it inaccessible.

	public int getWidth(){
		return width;
	} //this is called a getter or accessor

	public int setWidth(int w){
		width = w;
	} //this is called a setter or mutator

You can do this easily in IntelliJ using the Generate command (⌘N). 

A note on “this”:
private int width;
private int height;

Rectangle(int width, int height) {
    this.width = width;
    this.height = height;
}

Even though width and width are the same word, this.width tells you that it’s referring to the width of this object specifically, much like r.width. It differentiates the local variable and the instance variable.

public int getWidth(int width) {
    return width;
}

The above code will return the input instead of the width of the object. 

Only when the keyword “new” is used, a space is reserved in memory for the whole object. 

UML - Unified Modeling Language


This is a UML diagram, and it shows you stuff about the class so you can plan it out / tell people about it.  
Website tool: draw.io

September 10, 2024
## Relationships

Relationships between classes in a UML diagram is shown with lines or arrows.

Decomposition: breaking the code or design into smaller and more manageable pieces

Dependency - “uses”
One somehow uses the other (a very weak relationship). Changing one will have an effect on the other.
Example: Player - - - - > Bat (the player uses the bat, but the bat is not a part of the player, and a player is not a bat.)
In code, one object might reference another object in a method, etc. 

Aggregation - “has a”
Both entries can survive individually
Example: Cup —◊ Person (“the person has a cup”)
Association is like aggregation, except in Aggregation, an object can sort of survive on its own. 
In code, an object might have another as a status variable.

Inheritance - “is a” 


	public class Person extends Animal{ 
	}

Inheritance is the mechanism which one class 
Child (sub) classes can inherit behaviors from the parent (super) class. 
In java, you can only inherit from one class at a time, but one class can extend from another class that extends yet another class (multilevel inheritance!)
Advantages:
Minimizing amount of duplicated code by sharing common code
Easier to write & easier to debug (reduced maintenance overhead)
Simplifies further development and expansion
Classes from a common super class can be used interchangeably

September 11, 2024
## Recursive Searching

public static int search(int[] data, int value, int i){
    if(data[i] == value){
        return i;
    }
    return search(data, value, i+1);
}


//This one is more like binary search!
public static int searchalt(int[] data, int value, int low){
    if (low == data.length){
        return -1;
    }

    if (data[low] == value){
        return low;
    }
    
    return searchalt(data, value, low+1);
}


If the data is sorted, we can do binary search!
 //This one *is* binary search!
public static int searchalt(int[] data, int value, int low, int high){
    int middle;

    if (low > high){
        return -1;
    }

    middle = (high+low)/2;

    if (data[middle] ==  value){
        return (middle);
    }

    if(data[middle]<value){
        return searchalt(data, value, middle+1, high);
    }else{
        return searchalt(data, value, low, middle-1);
    }
}


September 12, 2024
## More Relationships

If a Dog is an Animal (inheritance) and all Animal objects can eat Food (dependency), all Dog objects automatically can also eat Food. (When drawing a UML diagram, you should point the dependency arrow from Animal to Food and not from Dog as well.)

September 13, 2024
## More OOP
final = cannot be changed. Usually final things have titles that are IN ALL CAPS.

September 14, 2024
## Making the Library Thing

Switch (option){
	case 1: 
		break;
	case 2:
		break;

“null” means no object
NullPointerException means you’re trying to command an object that doesn’t exist to do something

All objects are child classes of a class called Object, which has a method called toString() built into it. It returns a String version of your object (reference to the object).

You can, however, generate your own toString() in the object that overrides the original one to make it whatever you want. 

September 18, 2024
## File Systems!

To read and write files, go to Oracle and copy their code. Import all the classes, and attribute it.

package LibraryMS;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.nio.charset.Charset;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

/*

This class contains code to help us read and write files.
It was written in Mr. Gunn's class.

Most this code is modified from:
https://docs.oracle.com/javase/tutorial/essential/io/file.html#:~:text=Learn%20how%20to%20use%20various%20methods%20and%20options%20to%20read,

 */
public class FileUtilities {

    /*
        Read a file from the path( path) and return it
     */
    public static String readFile(String path) {
        Path file = Path.of(path);
        String data = "";
        // Charset charset = StandardCharsets.US_ASCII;  // ASCII
        Charset charset = StandardCharsets.UTF_8; // Unicode
        try {
            BufferedReader reader = Files.newBufferedReader(file, charset);
            String line = reader.readLine();
            while (line != null) {
                data += line + "\n";
                line = reader.readLine();
            }
            reader.close();
        } catch (IOException x) {
            System.err.format("IOException: %s%n", x);
        }
        return data;
    }

    /*
    This method helps write a text file (path) with the contents in data
     */
    public static void writeFile(String path, String data) {
        Path file = Path.of(path);
        //Charset charset = StandardCharsets.US_ASCII;
        Charset charset = StandardCharsets.UTF_8; // Unicode
        try {
            BufferedWriter writer = Files.newBufferedWriter(file, charset);
            writer.write(data, 0, data.length());
            writer.close();
        } catch (IOException x) {
            System.err.format("IOException: %s%n", x);
        }
    }
}


September 19, 2024
## Polymorphism

OOP -  Abstraction, Polymorphism, Inheritance, Encapsulation
Polymorphism - “Having many forms”, allows us to perform a single action in multiple different ways.
Overloading - where there are multiple functions with the same name but different parameters 
Also called compile-time polymorphism or static polymorphism

	Library (int size){
	this.size = size;
	//In this one you can define the number of books you want!
	}

	Library(){
	this.size = 10;
	//In this one you end up with a default value, say.
	//This constructor can be overloaded if you use the one with the 			int.
	}

Overriding -  when a subclass has a definition for one of the methods of the superclass
Also called runtime polymorphism or dynamic polymorphism

	class Animal(){
		void speak(){
		}
	}
	
	class Dog extends Animal(){
		@Override //this is a comment!
		void speak(){
			IBIO.output(“woof”);
		}
	}


This works because of polymorphism:

	Animal myDog = new Dog();

Like linking a more general remote control with all the Animal buttons, except it’s a Dog.
For instance, we could make an array of Animals that are of different types!

	Animal[] animals = new Animal[2];
	animals[0] = new Dog();
	animals[1] = new Cat();

	for(Animal a:animals){
		a.speak();
	}
	//And they can all speak in their own ways!

“super" - A bit like “this” - a reference to the super class

	public Dog(String name, String age, String breed){
		super(name, age); 
		//Lets the super class make the constructor 
		//So that you don’t have to handle it again
		this.breed = breed;
	}

Advantages:
Allows a general class to specify methods that will be common to all its derivatives while allowing sub classes to define the specific implementation of some or all of those methods
Overridden methods: make us able to call methods of any derived class without knowing the type of derived class object (like the cat and dog speaking example)
Overloading: we don’t have to remember different names for different functions that do largely the same thing (e.g. we don’t have to call a different method to print different data types, we can use the same output.)


September 20, 2024
## More Recursion

Tracing in an exam
Example:
fib(N) = fib(N-1) + fib(N-2)
fib(4) = fib(3) + fib(2)
	= fib(2) + fib(1) + fib(1) + fib(0)
	=fib(1) + fib(0) + 1 + 1 + 0
	= 1 + 0 + 1 + 1 + 0
	= 3

Advantages of recursion:
- Can be used to make clearer and simpler versions of several algorithms, such as QuickSort. 

Disadvantages of recursion:
Execution/Call stack issue
The order of things being executed is kind of screwy. 
Stack -> when you always add to the top and remove from the top, and are not allowed to take stuff from the middle. Last In, First Out (LIFO)
An iterative loop that runs forever will just keep going until you stop it.
A recursive loop, on the other hand, will keep trying to store the next step in the memory until it runs out of memory, crash, throw you a thousand exceptions, and tell you there’s a stack overflow.
The more RAM you use up, the slower your code runs, which we do not like in CS. 

Conclusion: recursion is cool, but you shouldn’t use it. 

September 23, 2024
## Abstraction
- Hiding the details about how you do something so you can think of them more clearly. A part of computational thinking. 

September 24, 2024
## Control Systems Intro

Control System - device or set of devices that manages, commands, or regulates the behavior of other devices and systems.

Input(sensors) -> process(computer) -> output(actuators)
Smoke sensor -> internal computer -> loud noise from speaker

Sensor - a device which detects or measures a physical property and records, indicates, or otherwise responds to it
Input device vs. sensor
Sensors - part of a larger system
Input devices measure human actions and output data that computer then uses.
Microprocessor/processor - an integrated circuit that contains all the functions of a central processing unit of a computer

Accessibility input devices
For disabled people
e.g. joystick and switch to use virtual keyboard for those unable to use physical keyboard, keystrokes with mouse, headcount, etc. 

Analog - continuous signal (physical measurement, like temperature)
Digital things want ones and zeroes. This transformation is done by a transducer

Centralized system - all the computing is done at a central location using terminals attached to a central computer; computers/terminals control peripherals
Easier administration
More control
Single point of failure
Distributed/decentralized system - components located on networked computers communicate with each other to achieve a shared goal
Shared load
Quicker access
Responses can be more specific to the environment
More expensive and complex

October 8, 2024
Microprocessors & Sensor Input

Microprocessor - an integrated circuit that contains all the functions of a central processing unit of a computer

Feedback - modification or control of a system based on its results or effects

Transducer - a device that converts variations in physical quantity into electrical signals or vice versa. 
Types:
Actuators (devices that move stuff)
Sensors
Ease of amplification
Ease of integration and differentiation
Ease of convertibility from analog to digital and vice versa
Remote controllability and easy data transmission capability
Compatibility with microprocessors and computers

Driver - software that provides the necessary interface between a hardware device and the operating system (OS)
Software -> operating system -> device driver -> hardware
The software of a printer, say, does not itself contain different things to adapt to different OSs. The driver does this. 

Sensors - input devices that provide an output (signal) based on their input (with respect to a physical quantity)
Can be active (requires an external excitation signal or a power signal) or passive (do not require external power to generate a response)
Examples!
Light sensor -  the sensor on a phone (so that the brightness of the screen matches the environment) - passive - analog?
Temperature sensor - the sensor in a fridge (a thermistor) - active - analog
Force/pressure - in a scale - active - analog
Sound - passive - analog
Location - car GPS - active - analog
Proximity - RADAR - active - analog
Orientation - gyroscope - passive - analog

Byte - 8-bit
Long - 64-bit

October 10, 2024
## Internationalization?
What enables modern programming languages to be used around the world?
ASCII
Only a few hundred characters
Each character is 8 bits long (even though you only need 7 bits for standard characters)
The extra character could be used to incorporate different languages, but this caused problems because each language maps these differently 
Unicode a.k.a UTF
16+ bits per character (can change in size)
Encompasses basically all languages and symbols used worldwide
Java supports Unicode!
Platform Independence
You can run Java byte code on any hardware that has a compliant JVM.
Java app -> JVM -> OS -> hardware
Resource bundles

October 15, 2024
## More sensor stuff 7.1.4

Process:
Sensor (input)
analog (antialias) filter 
analog to digital converter (ADC) 
digital processor
digital to analogue converter (DAC)
analog (reconstruction) filter
actuator (output)
Analog signals have to be converted to digital (and vice versa)
Original signal (sine wave) -> sampled signal turned into binary -> reconstructed digitally

October 22, 2024
Preconditions, try/catch.
Preconditions and postconditions are constraints, ensuring that the input and output of a process is valid according to the method’s expectations. 
Types:
Comments 
//This must be positive.

Exceptions
Throwable objects
Errors =/= exceptions!
Errors are caused by serious problems that are outside the control of the program
OutOfMemory (when the JVM runs out of memory)
StackOverflowError (stack runs out of space)
Exceptions can be recovered from / handled while the program is running
NullPointerException (when a null reference is accessed)
IllegalArgumentException (when an illegal argument is passed to a method)

	try{
		//what you want to happen
	}catch (IndexOutOfBoundsException e){ //Exception
		System.err.println(“ERROR MESSAGE!”);
	}

November 4, 2024
## Trees
Hierarchical structure with a bunch of interconnected nodes
Focus: Binary Search Tree
Where each node can have at most two child nodes
Search -> the node’s child node on the left is smaller, the one on the right is larger. 

November 5, 2024
## Feedback
Feedback - output value is continuously compared to desired value to produce an error value. The controller uses the error value to determine the new input to the system.
Used to maintain stability and desired performance

Watering System Pseudocode
	if LIGHT INTENSITY > LIGHT INTENSITY THRESHOLD
		if FLOWERBED WATER CONTENT < MIN WATER
			start watering
				while FLOWERBED WATER CONTENT < MAX WATER
					keep watering
				end while
			stop watering
		end if
	end if

Embedded Systems
Specialized computing systems that perform dedicated functions or tasks within a larger system
Single or limited functionality
Pre-programmed software (firmware)
Programmed directly into the hardware (ROM)
Resource-constrained - designed to be resource-efficient
Real-time or real-time operation

Autonomous Agents - entities that make decisions according to their environment without continuous human input


Nov 7, 2024
## Concurrency
Threads - extendable class where you can tell things to run()

Nov 12, 2024
## Abstract Data Types/Structures
A conceptual model for a data type
Specifies the behavior of the data type through operations, doesn’t specify how the data is actually stored

Stack - LIFO - Last in, first out
Push (put in) Pop (take out)
isEmpty()

Nov 13, 2024
## Algorithms
Sequential search - search algorithm where you search each one in an array until it matches. 

NAMES.resetNext()
loop while NAMES.hasNext()
	TEST = NAMES.getNext()
	if character at TEST[0] == D
		output TEST
	end if
End loop

Nov 14, 2024
## Reading Files

Buffers - useful when one thing is done much faster than another
So that the program doesn’t have to wait byte by byte for the file to read
Hard drives are thousands of times slower than the cpu
Buffered readers download everything from the file into temporary internal storage
String name = IBIO.input("Enter name of student:");
String path = "grades.csv";
int c = 0;
try {
    BufferedReader reader = new BufferedReader(new FileReader(path));
    c = reader.read();
    boolean readingName = true;
    boolean nameFound = false;
    boolean stopReading = false;
    String nameToken = "";
    while (c!=-1 && !(nameFound && (c == '\n'))) {
        //System.out.print((char) c);
        c = reader.read();
        if (c == ',') {
            readingName = false;
            if(nameToken.equals(name)){
                nameFound = true;
            }
            nameToken = "";
        } else if (c == '\n') {
            readingName = true;
        }  else if (readingName) {
            nameToken += (char) c;
        } else if (nameFound ){
            System.out.print((char) c);
        }
    }
    reader.close();
} catch (FileNotFoundException e) {
    IBIO.output("File not found!");
} catch (IOException e) {
    IBIO.output("Something went wrong :(");
}

OR!
String name = IBIO.input("Enter name of student:");
String path = "grades.csv";
String line = "0";
try {
    BufferedReader reader = new BufferedReader(new FileReader(path));
    line = reader.readLine();
    while(line != null){
        line = reader.readLine();
        if(line.split(",")[0].equals(name)){
            System.out.println(line.split(",")[1]);
        }
    }
    reader.close();
} catch (FileNotFoundException e) {
    IBIO.output("File not found!");
} catch (IOException e) {
    IBIO.output("Something went wrong :(");
} catch(NullPointerException e){

}


November 21, 2024
## Searching

(Complexity - time of the worst case scenario)
Binary Search: O(logn) (log here has base 2)
Sequential search: O(n)
Bubble sort: O(n^2)

Adding “flags” that stop the code early may make the code faster, but they don’t improve the complexity.

Random Access Files

public static void main(String[] args) {
    try {
        RandomAccessFile raf = new RandomAccessFile("grades.bin", "rw");
        int recordSize = 10+1;
        String name = IBIO.inputString("What student do you want to look up?");
        int grade = findGrade(name, raf, recordSize);
        if(grade == -1){
            IBIO.output("Student not found");
        }else{
            IBIO.output("The grade of "+name+" is "+grade+".");
        }
        raf.close();
    } catch (FileNotFoundException e) {
        throw new RuntimeException(e);
    } catch (IOException e) {
        throw new RuntimeException(e);
    }
}

public static int findGrade(String name, RandomAccessFile raf, int recordSize) throws IOException {
    byte[] nameBuffer = new byte[10];
    String currentName;
    int min = 0;
    int max = (int) (raf.length()/recordSize-1);

    while(min <= max){
        int mid = min + (max - min) / 2;
        raf.seek((mid*recordSize));
        raf.readFully(nameBuffer);
        currentName = (new String(nameBuffer)).trim();
        int comp = currentName.compareTo(name);
        if(comp == 0){
            return raf.readByte();
        }
        else if (comp > 0){
            max = mid-1;
        }else if(comp < 0){
            min = mid+1;
        }
    }

    return -1;
}


Dec 2, 2024
## GUI

AWT -  Abstract Window Toolkit - Ancient platform-dependent thing
Swing - platform independent - no hardware acceleration
JavaFX -  new standard for Java GUI

MVC - model view controller
Controller - like “main”
View - visible stuff
Model - where all the data lives (or a file or something)
Dec 4, 2024
Queues and LinkedLists

Stack - Last In, First Out
Push to add to the top of the stack
Pop to take from the top of the stack
isEmpty
Queue - First In, First Out
Enqueue to put in the queue
Dequeue to take out of the queue
Also has isEmpty

LinkedList Example:

public class Queue {
//    Collection data;
    int pointer;

    private class Node{
        Object value;
        Node next;

        public Node(Object value){
            this.next = null;
            this.value = value;
        }
    }

    private Node front;
    private Node back;

    public Queue(){
        pointer = 0;
        front = null;
        back = null;
    }


    void enqueue(Object value){
        Node n = new Node(value);

        if(back == null){
            back = n;
            front = n;
        } else{
            back.next = n;
            back  = n;
        }
    }

    Object dequeue(){
        if(front == null){
            throw new IllegalStateException("Your queue is empty! There's nothing to dequeue!");
        }else{
            Object ret = front.value;
            front = front.next;
            return ret;
        }
    }

    public boolean isEmpty(){
        return front == null;
    }
}


We want stacks and queues to be O(1) operations. If we used a static data structure, managing the array would make it too complex. 

LinkedList:
A list has many nodes and may have a head or tail. Each node has its data and its next.
Like a line of unruly kindergarteners
If you unlink a node, it eventually gets deleted by the Garbage Collector, which is constantly checking for things that have no memory reference. 


Dec 6, 2024
## Basic Computer Stuff

The five most fundamental operations are add, compare, retrieve, store, and branch (go to another place)
Operating Systems -> a program that puts another program in the computer

Natural vs computer languages
Natural languages evolve, computer languages are highly fixed
Ambiguous vs. non-ambiguous meaning

Low-level languages - only fundamental operations, one instruction per cycle

Translators - High-level to low-level code
The simplest translator is an assembler
Compiler vs. Interpreter
Compilers -> like someone who translates an entire speech beforehand, executing the whole thing afterward
Interpreter -> like someone who reads a sentence of a speech and translates it line by line, executing each line immediately
For obvious reasons, compilers are generally more optimal.
Faster execution - compiled programs run faster at execution time because it’s already translated into ML
Portable - once compiled, the code can run from any system with a compatible architecture with out the need of the compiler installed. (Example - .exe files are executable versions already!)
Error checking - compilers perform a thorough check for grammar and syntax errors before program execution using the entire program
Advantages of Interpreter 
Immediate feedback for errors
Platform independence - can run on any program with the interpreter (equivalent - code can run on any computer where you have Python, for example, installed)


JDK - Java Development Kit
Tools for developing applications
JRE - Java Runtime Environment
JVM - Java Virtual Machine
Heap memory, stack memory memory area, JIT…
Libraries
Java standard extensions

Java is a compile-interpreted language
.java files (source code) are compiled into a .class file (byte code), which is interpreted into the machine code (output)
You can’t really decompile byte code properly, which gives it more security
JVM - allows the same java code to be run on many different types of hardware

Dec 30, 2024
## Binary Tree

Root is at the top
Parent -> left child, right child
Leaf nodes - nodes that have no children

In a binary search tree, the left node contains values less than the parent and the right contains values greater than the parent.
If the data is well-balanced, it’s very easy to sort. 

Jan 2, 2025
Tree Traversal



For a binary search tree, preorder reads subtree by subtree, and each node happens before its left node. Inorder reads from min to max, hence the name. In postorder, each node happens after its subtrees. 

State two applications of stacks. [2]
In a stack, the last one to be put in is the first one to be taken out. 
Examples: simulating recursion, parsing, undo function in computers

Explain the use of a one-dimensional array as a static stack. Your answer should include brief outlines of the push and pop operations and the test for empty and full stacks. [6]
LIFO
What’s a static array?
Add things by storing the number of elements in the array
Push -> add to the end, 
Pop -> return the end one and remove it from the array
Test for empty stack -> test if the first one is 

Compare the use of static and dynamic data structures. [3]
Static data structures have a fixed size, while the size of dynamic data structures can change throughout the program. 
Dynamic data structures are useful when you do not know how the ultimate size of the data. They are more flexible in those situations. 
Static data structures have lower overhead because the memory is allocated during compile time
Static data structures allow faster access times than dynamic ones because in a dynamic one you have to look through the entire thing (direct access vs. sequential access)


Feb 18, 2025
## Storage
CPU: Central Processing Unit
Like the conductor of an orchestra - everyone else already knows what to play, but they can’t coordinate themselves
Buses - connection wires that connect the CPU to other devices, carrying instructions to/from components.
Everything connected to the bus has access to the communication regardless of whether they’re the target; Information is controlled and interruptions prevented by ordering when communications happen
The MAR gives the address the data of the MDR will be read from or written to.
Caches: faster and smaller than RAM, slower and larger than cache
Comparison: pencil cases within a backpack - searching the pencil case first can get you to smaller things with faster access required - you could still find it without using a pencil case by just throwing everything into your bag, but it might be slower.
L1 L2 L3 are physically further and further away from the CPU, memory is in a different place
Small, high-speed memory inside the CPU to hold frequently used data so the CPU needs to access the much slower RAM less frequently


ALU: Arithmetic Logic Unit
CU: Control Unit

CPUs need their own “memories” - registers - MAR & MDR. 
MAR: Memory Address Register
MAR is connected to the address bus and contains a memory address. Its sole function is to contain the RAM address of the CPU instructions.
MDR: Memory Data Register
Temporarily stores instructions from RAM during the fetch stage. Holds a copy of the contents of the memory which are transferred from/to memory from/to other CPU components, allowing the processor and memory to act independently so that the processor is not affected by speeds in the difference in operation. 
ALU - the part of the CPU that does all the arithmetic (+/-) and logical (AND/OR) operations
Also called the “core”


Programs are loaded from storage, into memory (RAM) and executed one instruction at a time by the CPU

RAM - Random Access Memory - even though lots of memory is random access now; a.k.a. memory
Primary memory
System RAM and the caches are “volatile” memory, the stuff underneath it is “permanent”
Volatile - things are susceptible to rapid changes - contents lost if power is lost
Special links to the CPU with three special buses: address, data, control.
Contains user programs that have been loaded since the computer has been booted

ROM - Read-only memory - even though it’s not
Originally its contents were static, but not anymore
Non-volatile
Stores the BIOS (Basic Input Output System) - a small program that allows the computer to know what to do after the operating program starts (how to boot the computer)

Fetch-decode-execute-store - machine instructing cycle
state where all instructions and data are stored: RAM/memory/primary storage
Outline the role of the address bus and data buss in this process:
	Data bus - bus (physical connection) that takes data from the RAM to and from the MDR
	Address bus - transports the address of memory storage where data should be read/written
(c) Outline the role of the memory data register in the machine execution cycle. 
	
Persistent memory
Data that’s stored forever that isn’t deleted whenever the machine reboots
Mechanical Hard Drives (HHD)
Solid state drives (SSD)
Flash memory (USB drives)
Stores operating systems, applications, and user data permanently
Usually much larger than RAM

File - logical unit of storage that contains data
“logical” - not *really* one thing
Name - human-readable identifier
File size
Permissions (read only, read-write, etc.)
Info about itself (creation date, etc)
Kept in a file system

Differences between primary and secondary storage: 
Primary stage is access by the computer’s CPU while secondary storage is not accessed directly by the CPU
Primary storage has lower access time and smaller capacity
Primary is volatile and uses RAM, cache memory, or some other specialized hardware to store data while the computer is powered on, secondary storage is held in non-volatile devices
Primary storage holds currently running programs/data/operating system, secondary storage does not.

Operating System - a platform to support the applications 

Tree Set

Trees can be unbalanced - e.g. a tree where everything branches in one direction so it’s essentially just a 1D list
TreeSets are Java’s implementation of a self-balancing Tree
Our old BST code was also recursive, which makes it slow and inefficient

March 3, 2025
## Operating Systems

The OS is the core software that manages hardware resources and provides essential services for software applications
Memory Management
Requirement: dynamically allocate portions of the memory to programs on request. 
Memory allocation & deallocation - OS allocates memory blocks to programs, ensuring no overlap. Frees memory once a program finishes executing. 
Virtual memory - a technique to give the appearance of a large, contiguous block of memory to applications, even if the physical memory is limited.
Allows larger applications to run on systems with less RAM
The OS uses secondary storage when the RAM is insufficient to simulate more memory
Memory protection - keeps track of which processes are using which physical blocks of memory
One application cannot interact with another application’s memory
Ensures data integrity
Processor management
OS manages how the CPU executes processes, optimizing time-sharing between processes (scheduling)
Switches between tasks to provide the appearance of simultaneous execution
Security Management
Safeguard between the hardware and the applications
Confidentiality, integrity, availability
Authentication, authorization, process isolation, encryption, auditing and logging, security policies, malware protection, system updates

Encryption - obscuring information so that it can only be interpreted using a key

Device drivers - control things like keyboards, monitors, printers - act as translators between devices and the OS. 
March 4, 2025
## Practice questions

	loop I from 0 to 5
		STATION = Stats[I][0];
		FREQ = Radio[STATION]
		Q.enqueue(FREQ)
	end loop

	if (leverFlicked)
		item = Q.dequeue()
		output item
		Q.enqueue(item)
	end if
		


	List WithinThirty = new List()
	List BetweenFourteenAndThirty = new List()
	List MoreThanThirty = new List()

	while Customers.hasNext()
		currentCustomer = Customers.GetNext
		if(currentDate - currentCustomer.getPaymentDate > 30)
			MoreThanThirty.add(currentCustomer)
			currentCustomer.flagForDeletion()
		end if
		if(currentDate - currentCustomer.getPaymentDate > 14 AND currentDate - 				currentCustomer.getPaymentDate <= 30)
			BetweenFourteenAndThirty.add(currentCustomer)
			sendWarning(currentCustomer)
		end if
		if(currentDate - currentCustomer.getPaymentDate > -30)
			WithinThirty.add(currentCustomer)
			sendReminder(currentCustomer)
		end if

March 10-11, 2025
## Open Source Movement
Rejects secrecy and centralized control of creative work
In favor of decentralization, transparency, unrestricted sharing of information

Linux
a “kernel”, “the most operating system part of an operating system”
Acts as a bridge between applications and the data processing performed at the hardware level using inter-process communication and system calls
 
An OS:
Controls (peripheral) devices
Through the use of drivers (individualized “translation” programs)
e.g. mouse, printer, keyboard
Manages primary memory
Each program runs in its own allocated memory space
Virtual Memory
A feature of an operating system that allows a computer to compensate for shortages of physical memory by temporarily transferring pages go data from random access memory to disk storage. 
Manages secondary memory
Providing structure and access to these structures (folders, directories)
Provides interfaces
Including user interfaces

March 12-13, 2025
## Resource Management

Multitasking =/= multiprogramming
Multitasking - CPU switches rapidly between tasks
Multiprogramming - multiple programs are loaded in RAM at the same time

Short-term scheduling (CPU scheduling)
Time-slicing allows multiple processes to share CPU time.
Time-slice - small units of time allocated to a thread
Lifecycle of a process: New -> ready -> waiting -> running -> terminated 
Context switching - saving the state of a running process and loading the stake of another process. 
Allows multitasking by enabling the CPU to switch between processes efficiently, creating the illusion of parallel execution
Stop one task (either voluntarily (a slow process might cede priority to faster processes) or preemptively(when someone else decides that another thing will run)) and start another
Interrupt handling: when an I/O operation occurs, the CPU switches to another task
High-priority tasks may preempt lower priority ones
Context switching takes CPU time and adds latency. Frequent switching slows down performance
Scheduling algorithms improves efficiency
Round Robin - uses equal time slices for fairness
Priority Scheduling - runs high-priority tasks first
Multilevel Queue Scheduling - different priority queues

Linux - lots of freedom in terms of deciding priority
Process type - some things, like managing memory, night just be more important
Time sensitivity - UI response, I/O operations run before background calculations
CPU vs. I/O bound tasks -> I/O operations don’t use much CPU and complete faster
Aging Mechanism -> low priority processes gain priority over time to prevent starvation

March 17-18, 2025
## Application Software

Cloud computing - allows programs to run on servers and not local machines, reducing load
Downside: limited by network connection

March 19, 2025
## Polling & Interruption

The OS schedules tasks for the CPU to perform; higher priority tasks will preempt (interrupt) lower priority ones
It enforces time slicing using a hardware timer interrupt
The CPU is forced to switch processes periodically

The CPU is always executing instructions; To know if something else is going on, it can keep checking all the time (polling) or wait for an event (interrupt)?
Polling
Read input from keyboard buffer
Check if anything is there
No? Keep polling
Wastes time while running in a loop when nothing will have changed most of the time; the CPU is stuck checking the input buffer constantly; blocks all other processes; prevents multitasking

Interrupt
Devices notify the CPU when they need attention, causing the CPU to pause its current task, handle the event, and resume work. 
The CPU stops its current task and jumps to the Interrupt Service Routine associated with that interrupt type
The ISR processes the input (e.g. reading a keypress)
The ISR:
Saves the state of the current program to interrupt stack (a dedicated area of memory used to temporarily store the state of the CPU when an interrupt occurs)
Services the interrupt - performs all the necessary actions to handle the interrupt
Resumes normal CPU activity - restores the saved state of the interrupted program from the interrupt stack
Interrupts enable preemptive multitasking

Practice questions:

A control system is used to control sliding doors which automatically open to allow people in and out of a shop.
Define the term interrupt [2]
A signal sent to the processor sent by hardware or software that indicates that an event needs the OS/processor’s immediate attention.
Describe a situation in this system where an interrupt would occur [2]
When someone enters through the door the door will close behind them. When a second person walks toward the door, the process of closing the door must be interrupted by the higher priority task of opening the door for the second person. In this case the interrupt is sent by the sensor that detects the person. 

Outline the function of an interrupt [2]
An interrupt is a signal to the CPU sent by hardware or software, meant to alert the CPU to suspend execution of the current program and to transfer the control to the interrupt handler (which saves the state of the current program to the interrupt stack, services the interrupt, and resumes normal CPU activity)
Interrupts enable preempting

The temperature, humidity, light levels, and automatic watering of plants inside the greenhouses of a garden center are centrally monitored and controlled. Describe the difference between polling and interrupt in the event that some of the sensors malfunction. [3]
Polling is when the CPU checks constantly to know if something is going on. Interrupt is when the CPU runs until it is notified that something needs immediate attention.

In a polling system it will know that sensors have malfunctioned when they check every cycle to see if there is input data.
In a system that uses interrupts it will not know that the sensor has malfunctioned (unless it’s set with a timer)

E.g. the teacher asking the student “are you done with your homework” every minute will know immediately if the student is dead; a teacher who assumes a student is not done with their homework until they report back without checking on the student will think that the student is taking centuries to do their homework.

Policies - ways to ensure security

March 20, 2025
## Binary Representation
Byte - 8 bits
Kilobyte 10^3
Megabyte 10^6
Gigabyte 10^9
Terabyte 10^12

Kibibyte 2^10
Mebibyte 2^20
Gibibyte 2^30
Tebibyte 2^40


101 binary = 5 denary
101 decimal = 101 denary
101 decimal = 1100101 binary
101 hexadecimal = 100000001 binary
101 decimal = 65 hexadecimal

Without knowing what a chunk of binary is (a letter? A number?) it’s impossible to parse binary

Character set - like unicode, universal set of characters and unique code points
Encoding - a method of storing an d encoding unicode characters as binary data, from most common to least

Why did we change from ascii to unicode?
Ascii has a limited size and only supports a limited amount of characters -> problems if you want to use lots and lots of characters, 8-bits vs 16/32 bits
Unicode is the standard!
Different character encoding like UTF-8, UTF-16

March 21-24, 2025
Database Management Systems (DBMS)

Application software for creating and managing databases
Users and programmers use it to systematically create, retrieve, update, and manage data
DBMS/database —(API)—▷ Users and Apps
Unlike excel spreadsheets, databases have data types (like “strings” or integers)
Databases place restrictions on the things you get to change (hence, database management)
ACID properties (Atomicity, Consistency, Isolation, Durability)

Relational databases
SQL; Structured Query Language - language that DBMS understands
Create Read Update Delete - CRUD operations
Declarative - not concerned with order

JDBC - Java database connectivity 

Object Relational Mapping
ORM
Converts between Java objects and database tables
Avoids writing raw QL queries, removes SQL complexity
Mr. Gunn suggests ORMLite

March 21-26, 2025
## Simple Logic Gates


 Logic Tables


Order of precedence:
NOT AND NAND XOR OR NOR

NAND = (!A)||(!B) ≠ (!A)&&(!B) 
NOR = (!A)&&(!B) ≠ (!A)||(!B)

C && (A||B)


March 25, 2025
## Memory Management

Ensuring a program has sufficient memory to run
Prevents overwriting/clashing of data from different programs

Paging
Allows a process to use more memory than is physically available in the system (virtual memory)
Divides the memory into fixed-sized blocks called pages and stores them in secondary storage when they are not in use
Page tables map a process’ pages to physical frames.
Allows OS to manage and allocate memory more efficiently without the need for contiguous blocks of physical memory
Allows virtual memory
Page Replacement Algorithms
Least Recently Used - replaces the one that hasn’t been used for the longest time
FIFO
Optimal Page Replacement - replaces the page that will not be used for the longest time in the future (theoretical, not practical for real-time systems)
OS performs memory management and process management


!((A&&B)||!C)



!(A XOR B) AND C


Half Adder (no carry in) ^^ / Basic memory vv
Full adder (with carry in)

You can make anything with NAND


March 28 - April 7, 2025
## Networking Basics

Outline what is meant by the term computer network [2]
A group of computers and other computing hardware devices linked together through communication channels/cables/wirelessly
To enable communication between systems/among a wide range of users

Personal Area Network
Very short range
Connects personal devices: Bluetooth, USB
Usually peer-to-peer and temporary 
Without central networking device (communication is direct)

Local Area Network
Single building or small campus
Uses Ethernet cables, switches
High speed, owned and maintained privately
E.g. school network, office, home wired network
Ethernet: backbone of wired LANs, standard for wired Lan connections
Reliable and fast (1GB/s)
Most common LAN cable and port

Wireless LAN 
Same scope as LAN but wireless
Uses WiFi routers and wireless access points
Lower speed and more interference than LAN

Wide Area Network
Wider than a LAN
Less secure than LANs - connections through public networks, outside control of LAN, more potential for interception (encryption is critical!)
Slower than LANs - even though WANs typically use fiber-optic cables (much faster and more secure than ethernet) - WAN users have to share bandwidth 
Collection of other networks
Needs address (which LAN?)
Router to connect networks together

Why use a Private Network?
Restricted to internal use within an organization
Protected from unauthorized access
E.g. school LAN, company intranet
Secured by authentication, access rights, encryption, secure Wi-Fi, MAC filtering, firewall
Secure Wi-Fi - modern protocols like WPA3, encrypts data during transit, no eavesdropping

Confidentiality: authorized users can access information


Server: listens on a port, accepts requests, sends responses
Client: initiates the connection, sends requests, receives responses

Socket: combo of IP and Port
Programmatic endpoint that enables communication between a client and a server


Identify three ways in which the network administrator can reduce the risk of unauthorized access to confidential data [3]
Require users to be authenticated before they can access the data in the network
Different access rights for different people
Use latest WiFi protocol
Require MAC address authentication
Password
[Firewall is not an accepted answer because it’s trying to protect confidential data; in the same way that security guards don’t prevent students from looking at each other’s academic records]

Intranet: private network only accessible to an organization’s members of employees
Protected like any private network
Accessible only inside the organization (or via VPN)
Extranet: private network used for communication between different organizations
Allows secure communications between partners but not to “everyone”
Extension of intranet

VPN - Virtual Private Network
Creates a secure encrypted tunnel over the internet
Lets users access an internal network as if they were on-site
Used for remote work, private browsing, and secure access
Protects sensitive data from being intercepted in-transit
Bypasses geo-restrictions and maintain secure access
Authentication, tunneling(encapsulating data with different protocols like IPSec/TLS), encryption, VPN server decrypts and routes traffic inside the private network
Rise of home offices - telecommuting - workers can connect to a company’s internal network from almost anyone in the world
VPNs can protect agains phishing scams because they mislead scammers as to the location as the user 
VPN Clients make a “fake” network card and routes all the data through it

Distinguish between a VPN and an extranet [4]:
VPNs authenticates the sender before establishing the tunnel
VPN access is always encrypted, whereas extranet has limited encryption
VPN transmission is always encrypted
VPN users have access to everything whereas extranet users only have access to enabled specific services
Extranets can use VPNs

Outline one example of the use of a virtual private network (VPN) [3]:
VPNs can be used to protect against phishing scams
VPNs mislead scammers as to the location of the user by making it seem that the user’s request is being sent from the location of the server
Therefore scammers will have the wrong information and are less likely to trick the user

By making direct references to the technologies used, explain how a virtual private network allows a traveling salesperson to connect securely to their company’s network. [4]
VPN authenticates salesperson
VPNs create a secure encrypted tunnel over the internet
Servers route traffic inside the private network to let users access it as if they were on-site
Encryption prevents sensitive data from being intercepted in-transit

VLAN - Virtual Local Area Network
Save on physical switches - breaking one physical LAN into multiple VLANs
Each ethernet port configured to be part of a virtual LAN
Switch doesn’t send messages across the VLANs
Extending VLANs across multiple physical LANs so they will behave as if they were on the same physical LAN despite not being directly attached to the same physical LAN
Physical layout and logical layout are independent
 Broadcast - sent to all devices on a network

## Sample Network Stuff
March 28 - April 8, 2025

Sample code:

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.Socket;

public class TranslatorClient {
    public static void main(String[] args) {
        try {
            Socket socket = new Socket("localhost",806);

            BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);

            out.println("hello");
            String response = in.readLine();
            System.out.println("Server said: " + response);
            socket.close();

        } catch (IOException e) {
            throw new RuntimeException(e);
        }

    }
}


import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.ServerSocket;
import java.net.Socket;

public class TranslatorService {
    public static void main(String[] args) {
        try {
            ServerSocket server = new ServerSocket(806);
            System.out.println("Waiting for client..");
            Socket client = server.accept();
            System.out.println("Someone connected!!");

            BufferedReader in = new BufferedReader(new InputStreamReader(client.getInputStream()));
            PrintWriter out = new PrintWriter(client.getOutputStream(), true);

            String message = in.readLine();
            System.out.println("The client said" + message);
            if (message.equals("hello")) {
                out.println("你好");
            } else {
                out.println("再见");
            }
            client.close();

        } catch (IOException e) {
            throw new RuntimeException(e);
        }



    }
}


HTTP - Hypertext transfer protocol, port 80

Apr 16, 2025
## Centralized Data Storage Model

Mainframes - large centralized computers for batch processing
E.g. in a government agency or bank
Data and programs stored and run entirely on the mainframe
Reliable, secure

File Server -  computer attached to a network that provides a location for shared disk access
PCs request files from a central server

NAS - Network Attached Storage
A device optimized for storing serving files
Separate device
Often has multiple hard drives
Works over existing LAN

SAN - Storage Area Network
A specialized high-speed network that provides network access to storage devices
Consists of hosts, switches, and storage devices that are interconnected with a variety of protocols
Each machine can access shared storage as if it’s from a device directly attached to it
Disaster recovery - main data sites and backup sites (remote replication) - supports snapshots
Increased performance - highly specialized, independent from other networks, parallel data access
Availability - Redundancy


Database - software for organizing and retrieving data efficiently
Uses storage but not a storage model
Database can be stored on a local machine

Cloud storage
Service built on top of storage models like SAN

April 17, 2025
Peer-To-Peer Networks

Client-server model example - DHCP
Client automatically requests and IP address upon connection
DHCP server listens for requests, offers IP address, runs on router or server

World Wide Web
System of interlinked hypertext documents (html) and resources accessed via the internet using a web browser
Uses HTTP/HTTPS protocols to deliver content

P2P networks
where each device has equal status (theoretically)
Peers can act as both clients and servers - share things directly with each other
No central server
Redundancy/recovery
Resources more widely available
Supports file sharing & collaborative work

Example: blockchain
Distributed - spread across multiple computers
P2P networks - supposedly tamper-proof
Example: BitTorrent
Peer-to-peer protocol used to distribute large files efficiently across many users without needing a central server

April 18, 2025
## The Internet

Internet - A global network of interconnected…

Internet vs. Web
The internet is an infrastructure, the web runs on it
The Web uses websites and webpages; the internet includes everything that uses network protocols

Networking standards - define how devices can communicate, ensure compatibility between software & hardware, consistent and reliable data exchange

Layered communication
Customer - network interface (phone) - network 1 - router/gateway - network 2 - network interface
So that each layer only cares about a limited number of things

April 18-21, 2025
## OSI

Layers


Outline the concept of the Open Systems Interconnection model in the communication across a network [3]
The OSI is a standardized system/model for network connection consisting f 7 layers, each dealing with specific parts of network communication
Example.

Protocol - set of rules for data transmission
UDP - you don’t really know if it’s going to arrive
TCP - slower but you receive confirmation

Ensures devices can communicate properly
Ensures integrity - error checking - e.g. checksums, parity bits (always even numbers of 1s, so if an odd number of 1s is detected, it knows it’s corrupted)
Manage flow control - slows down the sender if the receiver is overwhelmed - prevents packet loss or overflow - e.g. receiver tells the sender how much it can receive right now (receive window)
Manage congestion - slows or reroutes packages as needed 
Prevent deadlock - prevents two devices from endlessly waiting on each other (e.g. timeouts)

April 22-28, 2025
## Packet Switching / other network stuff
Packet switching - a technique where data is broken into small packets that are sent individually across a network and reassembled at the destination
More efficient use of bandwidth
Resilient - us a different route if one route is down
Allows multiple conversations to happen on the same “road”

Data packet - formatted chunk of data, each with its own instructions (each packet knows where it’s going and how to be reassembled)
Header - like an envelope - source and destination - protocol (UDP? TCP?) - sequence number (like the page number)
Payload (uniform sizes)
Trailer (sometimes) - error checking codes (e.g. checksums) and control bits 

Routers and switches read the packet headers to route them
The packets may arrive out of order and are reassembled at the destination

Explain how data is transferred by packet switching [6]
Packet switching is a technique where data is split into small packets that are sent individually across a network (routed using switches and routers) and reassembled at the destination
Network switches and routers determine how best transfer the packet between a number of intermediate devices on the path to its destination rather than flowing directly over a single wire path to its destination
Each packet contains a uniform chunk of data
Each packet has a header, with the source, destination, protocol, and sequence number so that the receiver knows how to reassemble the packets once they arrive. The header is small.
Destination address so that each switch/routing station recognizes the address
Source address so that the data can be re-requested
Protocol so that the correct rules are followed
Each packet also has a trailer which is also small which contains transmission codes, error checking codes, and control bits so that the receiver knows if the data in the packet is correct and complete
If an error is detected an algorithm either corrects the error or requests that the packet is resent

Factors affecting transmission speed:
Network Congestion
Quality of connection
Distance
Protocol overhead. - extra data added by the communication protocols to manage the transmission e.g. headers, acknowledgments (UDP -> 8 bytes, TCP -> 20-60 bytes)
Device capability
Interference

Compression - encoding information using fewer bits than the original data entity 
Can be either lossless or lossy
Why? Less data to transmit, reduces bandwidth use, reduces cost of transmission
May increase amount of CPU time processing/decompressing


 Ethernet - most common LAN technology
Copper twisted pair
Used in offices and homes by switches and routers

Outline 2 reasons why there might be a reduction in data transmission speed at certain times [4]
High traffic causes slower speeds because bandwidth is limited so on average an individual user’s data will be transmitted at a lower rate, when there is less traffic speeds will be faster
Network interference? Someone is intermittently attacking the school?
Hardware malfunction - slow down if modem-router configuration is not correct


May 7, 2025
## Wireless Stuff/Technologies

Topologies - physical or logical layout of a network

Wireless networks: mobility - convenience - using your own device - coverage limitations depending on the location (deadlines, attenuation) - lower data transfer speeds than Ethernet - speed can fluctuate based on number of users

Repeater - boots an existing Wi-Fi signal, listens to existing Wi-Fi and rebroadcasts it (wirelessly)

Wireless Mesh Network:
Wireless access nodes added to each network user’s location
Contrast to star topology, where devices connect to a single central device (e.g, router); if the central device fails, the whole network goes down; bad things happen if a device gets too far with wireless
Complex, hard to manage large networks (Solution: use a wireless controller to centrally manage all the APs)

Wireless controllers - centrally manages multiple access points. Automatically updates settings, monitors performance, balances traffic. Improves network reliability and saves administrator time.

WiFi is not used everywhere because there are different use cases; not one standard fits all needs (range, speed, compatibility) 

Types:
LAN - WiFi (IEEE 802.11)
Tens of meters indoors, up to 1+ Gbps, convenient and widely supported but prone to interference and congestion
MAN (metropolitan)/rural WiMax
a.k.a Wireless Inter-operability for Microwave Access
Up to 50 km
Up to 70 Mbps
Great for rural areas or places with poor infrastructure
Higher latency, limited support
WAN: Cellular (3G, 4G, 5G)
3G - Cellular internet & voice, city to countryside via cell towers, up to 2 Mbps
4G - LTE - high-speed mobile broadband, wide area via cellular towers, global and reliable, not optimal for future IoT (Internet of Things) demands
5G - next-gen mobile, smart cities, IoT. Dense networks, varies with deployment. Up to 10Gbps. Low latency, ultra-fast, high capacity, but expensive and infrastructure-intensive.

May 9, 2025
## Network Security

Protects from unauthorized access, alterations, disruption (hackers, malware, system failures)

Confidentiality Integrity Availability
C: making sure data is kept secret of private. Access to information must be controlled
Sniffing unencrypted traffic, phishing to gain login credentials, network/file access without authorization
Encryption: prevents reading intercepted data, but requires key management and processing power
Strong authentication: something you know/something you have, more of a hassle
Anti-phishing systems: email filters, browser protection, blacklists, user training
Unauthorized access to network protected by MAC address filtering, which whitelists and blacklists devices but requires configuration on the router and MAC addresses can be spoofed
Stored files could be lost on a hardware device or through unauthorized access
Access rights - precisely applied to control file access, changes can apply to a large group
Must be well-managed; rights are centralized
I: making sure that your data is free from tampering and accurate
Threats:
Man in the middle attack - intercepts and alters data in transit. 
Protected by encryption and digital signatures
Private keys can be used to create a digital signature that can be checked with a public key
Provides strong validation but requires extra processing and infrastructure
Data corruption - data altered by error or attack
Protected by error checking
Checksums and hashing (a one-way encryption function, of sorts) are used to check if the data has changed
Efficient detection, but no prevention. Extra processing required.
A: Making sure that systems, networks, and applications myst be functioning as they should and when they should
Threats:
Distributed Denial of Service (DDoS) attack - server or service is overwhelmed by traffic - flooding a server with requests
A simple DOS attack is sent from one IP
A DDoS is sent from different sources
Protected by firewalls or intrusion prevention system
Power/hardware failure
Protected by redundancy
Universal power supply
Network segmentation
Threat: Malware - any software intentionally designed to cause damage, steal data, or disrupt systems 
Steals data (confidentiality) - spyware, trojans
Alters or protects data (integrity) - viruses, ransomware
Disrupts systems (availability) - ransomware, worms, DDoS
Protection:
User education
Anti-malware software
Backups
Use of sandboxing - running code in an isolated, secure environment
Clear company policies
Mobile Device Management (MDM)
A security system or software that allows network administrators to enforce policies, remotely wipe devices, control app installations, monitor device compliance
Used to manage the risk of bringing one’s own device 

Identify three ways in which the network administrator can reduce the risk of unauthorized access to confidential data in a WLAN sued to extend access to a school’s wired local area network. [3]
Give each user appropriate login details
Different access rights too students, teachers, and administrators
All passwords and files should be encrypted
Use latest WiFi protocol
Require MAC address authentication
Password protect the documents

A company has decided to replace their LAN with a WLAN. A WLAN will introduce additional security issues for the company. Discuss any two issues and the ways in which the company might resolve them
BYOD leading to insecure devices - clear company policy regarding use - use of sandbox - only approved devices - MAC addresses - only adding clean and tested devices - MDM services
Risk of interception as I goes through the air - use latest WiFi protocol - use of trusted MAC addresses, regular changes of router password

